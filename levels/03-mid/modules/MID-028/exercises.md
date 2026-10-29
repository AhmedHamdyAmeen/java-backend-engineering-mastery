# MID-028 · Apache Kafka — Exercises and lab

## Lab
### MID-028-LAB1 · Order events on Kafka
**Outcomes:** 1–5 · **Time:** ~4 h
1. Create `orders` (3 partitions). `orders` publishes `OrderPlaced` keyed by order ID with `acks=all` and idempotence enabled.
2. `inventory` and `payments` consume in separate groups with a `DefaultErrorHandler`, back-off, and a DLT.
3. Make handlers idempotent by `eventId`.
4. Test: events of one order stay in order; restart a consumer mid-stream and confirm nothing is lost; send a poison record and find it in the DLT.
**Acceptance:** per-order ordering preserved; consumer restart loses nothing.

## Exercises (assessment: partitioning and ordering scenarios; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-028-EX01 | 1 | Draw a topic with 4 partitions and replication factor 3 over 3 brokers; mark leaders and followers. |
| MID-028-EX02 | 2 | Pick a key for: order events, per-customer notifications, sensor readings per device. Say what ordering you get. |
| MID-028-EX03 | 3 | A group has 3 consumers and a topic has 2 partitions. Describe the assignment and what happens when one consumer leaves. |
| MID-028-EX04 | 3 | Explain the failure when offsets are committed before processing and the failure when committed after. |
| MID-028-EX05 | 4 | Configure a Spring Kafka error handler that retries 3 times, 1 s apart, then publishes to a DLT. |
| MID-028-EX06 | 5 | Choose `acks`, `min.insync.replicas`, and idempotence for payment events and explain the trade-off. |

## Solutions
- **EX01** Each partition has one leader and two followers on different brokers; leaders spread across brokers.
- **EX02** Order events: `orderId` (per-order order). Notifications: `customerId`. Sensors: `deviceId`. No ordering across keys.
- **EX03** Two consumers get one partition each; one idles. If an active one leaves, rebalance gives its partition to the idle one.
- **EX04** Commit before: crash loses the record. Commit after: crash causes redelivery, so handlers must be idempotent.
- **EX05** `new DefaultErrorHandler(new DeadLetterPublishingRecoverer(template), new FixedBackOff(1000L, 3))`.
- **EX06** `acks=all`, replication factor 3, `min.insync.replicas=2`, `enable.idempotence=true`; cost is extra latency and reduced availability if two replicas are down.
