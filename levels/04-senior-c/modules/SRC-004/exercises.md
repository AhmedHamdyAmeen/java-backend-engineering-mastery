# SRC-004 · Capacity planning — Exercises and lab

## Lab
### SRC-004-LAB1 · 10× capacity plan
**Outcomes:** 1–4 · **Time:** ~2.5 h
1. Build the forecast chain from business numbers to peak RPS, concurrency, and write rate for orders, inventory, Kafka, and PostgreSQL.
2. Estimate storage, network, and compute with multipliers (replication, retention, indexes).
3. Compare with the MID load-test data; find saturation points and headroom per component, including N-1.
4. Name the first bottleneck; write the plan with assumptions, margins, and re-planning triggers.
**Acceptance:** every number traceable to an assumption; first bottleneck named.

## Exercises (timed estimation; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| SRC-004-EX01 | 1 | Finance forecasts 5x orders next year and 10x on Black Friday. Derive peak RPS from 150k orders/day, with explicit assumptions. |
| SRC-004-EX02 | 1 | Estimate concurrent users and database connections needed at that peak. |
| SRC-004-EX03 | 2 | Estimate yearly storage for an orders table (1 KB rows, 2M/day) with indexes, replicas, and backups. |
| SRC-004-EX04 | 2 | Estimate Kafka disk for 3,000 events/s of 1 KB, replication factor 3, 7-day retention. |
| SRC-004-EX05 | 3 | A load test shows PostgreSQL saturates at 4,000 TPS; peak need is 3,200 TPS with one replica lost. Compute headroom and decide. |
| SRC-004-EX06 | 4 | Write a re-planning trigger set for the plan. |

## Solutions
- **EX01** Peak hour 12% of day gives 18k orders/h, about 5 orders/s; 10x gives 50/s; at 25 requests per order that is about 1,250 RPS, with a burst factor of 2 giving about 2,500 RPS design peak. Show the assumptions.
- **EX02** Little's Law: concurrency = RPS x latency, so 2,500 x 0.1 s is about 250 in-flight requests; database connections depend on the share needing DB time and query time; verify with a pool model.
- **EX03** 2M x 1 KB = 2 GB/day, about 730 GB/year; indexes x1.5 is about 1.1 TB; two replicas multiply to about 3.3 TB; add backups and WAL margin.
- **EX04** 3,000 x 1 KB = 3 MB/s; x 86,400 s x 7 days is about 1.8 TB; x 3 replicas is about 5.4 TB cluster-wide.
- **EX05** Headroom at full capacity is 20%, but if the lost replica shifted load the effective capacity may drop; if 3,200 is within 80% of 4,000, there is no N-1 margin; plan read offload or scale-up before the peak.
- **EX06** For example: peak CPU above 60% for a week; storage projection reaches 70% in 90 days; requests per order drifts 20% from assumption; forecast revision from Finance.

**Workplace evidence:** a capacity estimate you produced and later compared with actual usage.
