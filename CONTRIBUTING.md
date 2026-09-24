# Contributing to Scheduling Justice

Thanks for hacking on this. Here's exactly how to get your work into this repo.

## 1. Fork and branch

1. Fork this repository to your own GitHub account (top-right "Fork" button).
2. Clone your fork locally:
   ```
   git clone https://github.com/<your-username>/foss-pucar-hackathon.git
   cd foss-pucar-hackathon
   ```
3. Create a branch named after your team or your own name (lowercase, hyphens, no spaces):
   ```
   git checkout -b team-<your-team-name>
   ```
   This branch name must match your folder name in `submissions/` (see below) and the "team/solo name" you put in your PR.

## 2. Where your code goes

Everything you build lives under a single folder inside `submissions/`, named after your team:

```
submissions/
└── <your-team-name>/
    ├── SUBMISSION.md          ← copied from SUBMISSION_TEMPLATE.md, filled in
    ├── proposed_schedule.csv  ← (or your equivalent output) the schedule your tool produces
    ├── src/                   ← your code
    └── ...                    ← anything else you need (notebooks, viz, etc.)
```

Do not edit anything outside your own `submissions/<your-team-name>/` folder. Do not touch other teams' folders, `data/`, or the case study PDF.

## 3. Working with the data

Pull whatever you need from `data/` (see `data/README.md` for what each file contains). If you generate additional synthetic cases (e.g. to scale the 100-case roster up to 3,000), put your generator script in your own submission folder and note it in `SUBMISSION.md` — don't overwrite the files in `data/`.

**No real case numbers, party names, or advocate names may appear anywhere in your submission** — the provided data is already anonymised; keep any data you generate that way too.

## 4. Opening your PR

1. Commit your work to your branch and push it to your fork:
   ```
   git add submissions/<your-team-name>
   git commit -m "Add <your-team-name> submission"
   git push origin team-<your-team-name>
   ```
2. On GitHub, open a Pull Request from your fork's branch into this repo's `main` branch.
3. Fill in the PR checklist that appears automatically (from `.github/PULL_REQUEST_TEMPLATE.md`) — it mirrors what's required in `SUBMISSION.md`.
4. **Your PR must be open before 5 PM.** Late PRs won't be reviewed.

If you're not comfortable with the command line, GitHub's web UI also lets you fork, create a branch, and upload files directly — use the "Add file → Upload files" option inside your forked repo's `submissions/<your-team-name>/` path, then open the PR from there.

## 5. What happens after 5 PM

- All PRs remain open and public in this repo — every team's work is visible and reusable, whether or not it wins.
- The panel reviews all submissions using the criteria in the case study PDF (scheduling performance + visualised insight + complexity level).
- **Only the winning team's (or two teams') PR gets reviewed for merge into `main`.** Everyone else's PR stays open as a public reference submission — it will not be merged, but it will not be deleted either.
- The winning submission(s) move forward for integration into the DRISTI 2.0 stack, and the team works directly with the Court Master and Judge afterwards.

## Questions during the hackathon

Open a GitHub Issue on this repo, or ask in the room — don't block on it, simplify and keep building.
