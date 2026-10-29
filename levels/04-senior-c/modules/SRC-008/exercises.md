# SRC-008 · Architectural decomposition — Exercises and lab

## Lab
### SRC-008-LAB1 · Boundary review
**Outcomes:** 1–4 · **Time:** ~2 h
1. Map Shop Platform's services, owning teams, and databases.
2. Mine Git history for change coupling; add data, deployment, and runtime coupling evidence.
3. Apply explicit criteria (team topology, change coupling, scaling, fault isolation).
4. Recommend one split and one merge, or justify none; outline migration path and exit criteria.
**Acceptance:** recommendation backed by data and team considerations.

## Exercises (boundary defense; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| SRC-008-EX01 | 1 | A VP wants the order module extracted "for scalability". List the evidence you need and the criteria you apply. |
| SRC-008-EX02 | 2 | Given a co-change table, interpret three pairs and say which need follow-up. |
| SRC-008-EX03 | 2 | Classify five symptoms by coupling kind (code, data, deployment, temporal, change). |
| SRC-008-EX04 | 3 | Two services share a database, release together, and call each other 12 times per request. Recommend an action with a plan. |
| SRC-008-EX05 | 4 | Draft a staged migration for extracting notifications with exit criteria per stage. |
| SRC-008-EX06 | 1 | Evaluate "one service per noun" for Shop Platform with the criteria. |

## Solutions
- **EX01** Load profile per module, change rate, team ownership, failure isolation need, data coupling; if only scaling is claimed, show load data and consider cheaper fixes first.
- **EX02** High co-change across services (for example orders and inventory in 70% of commits) needs follow-up; same-module pairs are expected; verify noise and merges.
- **EX03** Shared library: code; shared table: data; must release together: deployment; synchronous call required: temporal; files change together: change.
- **EX04** Merge: shared data and lockstep releases make it a distributed monolith; plan: align the code, merge deployments, keep modules inside, measure release time and incidents.
- **EX05** Stage 1 enforce module boundary; stage 2 separate data; stage 3 deploy service behind a flag; stage 4 remove the old path; exits: latency and error budgets, rollback if exceeded.
- **EX06** Boundaries by noun ignore change patterns and teams, producing chatty services; use capabilities and evidence instead.

**Workplace evidence:** a decomposition or consolidation decision you contributed to, with its outcome.
