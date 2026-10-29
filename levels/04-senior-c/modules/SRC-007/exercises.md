# SRC-007 · Database scaling — Exercises and lab

## Lab
### SRC-007-LAB1 · Order data at 10×
**Outcomes:** 1–4 · **Time:** ~2.5 h
1. Quantify the 10× need from SRC-004 (reads, writes, size) against the current single-primary limits.
2. Walk the scaling ladder with evidence; decide among replicas, partitioning, sharding, or managed distributed SQL.
3. If sharding, choose the key from real distribution data and quantify hot-partition risk.
4. Write the ADR and a migration outline with resharding and rollback.
**Acceptance:** hot-partition risk quantified.

## Exercises (shard-key scenarios plus ADR; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| SRC-007-EX01 | 1 | A "my orders" page shows missing orders after checkout when using replicas. Diagnose and design a lag-aware fix. |
| SRC-007-EX02 | 2 | Given measurements (CPU 85%, 90% reads, write rate 40% of limit), decide the next rung of the ladder and justify. |
| SRC-007-EX03 | 3 | Evaluate customer id, order id hash, and region as shard keys for the three main order queries. |
| SRC-007-EX04 | 3 | Top 1% of customers produce 30% of orders across 8 shards. Estimate hot-shard load and propose a mitigation. |
| SRC-007-EX05 | 3 | Outline a resharding plan from 4 to 8 servers. |
| SRC-007-EX06 | 4 | Compare managed distributed SQL with sharded PostgreSQL for the order database and name the proof-of-concept tests. |

## Solutions
- **EX01** Replica lag; route read-your-writes to the primary (or wait for LSN), monitor lag, fall back above a threshold, add a test.
- **EX02** Reads dominate, so read replicas plus caching; write headroom is fine; sharding is premature.
- **EX03** Customer id fits "my orders" and customer-scoped queries; order id hash spreads evenly but scatters customer queries; region is low cardinality. Choose customer id, with a lookup for order by id.
- **EX04** If the top 1% land in one shard that could mean 30% of load on a shard expected to take 12.5%, roughly 2.4x average; mitigate with salting, splitting large tenants, or extra capacity for that shard.
- **EX05** Use logical shards; create new servers, copy and replicate changes for moved logical shards, verify, cut over by updating the mapping, clean up; keep rollback until verified.
- **EX06** Test transaction latency, cross-shard joins, failover time, compatibility of queries and extensions, cost at 10x, migration effort; compare operating burden.

**Workplace evidence:** a database scaling change you designed or reviewed.
