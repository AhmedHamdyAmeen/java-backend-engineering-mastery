# MID-044 · Data selection — Exercises and lab

## Lab
### MID-044-LAB1 · Datastore ADRs
**Outcomes:** 1–3 · **Time:** ~2 h
Write one ADR each for Shop's catalog, orders, reviews, search, and sessions. Each ADR has context, workload characterization with evidence, options, decision, consequences, operational cost, and a revisit trigger.
**Acceptance:** each cites workload evidence; at least one concludes "PostgreSQL is enough".

## Exercises (assessment: ADR review)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-044-EX01 | 1 | Characterize the sessions workload with the template (access, volume, consistency, latency, flexibility). |
| MID-044-EX02 | 2 | Pick a store for each: orders, product search, rate-limit counters, product reviews at 2 M rows; justify in one line. |
| MID-044-EX03 | 3 | List the operational costs of adding MongoDB to a team that runs only PostgreSQL. |
| MID-044-EX04 | 2 | Review this ADR: "We use MongoDB because it is modern and scalable." List what is missing. |
| MID-044-EX05 | 2 | Write the revisit triggers for the reviews ADR. |

## Solutions
- **EX01** Point lookups by token, high read and write, small values, short TTL, loss tolerable (re-login), latency milliseconds, no query flexibility: a key-value store with TTL.
- **EX02** Orders: PostgreSQL (transactions). Search: OpenSearch if facets and typos matter, else PostgreSQL FTS. Counters: Redis. Reviews at 2 M rows: PostgreSQL is enough.
- **EX03** Provisioning, backup and restore tests, monitoring and alerts, upgrades, security, runbooks, skills and on-call, data sync and consistency.
- **EX04** Workload numbers, alternatives considered, consequences, operational cost, revisit trigger, and why PostgreSQL was rejected.
- **EX05** Example: review volume above 200 M, write rate above 5 000/s, or read latency targets missed after indexing and partitioning.

**Outcome 1** is also covered by the lab (workload evidence in each ADR).
