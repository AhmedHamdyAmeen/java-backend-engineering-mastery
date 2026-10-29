# SRC-013 · Disaster recovery — Exercises and lab

## Lab
### SRC-013-LAB1 · DR drill
**Outcomes:** 1–4 · **Time:** ~4.5 h
Write a DR plan for the order subsystem: RPO and RTO per data set, backup and replication choices, failover steps including secrets, DNS, and config, and the rebuild path for Kafka-derived data. Run a timed recovery drill from simulated database loss and cluster loss, and report the results.
**Acceptance:** RTO and RPO met, or gaps documented with a remediation plan.

## Exercises (assessment: drill report review)
| ID | Outcome | Task |
| --- | --- | --- |
| SRC-013-EX01 | 1 | Set RPO and RTO for orders, payments, search index, session cache, and audit log; justify each from business impact. |
| SRC-013-EX02 | 2 | The orders RPO is 1 minute. Pick backup and replication mechanisms and explain what each covers and misses. |
| SRC-013-EX03 | 2 | Design Kafka recovery for the order events: replication, consumer offsets, and consumer requirements. |
| SRC-013-EX04 | 3 | Review a drill report that says "RTO 12 min" where the timer stopped when the database started. Identify the flaws. |
| SRC-013-EX05 | 4 | Case: the primary cloud region is unavailable for a day. Write the region-loss plan for the order subsystem, including prerequisites to prepare in advance. |
| SRC-013-EX06 | 1 | Case: a bad migration dropped a column at 10:00 and was noticed at 10:20. Explain why the replica does not help and what does. |

## Solutions
- **EX01** Orders and payments: RPO near zero to minutes, RTO 15 min; search index: rebuild, RPO hours; session cache: none, rebuild; audit log: RPO near zero, RTO hours. Rationale cites lost revenue, regulatory duty, rebuild cost.
- **EX02** Synchronous or near-synchronous replica handles node and zone loss; continuous log archiving with point-in-time recovery handles mistakes; backups in another account protect against account compromise. Replica misses logical corruption.
- **EX03** Replicated topics across zones, cross-cluster mirroring for region loss, offset translation or reset policy, idempotent consumers, topic configuration as code.
- **EX04** Timer should stop at verified service, not database start; missing app reconnect, secrets, DNS time to live, smoke tests; single run, no RPO measurement.
- **EX05** Pre-provision warm standby or pilot light, replicated data and secrets, infrastructure as code, DNS or traffic switch with low time to live, access paths, runbook, comms, failback plan, exercised.
- **EX06** The drop replicated within seconds. Use point-in-time recovery to just before 10:00 into a side instance, extract the lost data, and repair; this loses nothing if logs are intact.
- Outcome 3 is also covered by the lab drill and Q07-Q08.

**Workplace evidence:** a recovery exercise you planned or ran.
