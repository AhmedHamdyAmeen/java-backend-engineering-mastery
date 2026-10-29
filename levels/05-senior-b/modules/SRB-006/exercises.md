# SRB-006 · Large-scale messaging — Exercises and lab

## Lab
### SRB-006-LAB1 · Partner feed at scale
**Outcomes:** 1, 2, 3, 4, 5 · **Time:** ~3.5 h
1. Estimate volume (50x Shop orders) and growth for three years.
2. Design topics, keys, partition counts, and consumer groups.
3. Define lag alerts, action plans, and a backlog-recovery plan.
4. Run a load test that simulates a backlog and measure catch-up time.
**Acceptance:** load test proves catch-up time within target; lag alerts have action plans.

## Exercises
| ID | Outcome | Task |
| --- | --- | --- |
| SRB-006-EX01 | 1 | Choose partition count for 20,000 msg/s with 2,000 msg/s per consumer and 3x growth. |
| SRB-006-EX02 | 1 | Pick the key for shipment events and justify. |
| SRB-006-EX03 | 2 | Write two lag alerts with thresholds and first actions. |
| SRB-006-EX04 | 3 | A rolling deploy causes repeated stop-the-world rebalances. Propose fixes. |
| SRB-006-EX05 | 4 | Design backpressure for ingest from partner HTTP to Kafka to DB. |
| SRB-006-EX06 | 5 | Compute storage for 5,000 msg/s x 1 KB, 7 days, replication 3. |

## Solutions
- **EX01** At least 10 now, 30 for growth; add catch-up headroom, e.g. 36 to 48.
- **EX02** shipmentId keeps per-shipment order; avoid carrierId which creates hot keys.
- **EX03** Warning: time-lag 2 min sustained; check handler latency and errors. Page: 10 min or rising; scale consumers, check downstream.
- **EX04** Cooperative assignor, static membership, longer session timeout, tune max poll interval.
- **EX05** Rate limit at the ingest API, bounded in-flight sends, pause consumer on DB slowness, shed or queue policy at the edge.
- **EX06** 5,000 KB/s x 604,800 s about 3 TB x 3 = about 9 TB; check compression and verify with real data.

**Workplace evidence:** a messaging scale problem you diagnosed or prevented.
