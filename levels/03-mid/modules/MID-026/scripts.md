# MID-026 · Messaging fundamentals — Lecture scripts

**Video:** 58 min · **Analogy used throughout:** a post office and a newspaper subscription: a letter goes to one recipient; a newspaper goes to every subscriber.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-026-L01 · Why messaging (8 min)
**Goal:** state what a broker adds.

**Key points**
- A broker stores messages between a producer and a consumer.
- Benefits: temporal decoupling, load levelling (a queue absorbs spikes), easy fan-out, retry without the sender waiting.
- Costs: eventual consistency, duplicates, ordering questions, one more system to run.
- Shop use: after `OrderPlaced`, inventory, payments, and notifications each react without `orders` knowing them.
- Do not use messaging when the caller needs an immediate answer.

**Show:** `orders` publishes once; three consumers receive independently.

**Check:** Name two benefits of a broker. *(For example decoupling in time and absorbing load spikes.)*

---

## MID-026-L02 · Queues vs topics (10 min)
**Goal:** distinguish point-to-point from publish/subscribe.

**Key points**
- Queue (point-to-point): each message goes to one consumer among competing consumers. Good for work distribution.
- Topic (publish/subscribe): each message goes to every subscriber (or subscriber group). Good for events.
- Brokers differ: RabbitMQ routes through exchanges to queues; Kafka topics keep a log read by consumer groups (MID-027, MID-028).
- Competing consumers scale a queue's throughput.
- Each independent subscriber needs its own queue or group so it gets its own copy.

**Show:** a diagram with one queue and three workers, and one topic with three subscriber groups.

**Check:** Which model delivers a message to all subscribers? *(Topic, or publish/subscribe.)*

---

## MID-026-L03 · Commands vs events (8 min)
**Goal:** name messages correctly.

**Key points**
- A command asks for something to be done: `ReserveStock`. Imperative name, one intended receiver, can be rejected.
- An event states a fact that happened: `StockReserved`. Past tense, any number of listeners, cannot be rejected.
- The publisher of an event does not know or care who listens.
- A "command in disguise" like `OrderPlacedPleaseReserveStock` couples sender to receiver.
- Name events after business facts, not technical changes (`OrderPlaced`, not `OrdersRowInserted`).

**Show:** a table of five Shop messages classified as command or event.

**Check:** Is `PaymentAuthorized` a command or an event? *(An event; it is past tense.)*

---

## MID-026-L04 · Delivery semantics (12 min)
**Goal:** explain the three guarantees and the exactly-once limit.

**Key points**
- At-most-once: send and forget; messages may be lost, never duplicated.
- At-least-once: retry until acknowledged; no loss, but duplicates are possible. The usual default.
- Exactly-once delivery across systems is not achievable end to end, because an acknowledgment can be lost (MID-023).
- Effectively-once: at-least-once delivery plus idempotent processing (or deduplication), so repeats have no extra effect.
- Some platforms offer exactly-once processing within their own boundary (for example Kafka transactions); verify scope before relying on it.

**Show:** timeline: consumer processes, ack lost, broker redelivers, the consumer sees the message twice.

**Check:** How do you get effectively-once? *(At-least-once delivery plus idempotent handling.)*

---

## MID-026-L05 · Designing event payloads (10 min)
**Goal:** choose the content of an event.

**Key points**
- Include: `eventId` (unique, for deduplication), `type`, `occurredAt`, `version` (schema), the aggregate ID, and key business data.
- Minimal (notification) event: IDs only; consumers call back for details, which adds coupling and load.
- Full-state event: carries the data consumers need; larger, but consumers stay autonomous.
- A middle path: carry the facts that changed or that most consumers need, not entire database rows.
- Evolve schemas compatibly: add optional fields, never reuse or retype fields (schema registry, MID-029).

**Show**
```json
{ "eventId": "a1b2...", "type": "OrderPlaced", "version": 1,
  "occurredAt": "2026-03-01T10:15:30Z",
  "data": { "orderId": "o-42", "customerId": "c-7", "total": "59.90", "currency": "EUR" } }
```

**Check:** What is the `eventId` for? *(Uniquely identifying the event so consumers can detect duplicates.)*

---

## MID-026-L06 · Demo: one event, three consumers (10 min)
**Goal:** see fan-out and independence. Prepares `MID-026-LAB1`.

**Steps**
1. Define the `OrderPlaced` JSON schema with the fields from L05.
2. Publish it once to a topic (use any broker available in the lab setup).
3. Start three consumers: inventory, payments, notifications, each with its own subscription.
4. Stop one consumer, keep publishing, restart it, and show it catches up while the others were unaffected.
5. **Planned mistake:** publish `ReserveStockAndChargeCard` as an "event". Explain why it is a command in disguise and rename it `OrderPlaced`.
6. Add the event to the catalog with an owner.

---
