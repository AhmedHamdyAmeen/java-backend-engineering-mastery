# STF-005 · Organization-wide reliability — Exercises and lab

## Lab
### STF-005-LAB1 · Reliability program
**Outcomes:** 1–4 · **Time:** ~3 h
1. Take a year of Platform 2.0 incident reports (case materials) and tag them with a common scheme.
2. Identify three systemic causes with counts and affected teams.
3. Design the program: SLO coverage, postmortem quality, action follow-through, on-call health, each with a target and owner.
4. Add a maturity self-assessment to direct help.
5. Draft a one-page leadership report with trends and requested decisions.
**Acceptance:** program targets are measurable and tied to the systemic causes.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| STF-005-EX01 | 1 | Given a table of 20 incidents with causes, group them into systemic and one-off causes and justify. |
| STF-005-EX02 | 1 | A postmortem says "engineer ran the wrong command". Rewrite the finding to expose the systemic cause and the fix. |
| STF-005-EX03 | 2 | Set targets for SLO coverage, action-item follow-through, and postmortem quality; define how each is measured. |
| STF-005-EX04 | 3 | Design a five-practice maturity grid and show how you would use it to pick three teams for help. |
| STF-005-EX05 | 3 | Review on-call data (pages per week, share actionable) for four rotations and recommend actions in priority order. |
| STF-005-EX06 | 4 | Write a one-page quarterly summary for the CTO translating reliability data into business risk and two decisions. |

## Solutions
- **EX01** Systemic: recurring across several teams (rollback gaps, alert gaps). One-off: single team, unique trigger. Show counts.
- **EX02** Missing guardrail: confirmation or environment labeling, access limits, automation; fix is a safer tool, not blame.
- **EX03** Examples: 80% of tier-one services with SLOs in two quarters; 90% of actions closed within 60 days; postmortems reviewed against a template with contributing factors. Measure from the SLO catalog and the tracker.
- **EX04** Practices: monitoring, SLOs, tested rollback, runbooks, game days. Pick teams that own critical paths and score lowest.
- **EX05** Fix highest noise first, then rotation size, then runbooks; escalate rotations above the paging target.
- **EX06** Show revenue-minutes at risk, trend arrows, top three risks, cost of the investment asked for.

Outcome coverage: all four outcomes are covered by the exercises and lab.

**Workplace evidence:** a reliability program or systemic fix that reduced repeat incidents across teams.
