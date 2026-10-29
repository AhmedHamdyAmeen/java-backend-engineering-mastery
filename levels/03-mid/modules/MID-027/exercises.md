# MID-027 · RabbitMQ — Exercises and lab

## Lab
### MID-027-LAB1 · Notifications
**Outcomes:** 1–4 · **Time:** ~2.5 h
1. Build a notification service with Spring AMQP, consuming `email` and `sms` queues bound to a topic exchange with routing keys.
2. Use manual acknowledgments and a prefetch limit.
3. Add a TTL retry queue (3 attempts) and a final dead-letter queue.
4. Send a poison message and normal messages together.
**Acceptance:** a poison message ends in the DLQ without blocking others.

## Exercises (assessment: lab plus tool-choice scenario; five exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-027-EX01 | 1 | Write the routing key patterns so one queue gets all `order.*` events and another only `order.cancelled`. |
| MID-027-EX02 | 1 | Name the exchange type for: exact routing, pattern routing, broadcast. |
| MID-027-EX03 | 2 | Convert an auto-ack listener to manual ack and explain the failure it removes. |
| MID-027-EX04 | 3 | Declare a queue with a dead-letter exchange and a 10-second delayed retry back to the main queue. |
| MID-027-EX05 | 4 | Scenario: a 20 TB event history must be replayable by new services; another need is delayed email jobs. Pick a broker for each. |

## Solutions
- **EX01** Bind `order.*` to the first queue and `order.cancelled` to the second (exact keys also match topic patterns).
- **EX02** Direct, topic, fanout.
- **EX03** Set manual acknowledge mode; `basicAck` after success, `basicNack(tag, false, false)` on failure. Removes loss of unprocessed messages on a crash.
- **EX04** `QueueBuilder.durable("main").deadLetterExchange("dlx")`; a retry queue with `x-message-ttl=10000` and `x-dead-letter-exchange` pointing to the main exchange.
- **EX05** Replayable history: Kafka. Delayed jobs: RabbitMQ with TTL and DLX (or plugin).
- Outcome 2 is also exercised by the lab (manual acks, prefetch).
