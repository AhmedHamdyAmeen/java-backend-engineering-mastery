# MID-015 · Isolation and locking — Quiz

Outcomes: O1 anomalies and isolation levels · O2 row locks · O3 diagnosing locks and deadlocks · O4 retries.

**Q01 (O1)** Two transactions read stock 5 and each write 4. This is a: A. Dirty read B. Phantom C. Deadlock D. Lost update
**Q02 (O1)** PostgreSQL's default isolation level is: A. `READ UNCOMMITTED` B. `READ COMMITTED` C. `REPEATABLE READ` D. `SERIALIZABLE`
**Q03 (O1)** Which level prevents write skew in PostgreSQL? A. `READ COMMITTED` B. `REPEATABLE READ` C. `SERIALIZABLE` D. None
**Q04 (O1)** Does `READ COMMITTED` prevent a lost update in read-then-write application code? A. No B. Yes C. Only with indexes D. Only with `LIMIT`
**Q05 (O2)** `SELECT ... FOR UPDATE` makes a concurrent `FOR UPDATE` on the same row: A. Fail silently B. Wait C. Skip it D. Read dirty data
**Q06 (O2)** `SKIP LOCKED` is ideal for: A. Reports B. Backups C. Schema changes D. Multi-worker job queues
**Q07 (O2)** The simplest oversell-safe stock decrement: A. Read in Java then write B. Cache the stock C. `UPDATE ... SET qty = qty - 1 WHERE qty > 0` D. Sleep and retry
**Q08 (O3)** PostgreSQL resolves a deadlock by: A. Aborting one of the transactions B. Waiting forever C. Restarting the server D. Ignoring it
**Q09 (O3)** Best way to prevent most deadlocks: A. Disable locks B. Larger pool C. Longer transactions D. Lock rows in a consistent order
**Q10 (O4)** A serialization failure (`40001`) should be handled by: A. Ignoring it B. Retrying the whole transaction a limited number of times C. Retrying forever D. Catching and continuing mid-transaction

## Answers
Q01 D · Q02 B · Q03 C · Q04 A · Q05 B · Q06 D · Q07 C · Q08 A · Q09 D · Q10 B

## Practical part
Anomaly-identification scenarios (five timelines to classify and fix) plus exercises `MID-015-EX01` to `EX07` and the lab. Pass: quiz 8/10, four of five scenarios correct, and the lab concurrency test never overselling.
