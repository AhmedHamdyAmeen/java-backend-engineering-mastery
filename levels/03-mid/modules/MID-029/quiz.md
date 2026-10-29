# MID-029 · Reliable messaging — Quiz

Outcomes: O1 dual write · O2 transactional outbox · O3 idempotent consumers · O4 retries and DLQ.

**Q01 (O1)** A service commits an order, then crashes before publishing. The result is: A. A duplicate event B. A lost event C. A rolled-back order D. A poison message
**Q02 (O1)** Why does publishing inside the DB transaction not solve dual write? A. Kafka is slower B. The broker is not part of that transaction C. Transactions forbid network calls D. It always duplicates events
**Q03 (O2)** In the outbox pattern the event row is written: A. After the commit B. To the broker first C. In the same transaction as the business change D. By the consumer
**Q04 (O2)** The delivery guarantee of an outbox relay is normally: A. At-least-once B. Exactly-once C. At-most-once D. None
**Q05 (O2)** `FOR UPDATE SKIP LOCKED` helps a polling relay by: A. Encrypting rows B. Letting several relays take different rows C. Deleting old rows D. Ordering by key
**Q06 (O2)** A benefit of CDC over polling: A. No infrastructure needed B. Lower latency without polling queries C. Removes need for idempotency D. Works without a database log
**Q07 (O3)** Which operation is naturally idempotent? A. `stock = stock - 2` B. Appending a log line C. `status = 'PAID'` D. Sending an email
**Q08 (O3)** Where should processed message ids be stored? A. In a `HashSet` B. In a durable table, in the same transaction as the effect C. In a log file only D. In the broker header
**Q09 (O4)** A malformed payload should: A. Be retried 10 times B. Block the partition C. Go to the DLQ without long retries D. Be ignored silently
**Q10 (O4)** Exponential backoff means: A. Retry immediately forever B. Waits that grow between attempts, with a limit C. Retry only once D. Random delivery order

## Answers
Q01 B · Q02 B · Q03 C · Q04 A · Q05 B · Q06 B · Q07 C · Q08 B · Q09 C · Q10 B

## Practical part
Seven exercises `MID-029-EX01` to `EX07` plus the failure-injection review and `MID-029-LAB1`. Pass: at least six exercises and a chaos run with no lost and no double-applied events.
