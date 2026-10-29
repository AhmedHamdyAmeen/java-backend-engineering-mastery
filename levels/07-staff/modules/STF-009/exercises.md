# STF-009 · Engineering productivity — Exercises and lab

## Lab
### STF-009-LAB1 · Productivity baseline
**Outcomes:** 1–4 · **Time:** ~3 h
1. Measure Platform 2.0 feedback loops: build, test, review, deploy, onboarding (case data).
2. Run or analyze a developer-experience survey and cluster themes.
3. Pick the top two improvements where gains compound across teams.
4. Estimate engineer-hours saved per month with stated assumptions and quality counter-metrics.
5. Record the baseline for later comparison in the capstone.
**Acceptance:** baseline recorded so the improvement can be measured in the capstone.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| STF-009-EX01 | 1 | A VP wants a leaderboard of commits per engineer. Write a short reply proposing balanced indicators instead. |
| STF-009-EX02 | 1 | Choose eight indicators across delivery, experience, and cognitive load; name the source and level of each. |
| STF-009-EX03 | 2 | From a commit-to-production timeline with waits, find the three biggest delays and rank by total hours across teams. |
| STF-009-EX04 | 3 | A CI pipeline takes 40 minutes with 12% flaky failures. Propose a stepwise plan and how you would measure each step. |
| STF-009-EX05 | 4 | Estimate hours saved per month for a 10-minute pipeline reduction for 160 engineers and state the assumptions. |
| STF-009-EX06 | 2, 4 | Design an onboarding improvement with a metric, and write the case in three sentences for the VP. |

## Solutions
- **EX01** Explain gaming and trust damage; offer team-level lead time, change failure rate, experience survey; keep individual data out of reports.
- **EX02** Examples: lead time, deployment frequency, change failure rate, time to restore, survey on tooling satisfaction, time to first production change, review wait, cognitive load score.
- **EX03** Typical: review wait, CI queue, deploy approvals; rank by hours x teams affected.
- **EX04** Baseline; cache; parallel shards; quarantine flaky tests; one change per run; compare duration and flake rate.
- **EX05** Example: 160 x 3 runs x 10 min = 80 hours per day if each engineer waits, but not all wait fully; state a discount factor (for example 30%) and show the range per month.
- **EX06** Metric: time to first production change (target in days); one-command setup, buddy, starter task; payback from faster ramp-up.

Outcome coverage: all four outcomes appear in exercises and lab.

**Workplace evidence:** a productivity improvement you led with before/after data.
