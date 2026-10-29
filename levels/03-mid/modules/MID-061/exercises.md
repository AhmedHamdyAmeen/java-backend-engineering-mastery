# MID-061 · Microservices introduction — Exercises and lab

## Lab
### MID-061-LAB1 · Split decision
**Outcomes:** 1–4 · **Time:** ~2 h
1. Collect evidence for each Shop module: load, change frequency, team ownership, data coupling.
2. Score each module against the extraction criteria.
3. Decide which modules to extract, if any.
4. Record the decision as an ADR: context, criteria, decision, consequences, review date.
**Acceptance:** ADR reviewed; "not extracting" is an acceptable outcome when justified.

## Exercises (assessment: ADR review; five exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-061-EX01 | 1 | Make a two-column table of microservice benefits and the conditions under which each really appears. |
| MID-061-EX02 | 1 | Take one in-process call in Shop and list everything that must be added when it becomes a network call. |
| MID-061-EX03 | 2 | Write a short argument for starting with a modular monolith for a 6-person team. |
| MID-061-EX04 | 3 | A colleague proposes "one service per entity" for Shop. Evaluate it with the criteria. |
| MID-061-EX05 | 4 | Review a description of 5 services that share a database and release together; name the problem and two fixes. |

## Solutions
- **EX01** For example: independent deployment needs independent code and data; scaling needs load evidence; ownership needs several teams.
- **EX02** Timeout, retry with backoff, idempotency, error mapping, authentication, tracing, versioned contract, and a partial-failure path.
- **EX03** Fewer moving parts, one deployment, local transactions, refactoring is cheap, boundaries still enforced by tooling; extract later when drivers appear.
- **EX04** Boundaries by entity ignore bounded contexts and create chatty calls and lockstep changes; apply criteria per capability, not per table.
- **EX05** It is a distributed monolith. Fixes: give each service its own data and API; merge back into a modular monolith where boundaries are unclear.
