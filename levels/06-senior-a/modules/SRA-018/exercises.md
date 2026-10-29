# SRA-018 · Organizational bottlenecks — Exercises and lab

## Lab
### SRA-018-LAB1 · Team design proposal
**Outcomes:** 1–4 · **Time:** ~2 h
1. Analyze provided dependency data for Commerce 2030 teams: cross-team change share, wait times, and handoffs.
2. Assess cognitive load for the teams at the bottleneck.
3. Propose team boundary changes aligned with the Commerce 2030 context map, paired with the architecture changes needed.
4. Present to role-played engineering managers; adjust to their constraints.
5. Predict the reduction in measured dependencies and define how you will check it.
**Acceptance:** proposal reduces measured cross-team dependencies.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| SRA-018-EX01 | 1 | Explain Conway's Law with an example from the dependency data and describe how the inverse Conway maneuver would respond. |
| SRA-018-EX02 | 2 | From a table of tickets, compute each team's share of changes needing another team and identify the top bottleneck. |
| SRA-018-EX03 | 4 | Assess cognitive load of a team owning four domains and nine services and recommend actions. |
| SRA-018-EX04 | 3 | Propose a split for that team aligned with the context map, with interfaces and data ownership. |
| SRA-018-EX05 | 3 | Prepare the manager conversation: data, options, transition, and decisions needed from them. |
| SRA-018-EX06 | 1 | Critique a proposal that reorganizes teams but leaves the shared database unchanged. |

## Solutions
- **EX01** A shared table between ordering and inventory teams that must agree on every release shows the mirror; the inverse maneuver gives each domain one owning team and a clear interface.
- **EX02** Count changes per team, flag those needing another team, rank by wait time; the team most waited on is the bottleneck, but check why before acting.
- **EX03** Load is high: split by subdomain, reduce services through consolidation or a platform capability, and limit on-call burden; move ownership before code.
- **EX04** Pricing and promotions to one team, seller fees to the seller domain team; each owns its data and a published interface; predict fewer cross-team changes.
- **EX05** Bring data, target architecture, two or three options, effect on people and careers, transition steps, and the decision needed; let managers own people decisions.
- **EX06** Without changing the shared database the coupling persists and the new teams still coordinate; pair the team change with data ownership and interface steps.

Outcome 4 is also covered by the lab load assessment.

**Workplace evidence:** a team-boundary or ownership change you influenced and its effect.
