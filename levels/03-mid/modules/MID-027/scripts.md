# MID-027 · RabbitMQ — Lecture scripts

**Video:** 60 min · **Analogy used throughout:** a sorting office: letters arrive at a counter (exchange), are sorted by address rules (bindings) into mailboxes (queues) and picked up by carriers (consumers).
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-027-L01 · RabbitMQ's model (10 min)
**Goal:** describe the parts and the message path.

**Key points**
- Producers publish to an exchange, never directly to a queue.
- The exchange routes messages to queues by bindings and routing keys.
- Queues store messages until consumers acknowledge them.
- Consumers read from queues; the broker pushes messages with a prefetch limit.
- Messages are deleted after acknowledgment; the broker is smart, consumers are simple.
- Protocol: AMQP 0-9-1; run locally with Docker and the management UI.

**Show:** producer → exchange → (binding) → queue → consumer.

**Check:** Does a producer publish to a queue or to an exchange? *(To an exchange.)*

---

## MID-027-L02 · Exchanges and routing (10 min)
**Goal:** pick the right exchange type.

**Key points**
- Direct: routes on an exact routing key match.
- Topic: routes by patterns: `*` matches one word, `#` matches zero or more. Example `order.*.created`.
- Fanout: copies to every bound queue; ignores the key.
- Headers exchanges also exist but are rare.
- Unroutable messages are dropped unless configured otherwise (mandatory flag or alternate exchange).
- Declare exchanges, queues, and bindings in code with Spring AMQP beans.

**Show**
```java
@Bean TopicExchange notifications() { return new TopicExchange("notifications"); }
@Bean Queue emailQueue() { return QueueBuilder.durable("email").build(); }
@Bean Binding b(Queue emailQueue, TopicExchange notifications) {
  return BindingBuilder.bind(emailQueue).to(notifications).with("order.#");
}
```

**Check:** Which exchange type ignores the routing key? *(Fanout.)*

---

## MID-027-L03 · Acknowledgments and prefetch (10 min)
**Goal:** avoid message loss with manual acks.

**Key points**
- Auto-ack removes the message on delivery; a crash during processing loses it.
- Manual ack: acknowledge after the work succeeds; `nack` or `reject` with or without requeue on failure.
- Unacknowledged messages return to the queue if the consumer dies.
- Prefetch (QoS) limits unacknowledged messages per consumer; it balances load and memory.
- Requeue loops forever on a poison message unless you route it to a dead-letter queue.
- Make handlers idempotent; redelivery is normal.

**Show**
```java
@RabbitListener(queues = "email")
void handle(Message m, Channel ch, @Header(AmqpHeaders.DELIVERY_TAG) long tag) throws IOException {
    try { process(m); ch.basicAck(tag, false); }
    catch (Exception e) { ch.basicNack(tag, false, false); } // no requeue: dead-letter
}
```
Set acknowledge mode `manual` and `prefetch` in the listener configuration (verify property names for the Spring Boot version before recording).

**Check:** Why is auto-ack risky? *(The message is removed before the work completes, so a crash loses it.)*

---

## MID-027-L04 · Dead-letter queues and delayed retry (10 min)
**Goal:** isolate poison messages and retry with a delay.

**Key points**
- A dead-letter exchange (DLX) receives messages that are rejected without requeue, expire (TTL), or overflow a queue.
- Set `x-dead-letter-exchange` (and optionally `x-dead-letter-routing-key`) as queue arguments.
- Delayed retry pattern: failed message goes to a wait queue with a TTL whose dead-letter target is the main exchange; it returns after the delay.
- Count retries (header `x-death` or your own) and park the message in a final DLQ after N attempts.
- A delayed-message plugin exists; verify availability and support status before recording.
- Alert on DLQ depth and make replay a deliberate action.

**Show:** main queue → reject → retry queue (TTL 10 s) → back to main; after 3 tries → DLQ.

**Check:** What stops an infinite redelivery loop? *(A retry limit and a dead-letter queue.)*

---

## MID-027-L05 · RabbitMQ or Kafka? (8 min)
**Goal:** choose a tool for a workload.

**Key points**
- RabbitMQ: flexible routing, task queues, per-message acks and TTLs, low latency, delete-after-consume. Good for commands and work distribution.
- Kafka: durable replayable log, high throughput, ordering per partition, many independent consumer groups. Good for event streams and event sourcing.
- Replay and long retention favor Kafka; complex routing and delayed jobs favor RabbitMQ.
- Operating cost and team skill matter.
- Using both is acceptable when each has a clear job.

**Show:** a decision table of eight workloads and the preferred broker.

**Check:** Which broker lets a new consumer replay old events? *(Kafka.)*

---

## MID-027-L06 · Demo: notification routing with a topic exchange (12 min)
**Goal:** build the notification flow. Prepares `MID-027-LAB1`.

**Steps**
1. Start RabbitMQ with Docker; open the management UI.
2. Declare topic exchange `notifications` and queues `email` (`notify.email.#`) and `sms` (`notify.sms.#`).
3. Publish `notify.email.order` and `notify.sms.shipped` from Shop; watch each queue receive its message.
4. Add a DLX and a poison message that throws; with auto requeue enabled, show the endless loop.
5. **Planned mistake:** leave requeue on. Fix with `nack` without requeue, route to the DLQ, and show later messages still flow.
6. Add a TTL retry queue and show a message returning after the delay.

---
