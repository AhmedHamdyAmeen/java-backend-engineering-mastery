# MID-027 · RabbitMQ — Quiz

Outcomes: O1 exchanges and bindings · O2 Spring AMQP and acks · O3 DLX and retry · O4 RabbitMQ vs Kafka.

**Q01 (O1)** Producers in RabbitMQ publish to: A. A queue directly B. A consumer C. An exchange D. A database
**Q02 (O1)** Which exchange copies a message to every bound queue? A. Direct B. Fanout C. Topic D. Default only
**Q03 (O1)** In a topic exchange `*` matches: A. Zero or more words B. Anything including dots and slashes C. Only numbers D. Exactly one word
**Q04 (O2)** With auto-ack, a consumer crash during processing: A. Redelivers the message B. Moves it to the DLQ C. Loses the message D. Blocks the queue
**Q05 (O2)** With manual acks, when should you ack? A. Before processing B. After successful processing C. On connection open D. Never
**Q06 (O2)** Prefetch limits: A. Message size B. Queue count C. Exchange count D. Unacknowledged messages per consumer
**Q07 (O3)** A message is dead-lettered when it: A. Is rejected without requeue B. Is acknowledged C. Is published D. Is routed to a topic
**Q08 (O3)** Delayed retry without a plugin is commonly built with: A. A TTL queue that dead-letters back to the main exchange B. A cron job deleting messages C. Auto-ack D. Fanout only
**Q09 (O3)** Infinite redelivery of a poison message is stopped by: A. Raising prefetch B. Requeue always on C. A retry limit and a DLQ D. Using auto-ack
**Q10 (O4)** Which need most favors Kafka over RabbitMQ? A. Replaying a long event history B. Per-message TTL C. Priority task queues D. Complex routing keys

## Answers
Q01 C · Q02 B · Q03 D · Q04 C · Q05 B · Q06 D · Q07 A · Q08 A · Q09 C · Q10 A

## Practical part
Five exercises `MID-027-EX01` to `EX05` plus the lab. Pass: at least four exercises correct and the lab's poison message landing in the DLQ while normal messages are still processed.
