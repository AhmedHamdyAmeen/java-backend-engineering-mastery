# SRB-006 · Large-scale messaging — Lecture scripts

**Video:** 92 min · **Running case:** The FulfillCo integration (Shop Platform acquires FulfillCo, a 10-year-old Java modular monolith on one PostgreSQL database; four teams integrate in real time and extract capabilities without stopping either business).
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRB-006-L01 · Messaging at scale (8 min)
**Goal:** see what changes when message volume grows by 50 times.

**Key points**
- Small design choices (keys, partitions, batch size) become big cost and reliability factors.
- The broker is shared infrastructure: one noisy topic can hurt others.
- Scale problems show up as lag, rebalances, and recovery time, not only as throughput.
- Plan for catch-up speed, not just steady-state.

**Show:** a chart sketch of FulfillCo's partner feed: 50x Shop's order events, daily peaks, and the headroom needed for catch-up.

**Check:** Why plan for catch-up speed? *(After an outage consumers must process backlog plus new events.)*

---

## SRB-006-L02 · Partition strategy (12 min)
**Goal:** choose partition count and keys with growth and ordering in mind.

**Key points**
- Partitions are the unit of parallelism: a consumer group can have at most one active consumer per partition.
- The key decides ordering: events with the same key stay ordered in one partition.
- Changing partition count later breaks key-to-partition mapping; plan headroom.
- Beware hot keys; avoid keys that concentrate traffic.

**Show:** a sizing formula: partitions >= max(target throughput / per-partition throughput, target throughput / per-consumer throughput), with a growth factor; example for shipment events keyed by shipmentId.

**Check:** Why is changing partition count risky? *(Key-to-partition mapping changes and ordering per key can break.)*

---

## SRB-006-L03 · Consumer lag (10 min)
**Goal:** monitor lag and act with thresholds.

**Key points**
- Lag is how far a consumer group is behind the log head, in messages or time.
- Time lag matters more to users than message count.
- Alert on sustained growth and on age, with a runbook per alert.
- Lag has causes: slow handler, bad message, rebalance storm, downstream failure.

**Show:** an alert table: warning at 2 min time-lag for 10 min, page at 10 min or growing for 30 min; each with the first three actions.

**Check:** Why alert on time lag? *(It reflects delay as users see it, unlike raw counts.)*

---

## SRB-006-L04 · Rebalancing (10 min)
**Goal:** reduce the damage of consumer group rebalances.

**Key points**
- Rebalance moves partitions between consumers and may pause processing.
- Cooperative rebalancing moves only the partitions that must move.
- Static membership avoids rebalances on quick restarts.
- Tune session and poll timeouts; slow handlers cause false evictions. Verify client settings before recording.

**Show:** a timeline comparing eager rebalancing (all stop) with cooperative (only a few partitions pause) during a rolling deploy.

**Check:** What does static membership help with? *(Restarting consumers without triggering a rebalance.)*

---

## SRB-006-L05 · Backpressure end to end (12 min)
**Goal:** stop producers from overwhelming consumers.

**Key points**
- Backpressure is a signal flowing upstream: slow down.
- Queues hide overload until they are huge; bound them.
- Tools: fetch and poll limits, pause and resume, rate limits at the producer, and shedding at the edge.
- Decide what happens at full: block, drop, or degrade.

**Show:** a pipeline diagram: partner API -> ingest service -> topic -> consumer -> DB; a bound and a policy at each hop.

**Check:** What does an unbounded queue hide? *(Overload until memory or latency explodes.)*

---

## SRB-006-L06 · Cluster capacity and governance (10 min)
**Goal:** plan the cluster and keep many teams safe on it.

**Key points**
- Capacity: throughput, storage = rate x retention x replication, network, and partition count per broker.
- Retention is a cost lever; tie it to the use case.
- Governance: topic naming, owners, quotas, ACLs, and an approval path for new topics.
- Verify broker limits and versions before recording.

**Show:** a capacity worksheet: 5,000 msg/s x 1 KB x 7 days x 3 replicas = storage; plus a topic request template.

**Check:** What multiplies storage besides rate and retention? *(Replication factor.)*

---

## SRB-006-L07 · Demo: recovering from a six-hour consumer backlog (15 min)
**Goal:** drain a large backlog without breaking live traffic.

**Steps**
1. Show lag at six hours after a consumer bug.
2. Fix the bug, then scale consumers up to the partition count.
3. Check the downstream database as the new bottleneck; add batching.
4. **Planned mistake:** scale consumers beyond partitions and see no gain; fix by increasing parallelism inside the consumer or using more partitions in future design.
5. Track time-to-clear against the estimate and record lessons in the runbook.

Prepares SRB-006-LAB1.

---

## SRB-006-L08 · Demo: choosing partition counts for three years of growth (15 min)
**Goal:** turn growth forecasts into a partition count.

**Steps**
1. Forecast partner feed volume for three years with a growth factor.
2. Measure per-partition and per-consumer throughput from a test.
3. Compute partitions needed and add headroom for catch-up.
4. **Planned mistake:** size only for today's peak; fix by sizing for year three plus a catch-up factor.
5. Document the key choice, ordering guarantee, and the cost of over-partitioning.

Prepares SRB-006-LAB1.

---
