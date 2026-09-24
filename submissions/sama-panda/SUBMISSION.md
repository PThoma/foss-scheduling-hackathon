# Submission: sama-panda

## 1. Team

- **Team / solo name:** sama-panda
- **Members:** Sama team 4 (P&A)
- **Complexity level claimed:** L1 — readiness gate (defects → READY/BLOCKED/HEALING) plus fixed-rule minute packer into List 1 / List 2 with +25% overbook and ageing score.

## 2. One-line summary

Only READY cases enter the day packer; the packer fills judge sitting blocks by duration table + ageing, with a 25% overbook buffer, and waitlists the rest for lack of minute capacity.

## 3. The approach

- **Inputs:** Local `data/roster_3000.csv` (synthetic scale of the hackathon roster), `data/court_calendar.csv` (working days / holidays), hearing-type duration defaults, fixed purpose→defect catalog. Generator notes live in README; we do not overwrite repo-root `data/`.
- **Core logic (readiness):** Normalize purpose/stage → attach required defect codes → keyword overlays on `last_hearing_summary` → `recompute_readiness`: only **blocking** open defects gate READY (soft defects warn). Party/counsel actions → submitted; registry verify/waive/reject. Soft↔blocking toggles via judge **Defect policy**.
- **Core logic (packer):** `POST /generate` takes READY pool for a working day, packs by duration mins into sitting blocks (Zeng-style expected load + overbook %), ranks by ageing score, returns listed + waitlisted (`no_capacity`). Week mode chains days with `exclude_case_numbers` so later days take the next tranche.
- **Key decisions:** Soft defects do not block listing; holidays refused unless `force_holiday`; demo seed is explicit (`POST /seed/demo` / Overview button) — empty DB stays empty until seeded.
- **Assumptions:** Seed invents defects (roster has no preparedness fields); auth is stub header `X-Actor-Role`; uploads are URI/note refs.

## 4. Justify your complexity level

- **L1 (fixed behaviour):** Fixed catalog (`src/catalog.py`), deterministic readiness (`src/readiness.py`), fixed duration table + greedy minute packer (`src/packer.py` / generate), Gherkin-style pytest. No ML, no agents, no learned distributions.
- **L2 / L3:** Not claimed.

## 5. Results

- After seed of 3,000: roughly ~269 READY / ~2731 BLOCKED (varies with policy). A working day packs ~13 cases into ~420 mins (~93% of budget); remainder waitlisted for minute capacity, not defects.
- **Visualisation:** Local UI (`ui/artifacts/court-time-planner`) — Overview (empty→Seed 3k), Roster, Eligibility, Cause List (Calendar gantt / List + Generate), Defect policy, Registry queue, case defect chips (Blocking / Soft / By law).
- **Vs baseline 60-day dump:** Defective matters stay off eligibility until cleared; listed set is capacity-aware instead of “whatever CIS dumps.”

## 6. Specs for integration

- **Data schema:** Roster CSV columns as hackathon sample; eligibility JSON (`case_number`, UPPER_SNAKE purpose, cleared codes, duration estimate, …). SQLite: `cases`, `defects`, `audit_log`, `drafts`, policy + judge prefs.
- **Interfaces:** FastAPI `src/main.py` + Vite/React UI. Stub `X-Actor-Role: registry|counsel|party`.
- **Dependencies:** Python 3.10+, fastapi, uvicorn, pydantic, pytest; UI via pnpm in `ui/`.
- **Stubbed vs real:** Auth header stub; no blob store; no eCourts webhooks; calendar from CSV.
- **Integration:** Point roster ETL at CIS export; SSO for actors; document store for evidence_uri; scheduler consumes `GET /eligibility` / `POST /generate`.

## 7. How to run it

```bash
cd submissions/sama-panda
python3 -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
# optional empty start — seed from UI (Seed demo roster) or:
# curl -X POST localhost:8000/seed/demo
uvicorn src.main:app --reload --host 127.0.0.1 --port 8000

# UI (second terminal)
cd ui/artifacts/court-time-planner
pnpm install
PORT=5173 BASE_PATH=/ pnpm dev
# → http://127.0.0.1:5173/

# smoke
curl -s localhost:8000/stats
pytest -q src/tests
```

Reset to empty without reseeding: `curl -X POST localhost:8000/reset`

## 8. What we'd build next

Expire HEALING deadlines; bulk process-return for warrant clusters; richer Impact/Finalise flows; live CIS roster ETL.

---
**Checklist before you open your PR:**
- [x] No real case numbers, party names, or advocate names appear anywhere in this submission.
- [x] Everything lives under `submissions/sama-panda/`.
- [x] This file is filled in, not left as a template.
- [x] Your code actually runs with the commands in section 7.
