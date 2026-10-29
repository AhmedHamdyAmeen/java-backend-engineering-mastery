# ARC-016 · Database architecture — Exercises and lab

## Lab
### ARC-016-LAB1 · Larkspur data platform
**Outcomes:** 1–4 · **Time:** ~3.5 h
1. List Larkspur data workloads and their access patterns and consistency needs.
2. Choose a data store per workload and name the source of truth.
3. Design replication, read scaling, and failover per store.
4. Define backup, PITR window, RPO, and RTO per store and compare with requirements.
5. Write the migration approach for the current web shop database (method, cutover plan, rollback).
**Acceptance:** each store's RPO/RTO meets requirements or the gap is flagged.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| ARC-016-EX01 | 1 | Choose a store for carts, orders, product search, and a catalog read cache; justify each. |
| ARC-016-EX02 | 1 | List what Larkspur still owns after adopting a managed relational database. |
| ARC-016-EX03 | 2 | The reporting queries slow the order database. Propose a design and its staleness trade-off. |
| ARC-016-EX04 | 2 | Explain the difference between a multi-AZ standby and a read replica, with an example failure of each. |
| ARC-016-EX05 | 3 | A developer deleted rows at 14:05. Describe how to recover and what RPO the design gives. |
| ARC-016-EX06 | 4 | Outline a migration plan for the web shop database with 200 GB, a nightly low-traffic window, and a four-hour downtime limit. |

## Solutions
- **EX01** Carts: key-value/document (simple, fast); orders: relational (transactions); search: managed search fed from the catalog; cache: in-memory cache, source of truth stays relational.
- **EX02** Schema, indexes and queries, sizing, access and encryption, monitoring, restore testing, upgrade planning, cost.
- **EX03** Add a read replica for reporting; accept replication lag of seconds to minutes; reports must tolerate stale data.
- **EX04** Standby: survives zone failure with automatic failover, no extra read capacity. Replica: serves reads, may lag, promotion is a manual or scripted step.
- **EX05** PITR to 14:04 into a new instance, copy back the rows, or switch with care; RPO is minutes, bounded by the log retention and backup configuration.
- **EX06** Replicate continuously from on-premises, validate, rehearse, freeze writes in the window, final sync, switch connection, keep the old database read-only as the rollback; downtime minutes, within four hours.

**Workplace evidence:** a data platform design you led to production.

---
Outcome coverage: all outcomes covered by exercises and the lab.
