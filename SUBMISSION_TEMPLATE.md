# Submission: <your-team-name>

Copy this file to `submissions/<your-team-name>/SUBMISSION.md` and fill in every section. Keep it structured but don't over-write it — a reviewer should understand your approach in under 5 minutes of reading, before they even run your code.

## 1. Team

- **Team / solo name:** (must match your branch name and folder name)
- **Members:**
- **Complexity level claimed:** L1 / L2 / L3 — pick one, and see section 4 for why it must be justified, not just asserted.

## 2. One-line summary

What does your scheduler optimise for, in one sentence?

## 3. The approach

Walk us through your algorithm or model in plain language first, then in as much technical detail as useful.

- **Inputs:** which datasets did you use (roster, calendar, hearing-type reference, substantive-ness probability, hearing-failure reasons, sample causelist)? Did you generate any additional data (e.g. scaling the 100-case roster to 3,000)? If so, how, and where's the script?
- **Core logic:** how do you decide what to hear, when, and how to pack a day? What's the actual scheduling/optimisation method (rule-based, greedy, constraint solver, ML-assisted, agent-based, etc.)?
- **Key decisions:** what did you have to choose that wasn't obvious from the data — and why did you choose it that way?
- **Assumptions made:** be explicit. Any distribution you assumed, any behaviour you modelled, any simplification you made instead of building the full thing — list it here. This is not a weakness to hide; unstated assumptions are worse than stated ones.

## 4. Justify your complexity level

Don't just claim L1/L2/L3 — show it:
- **L1 (fixed behaviour):** point to your fixed rules and your walkthrough.
- **L2 (dynamic + realistic data):** point to the specific distribution(s) you modelled, the cost/incentive/constraint you introduced, and what changes when a judge overrides a rule.
- **L3 (behavioural/agent-based):** point to the agent(s) you built, what decision(s) they make, and how their decisions feed back into the schedule.

## 5. Results

- How does your schedule perform against the five scoring dimensions from the case study — utilisation, predictability, substantiveness, backlog-age impact, next-date recommendation quality? Give numbers where you can, even rough ones.
- What does your visualisation show, and what decision could a judge actually make by looking at it? Include a screenshot or link if you have one.
- What happens differently in your model vs. the "default 60-day gap, whatever gets listed gets attempted" baseline in the case study?

## 6. Specs for integration

This is the part PUCAR will read most closely if your submission moves forward toward DRISTI 2.0 — be concrete, not aspirational.

- **Data schema:** what does your tool expect as input (columns/fields, formats), and what does it output? If you extended or changed the schema from what's in `data/`, document exactly what changed and why.
- **Interfaces:** is your tool a script, an API, a notebook, a web app? What would another engineer need to call it or embed it?
- **Dependencies:** language, libraries, any external services or models used.
- **What's stubbed vs. real:** be honest about what's a working implementation vs. a placeholder for the demo.
- **What integration would take:** in a few sentences, what would need to happen to plug this into a real court's system?

## 7. How to run it

```
# exact commands a reviewer should be able to copy-paste
```

## 8. What we'd build next

Given more time, what would you add or fix first? (Not scored, but tells us how you think.)

---
**Checklist before you open your PR:**
- [ ] No real case numbers, party names, or advocate names appear anywhere in this submission.
- [ ] Everything lives under `submissions/<your-team-name>/`.
- [ ] This file is filled in, not left as a template.
- [ ] Your code actually runs with the commands in section 7.
