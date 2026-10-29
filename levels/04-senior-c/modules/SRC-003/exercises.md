# SRC-003 · Architecture trade-offs — Exercises and lab

## Lab
### SRC-003-LAB1 · Option analysis
**Outcomes:** 1–4 · **Time:** ~2 h
1. Take the utility tree from SRC-002; list the decisions for scaling the order subsystem and mark one-way doors.
2. Define three candidate designs; describe each at its strongest.
3. Evaluate each against the top scenarios with a lightweight ATAM-style review; include complexity and operational cost.
4. Record risks, sensitivity points, and trade-off points.
5. Write an ADR for the chosen design, including rejected options.
**Acceptance:** rejected options documented with honest strengths.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| SRC-003-EX01 | 1 | Sort twelve order-subsystem decisions into one-way and two-way doors and say where design effort should go. |
| SRC-003-EX02 | 2 | Evaluate "add a Kafka-based outbox" against two utility-tree scenarios using the scenario-by-option grid. |
| SRC-003-EX03 | 3 | Estimate the complexity cost (components, runbooks, pages, onboarding) of introducing a service mesh for a team of six. |
| SRC-003-EX04 | 3 | A colleague wants a generic repository layer "to swap databases". Argue for or against with costs. |
| SRC-003-EX05 | 4 | Classify four findings as risk, sensitivity point, or trade-off point and record each with scenario and owner. |
| SRC-003-EX06 | 2 | Review an ADR with a strawman alternative; rewrite the alternative honestly and re-decide. |

## Solutions
- **EX01** One-way: shard key, public API shape, event schemas, cloud region and vendor, data model. Two-way: library choices, internal refactors, pool sizes. Spend analysis on the first group; make the second quickly and revisit.
- **EX02** Outbox improves durability and consistency of event publishing (+), adds a relay process and lag monitoring (-), neutral on checkout latency; the grid names the reason per cell.
- **EX03** Adds control plane, sidecars, certificate rotation, new failure modes, mesh-specific debugging; likely not worth it for six engineers unless a requirement (mTLS everywhere) demands it.
- **EX04** Against: JPA and SQL features leak through; cost is indirection and lost features; benefit speculative. For: only if two real implementations are needed now.
- **EX05** Examples: single primary at 10x peak is a risk; replica lag is a sensitivity point; synchronous replication is a trade-off point (durability vs commit latency).
- **EX06** A fair alternative states its real benefit (for example simpler operations), then compares on scenarios; the decision may change or be confirmed with stronger reasons.

Outcome 4 is also covered by the lab ADR.

**Workplace evidence:** an ADR or design review where you recommended against a more complex option.
