# Scheduling Justice

**A PUCAR hackathon for FOSS United Week — give a High Court judge their day back.**

A judge's roster runs 3,000 cases deep. A typical day lists 60 hearings; the court reaches 20; only 10 move the case forward. Build the scheduling layer that decides, before the day starts, which cases actually get a shot — and show your work against real, anonymised court data.

| | |
|---|---|
| **Format** | 1 day. Solo or team; teaming up at the venue is fine. |
| **Input** | `data/roster_sample_100.csv` — 100 sample cases, bui
| **Scoring** | Scheduling logic — Utilisation, Predictability, Substantiveness, Backlog-age impact, Next-date sanity | Insight Visualisation
| **Complexity** | L1 (fixed schedule) → L2 (dynamic + realistic data) → L3 (behavioural / agent-based) — see the case study |
| **Submit by** | 4:30pm — pull request against this repo, ready for review |

Full context — the problem, the three judges' styles, the ask, and what "good" looks like — is in [`Scheduling Justice - Case Study.pdf`]([./Scheduling%20Justice%20-%20Case%20Study.pdf](https://drive.google.com/file/d/1yYbbY5ADWnRgNCkearerVrZsIPGjtxx5/view?usp=sharing)). Read that first. This README is the technical entry point.

## Repo layout

```
data/
  roster_sample_100.csv                 100-case sample roster (the docket you schedule against)
  court_calendar.csv                    working days, weekly offs, holidays
  hearing_type_reference.csv            real hearings-per-case stats + estimated duration & ideal gap, per hearing type
  hearing_failure_reasons.csv           real adjournment-reason breakdown, per hearing type (Kollam pilot data)
  substantiveness_by_hearing_type.csv   real probability a hearing of that type is substantive, per hearing type
  sample_causelist_2026-09-22.csv       a real day's causelist shape, to check your output against
  README.md                            what each file above contains
scripts/
  generate_roster.py                    scales roster_sample_100.csv up to a bigger synthetic roster
Scheduling Justice - Case Study.pdf  full problem statement
CONTRIBUTING.md                      how to submit — fork, branch, PR, and the structured write-up we need
```

## Quick start

```bash
# 1. The 100-case sample is already in data/. To generate a bigger roster (up to 3,000):
cd scripts && python generate_roster.py --num-cases 3000 --seed 42 --out ../data/roster_3000.csv

# 2. Build your solution — read data/roster_sample_100.csv and data/court_calendar.csv,
#    discuss your solutions and prototype them with your build

# 3. Score it
No SDK, no API, no required framework. The only contract is the `scheduling algorithm` and how well you are visualising the insight. Write your scheduler in Python, JS, Go, Rust — whatever you're fastest in.

## What you're scored on

Your solution to optimise a fixed capacity of a judge (420 minutes/day — the case study's 7-hour day) and prints:

| Metric | What it measures |
|---|---|
| **Utilisation** | % of available court minutes actually spent on hearings that were reached |
| **Reach rate** | % of what you scheduled the court actually gets to before time runs out |
| **Substantiveness** | % of reached hearings that move the case forward, vs. adjourned for nothing |
| **Backlog-age impact** | % of the oldest cases (4+ years) that get heard at all |
| **Predictability** | avg. gap, in days, between a case's first scheduled date and when it's actually heard |


## Constraints

- Schedule against the roster you were given or generated — `court_calendar.csv` only tells you which days are working days, it is not itself an input to schedule against.
- Anything not explicitly constrained here is a design decision — that's intentional. The case study's ask is a set of outcomes, not a spec.

## How to submit

See [`CONTRIBUTING.md`](./CONTRIBUTING.md) for the full process. Short version: fork this repo, build on a branch, open a pull request by 5pm with the structured write-up template filled in. We review every PR; the two strongest are merged and go forward to work with the Court Master and Justice Sehgal on DRISTI 2.0. Every other PR stays open as a public reference — anyone is free to fork and build on it after the hackathon.

## Where this data comes from

Hearing-type mix, hearings-per-case stats, and adjournment-reason breakdowns are calibrated to real, anonymised data from a district-court observations (~500 hearings). Case ages and daily volumes are scaled to match the case study's illustrative High Court roster (Justice Sehgal). **No real case numbers, party names, or advocate names appear anywhere in this repo** 
