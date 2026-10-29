# SRB-001 · Distributed architecture patterns — Exercises and lab

## Lab
### SRB-001-LAB1 · Shipment tracking design
**Outcomes:** 1, 2, 3, 4 · **Time:** ~4.5 h
1. List FulfillCo's shipment tracking requirements (status, history, corrections, partner feed, audit).
2. Design option A: event-sourced; option B: state plus outbox.
3. Estimate replay time, schema evolution effort, and storage for each at expected volume.
4. Write an ADR with the decision, rejected option, and revisit triggers.
**Acceptance:** operational costs (replay time, schema evolution, storage) estimated for both options; ADR records the decision.

## Exercises
| ID | Outcome | Task |
| --- | --- | --- |
| SRB-001-EX01 | 1 | Your read screens need a different shape but load is light. Choose CQRS-lite or full CQRS and justify. |
| SRB-001-EX02 | 2 | List three costs of event sourcing for shipment tracking that a state table would not have. |
| SRB-001-EX03 | 2 | A v1 event lacks a field the new projection needs. Describe the upcasting approach. |
| SRB-001-EX04 | 3 | Shop shows carrier status from FulfillCo. Define acceptable staleness and the reconciliation job. |
| SRB-001-EX05 | 4 | Three workflows exist, each two steps with no timers. Engine or hand-built saga? Argue. |
| SRB-001-EX06 | 1 | Review a proposal to event-source the product catalog. Write a five-line critique. |

## Solutions
- **EX01** CQRS-lite: SQL views or separate read classes on the same database; full CQRS adds a second store and lag for no needed gain.
- **EX02** Replay time for rebuilds, permanent event schema and upcasting work, harder ad hoc queries and deletion of personal data.
- **EX03** Add an upcaster mapping v1 to v2 with a default or derived value on read; do not rewrite history unless unavoidable.
- **EX04** e.g. status within 30 s of the event, timestamp shown; a nightly job compares counts per status and repairs gaps by re-consuming.
- **EX05** Hand-built with an outbox and state table: small, short, no timers; revisit if workflows grow.
- **EX06** Catalog history is rarely business-critical, reads dominate, edits are simple; an audit history table suffices; propose a spike measuring need first.

**Workplace evidence:** a design where you chose a simpler pattern over a fashionable one and could show why.
