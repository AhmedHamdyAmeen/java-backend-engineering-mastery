# SRB-008 · Architecture migration — Exercises and lab

## Lab
### SRB-008-LAB1 · Migration plan
**Outcomes:** 1, 2, 3, 4, 5 · **Time:** ~4.5 h
1. Map the monolith's shipment tracking and carrier integration.
2. Plan phases with routing, branch by abstraction, and data migration.
3. Define rollback and measurable exit criteria per phase.
4. Defend the plan to role-played FulfillCo teams.
**Acceptance:** no phase requires both systems to write the same data; rollback and metrics for every phase.

## Exercises
| ID | Outcome | Task |
| --- | --- | --- |
| SRB-008-EX01 | 1 | Argue against a proposed two-year rewrite of FulfillCo in five lines. |
| SRB-008-EX02 | 1 | Choose the first extraction candidate among shipment tracking, stock, and billing and justify. |
| SRB-008-EX03 | 2 | Sketch the interface and flag for branch by abstraction of carrier calls. |
| SRB-008-EX04 | 3 | A teammate proposes a temporary dual write. Write the objections and the alternative. |
| SRB-008-EX05 | 4 | Plan the data ownership cut-over for tracking history. |
| SRB-008-EX06 | 5 | Write exit criteria for the 50% traffic step. |

## Solutions
- **EX01** Moving target, hidden behavior, no early value, hard to stop; propose strangler steps.
- **EX02** Shipment tracking: bounded, high value to Shop, lower risk than stock or billing.
- **EX03** CarrierGateway interface with legacy and remote implementations; flag per carrier.
- **EX04** Non-atomic, drift risk; use CDC or outbox with a single writer.
- **EX05** Backfill, one-way CDC sync, verify, switch writer behind a gate, reverse window, retire.
- **EX06** Error rate within 0.1% of legacy, zero unreconciled records for 7 days, rollback tested.

**Workplace evidence:** a strangler or extraction step you led into production.
