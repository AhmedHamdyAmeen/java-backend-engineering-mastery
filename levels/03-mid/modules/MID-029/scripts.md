# MID-029 · Reliable messaging — Lecture scripts

**Video:** 80 min · **Analogy used throughout:** a shop's outgoing-mail tray: write the letter and log it in the same motion (outbox), and the receiving clerk keeps a stamped list of letters already handled (inbox).
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-029-L01 · The dual-write problem (10 min)
**Goal:** explain why writing to a database and a broker separately can lose or invent events.

**Key points**
- A **dual write** updates two systems (database, broker) with no shared transaction.
- Commit then publish: a crash between the two loses the event. The order exists, nobody hears about it.
- Publish then commit: a rollback or crash leaves an event for an order that does not exist.
- Publishing inside the DB transaction does not fix it: the broker call is not part of that transaction.
- Retrying makes it worse without idempotency: you may publish twice.

**Show**
```java
@Transactional
void place(Order o) {
    repo.save(o);
    kafka.send("order-placed", o.id(), event); // not atomic with the commit
}
```

**Check:** The service crashes after the commit but before `send`. What is lost? *(The `OrderPlaced` event; the order stays in the database.)*

---

## MID-029-L02 · Transactional outbox (14 min)
**Goal:** make "change state" and "record the event" one atomic step.

**Key points**
- Write the business row and an **outbox** row in the same local transaction. Either both exist or neither.
- A separate **relay** reads unsent outbox rows and publishes them, then marks them sent.
- Delivery becomes **at-least-once**: the relay may publish, crash, and publish again. Consumers must cope (L04).
- Keep the outbox row small: event id, aggregate id, type, JSON payload, created time, sent flag.
- Use the aggregate id as the Kafka key so one order's events stay ordered.

**Show**
```sql
CREATE TABLE outbox (
  id UUID PRIMARY KEY, aggregate_id BIGINT NOT NULL,
  type TEXT NOT NULL, payload JSONB NOT NULL,
  created_at TIMESTAMPTZ NOT NULL DEFAULT now(), sent_at TIMESTAMPTZ);
```
```java
@Transactional
void place(Order o) { repo.save(o); outbox.save(OutboxEvent.of("OrderPlaced", o)); }
```

**Check:** Why is the outbox write safe where `kafka.send` was not? *(It is in the same database transaction as the order.)*

---

## MID-029-L03 · Outbox relays: polling vs CDC (10 min)
**Goal:** choose how outbox rows reach the broker.

**Key points**
- **Polling relay:** a scheduled job selects unsent rows (`ORDER BY created_at`), publishes, marks them sent. Simple; adds latency and database load.
- With several relay instances, use `FOR UPDATE SKIP LOCKED` so they do not take the same rows.
- **CDC** (change data capture, for example Debezium) reads the database log and publishes row changes. Low latency, no polling, but more infrastructure.
- Both give at-least-once. Ordering per aggregate must be preserved.
- Delete or archive sent rows, or the table grows forever.

**Show**
```sql
SELECT * FROM outbox WHERE sent_at IS NULL
ORDER BY created_at LIMIT 100 FOR UPDATE SKIP LOCKED;
```

**Check:** What does `SKIP LOCKED` allow? *(Several relay instances to work on different rows at once.)*

---

## MID-029-L04 · Idempotent consumers and the inbox (12 min)
**Goal:** apply each event once in effect, even if delivered many times.

**Key points**
- Brokers redeliver after crashes, rebalances, and timeouts. Duplicates are normal.
- **Natural idempotency:** `SET status = 'PAID'` is safe to repeat; `balance = balance - 10` is not.
- **Inbox table:** store the processed message id with a unique constraint, in the same transaction as the effect.
- Insert the id first; a duplicate key means "already done", so skip.
- An in-memory set is not enough: it is lost on restart.

**Show**
```java
@Transactional
void on(StockReserve msg) {
    if (!inbox.tryInsert(msg.eventId())) return; // unique violation: duplicate
    stock.reserve(msg.sku(), msg.qty());
}
```

**Check:** Why must the inbox insert and the stock change share a transaction? *(Otherwise a crash between them either skips the work or repeats it.)*

---

## MID-029-L05 · Retries, backoff, and DLQs (10 min)
**Goal:** retry transient failures sensibly and park permanent ones.

**Key points**
- **Transient** failures (timeout, deadlock) deserve a retry; **permanent** ones (bad payload, rule violation) never succeed.
- Use exponential backoff with a maximum attempt count; blocking retries stall the partition, so use retry topics for long delays.
- After the limit, send the message to a **dead-letter queue (DLQ)** with the error and original headers.
- Alert on DLQ depth and provide a way to replay after the fix.
- Spring Kafka offers `DefaultErrorHandler` with backoff and a dead-letter recoverer (verify version before recording).

**Show**
```java
var handler = new DefaultErrorHandler(
    new DeadLetterPublishingRecoverer(template),
    new ExponentialBackOff(500, 2.0)); // add a max elapsed time or attempts
```

**Check:** Why should a malformed payload go straight to the DLQ? *(Retrying cannot fix it and only delays the messages behind it.)*

---

## MID-029-L06 · Demo: losing an event without an outbox (12 min)
**Goal:** reproduce the dual-write loss, then fix it. Prepares MID-029-LAB1.

**Steps**
1. Start `orders`, Kafka, and a consumer log; place an order and see the event arrive.
2. Add a `Thread.sleep` (or a kill hook) between `repo.save` and `kafka.send`.
3. Place an order and `kill -9` the service during the pause; restart and check: the order exists, no event ever arrives.
4. **Planned mistake:** "fix" it by moving `send` inside `@Transactional` and repeat the kill. The event is still lost (or sent for a rolled-back order). Fix: it is the same dual write.
5. Add the outbox table and relay; repeat the kill and watch the event arrive after restart.

---

## MID-029-L07 · Demo: processing the same message twice, safely (12 min)
**Goal:** show duplicate delivery and make `inventory` immune. Prepares MID-029-LAB1.

**Steps**
1. Publish one `OrderPlaced` event to `inventory`; stock drops by 2.
2. Replay the same record (reset the offset or resend); stock drops by 2 again. Show the bug.
3. Add an `inbox` table with the event id as primary key and insert it in the same transaction.
4. **Planned mistake:** keep processed ids in a `HashSet`. Restart the service, replay, and the duplicate is applied. Fix: durable inbox row.
5. Replay again: the unique violation is caught, stock is unchanged, and a log line says "duplicate skipped".
