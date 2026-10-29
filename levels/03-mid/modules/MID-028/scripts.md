# MID-028 · Apache Kafka — Lecture scripts

**Video:** 100 min · **Analogy used throughout:** an append-only ledger split into several notebooks (partitions); each reader keeps a bookmark (offset).
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-028-L01 · Kafka as a distributed log (10 min)
**Goal:** explain Kafka's model.

**Key points**
- Kafka stores records in an append-only, ordered log; consumers read by position and do not delete records.
- Records stay for a retention period (time or size), so many consumers can read and replay.
- A cluster has brokers; producers write, consumers read.
- Modern Kafka runs without ZooKeeper (KRaft mode); verify version before recording.
- Log reads are sequential, which is why throughput is high.

**Show:** a log with offsets 0..7, producer appending at the end, two consumers at offsets 3 and 7.

**Check:** Does Kafka delete a record when it is consumed? *(No; retention controls deletion.)*

---

## MID-028-L02 · Topics, partitions, replicas (12 min)
**Goal:** describe how data is spread and protected.

**Key points**
- A topic is split into partitions; each partition is an ordered log.
- Ordering is guaranteed only within a partition, not across the topic.
- Partitions give parallelism: at most one consumer per partition in a group.
- Each partition has replicas on other brokers: one leader serves reads and writes, followers copy.
- In-sync replicas (ISR) and `min.insync.replicas` decide when a write counts as durable.
- Partition count can be increased later but changes key-to-partition mapping; plan it.

**Show:** a topic `orders` with 3 partitions and replication factor 3 across 3 brokers.

**Check:** Where is order guaranteed? *(Within a single partition.)*

---

## MID-028-L03 · Keys and ordering (10 min)
**Goal:** choose a key that keeps the ordering that matters.

**Key points**
- The producer picks the partition from the key hash; the same key always goes to the same partition (while partition count is unchanged).
- Key by the entity whose events must stay in order: `orderId` for order events.
- A null key spreads records across partitions; no ordering between them.
- A hot key (one huge customer) overloads one partition.
- Ordering across different keys is not guaranteed and rarely needed.

**Show:** `OrderPlaced(o-42)`, `OrderPaid(o-42)`, `OrderShipped(o-42)` all land in partition 1 in order.

**Check:** What key keeps all events of one order together? *(The order ID.)*

---

## MID-028-L04 · Consumer groups and offsets (12 min)
**Goal:** explain how consumers share work and track position.

**Key points**
- A consumer group shares a topic's partitions; each partition goes to one member. Different groups each get all records.
- Offsets record the group's progress per partition, stored in the internal `__consumer_offsets` topic.
- Commit after processing for at-least-once; commit before processing risks loss.
- Rebalancing reassigns partitions when members join, leave, or time out; processing pauses briefly.
- More consumers than partitions leaves some idle.
- Tune `max.poll.interval.ms` so slow processing does not trigger rebalances.

**Show:** group `inventory` with 2 consumers over 3 partitions, plus group `payments` reading the same topic.

**Check:** What happens if a group has more consumers than partitions? *(Extra consumers stay idle.)*

---

## MID-028-L05 · Spring for Apache Kafka (12 min)
**Goal:** produce and consume from Spring.

**Key points**
- `KafkaTemplate` sends records; `@KafkaListener` consumes.
- Configure serializers (String, JSON) and the consumer `group-id` in `application.yml`.
- Set the listener ack mode (default commits after the batch is processed; `MANUAL` for control).
- Use a JSON serializer with a trusted-packages setting, or a schema registry (MID-029).
- `auto.offset.reset` decides where a new group starts (`earliest` or `latest`).
- Check configuration names against the Spring Boot version before recording.

**Show**
```java
kafka.send("orders", order.id(), new OrderPlaced(order.id(), order.total()));

@KafkaListener(topics = "orders", groupId = "inventory")
void on(OrderPlaced e) { reserve(e); }
```

**Check:** Which property gives each service its own copy of all events? *(A distinct `group-id`.)*

---

## MID-028-L06 · Error handling and dead-letter topics (10 min)
**Goal:** keep a poison record from blocking a partition.

**Key points**
- An exception in a listener hits the error handler; the default `DefaultErrorHandler` retries with a back-off, then skips (logs).
- Configure `DeadLetterPublishingRecoverer` to send failed records to `<topic>.DLT`.
- Classify errors: retry transient ones (timeouts), send non-retryable ones (bad payload) straight to the DLT.
- Non-blocking retry topics are available through `@RetryableTopic` (verify support for your version).
- Monitor DLT size and keep the failure headers for diagnosis.

**Show**
```java
@Bean DefaultErrorHandler errors(KafkaTemplate<Object,Object> t) {
  return new DefaultErrorHandler(new DeadLetterPublishingRecoverer(t), new FixedBackOff(1000L, 3));
}
```

**Check:** Where does a record go after retries are exhausted? *(To the dead-letter topic.)*

---

## MID-028-L07 · Producer durability settings (8 min)
**Goal:** choose settings that avoid loss and duplicates.

**Key points**
- `acks=0` no wait; `acks=1` leader only; `acks=all` all in-sync replicas. Use `all` for important data.
- With `acks=all` and replication factor 3, set `min.insync.replicas=2` so a write needs two copies.
- `enable.idempotence=true` prevents duplicates from producer retries within a partition; it is the default in recent client versions (verify).
- Retries and `delivery.timeout.ms` bound how long the producer keeps trying.
- Durability trades latency for safety.

**Show:** a table: setting, effect, trade-off.

**Check:** Which `acks` waits for all in-sync replicas? *(`acks=all`.)*

---

## MID-028-L08 · Demo: order events end to end (14 min)
**Goal:** run the full flow. Prepares `MID-028-LAB1`.

**Steps**
1. Start Kafka (KRaft) with Docker Compose; create `orders` with 3 partitions.
2. `orders` publishes `OrderPlaced` keyed by order ID with `acks=all` and idempotence on.
3. Consume in groups `inventory` and `payments`; show each gets every record.
4. Check ordering: send three events for one order and see the same partition and order.
5. **Planned mistake:** publish with a null key and show events of one order in different partitions and out of order. Fix with the order ID key.
6. Throw on a bad payload and show it arriving in `orders.DLT`.

---

## MID-028-L09 · Demo: what a rebalance does to in-flight messages (12 min)
**Goal:** observe duplicate delivery on rebalance. Prepares `MID-028-LAB1`.

**Steps**
1. Start two `inventory` consumers; note partition assignments.
2. Make the handler slow (5 s) and record each processed `eventId`.
3. Kill one consumer mid-processing; watch partitions reassign.
4. The surviving consumer re-reads from the last committed offset; show a message processed twice.
5. **Planned mistake:** enable auto-commit before processing and show a message lost on a crash. Fix by committing after processing.
6. Add an idempotency check on `eventId` and replay; the duplicate no longer has an effect.

---
