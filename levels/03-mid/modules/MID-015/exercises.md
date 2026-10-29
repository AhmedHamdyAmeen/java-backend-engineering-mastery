# MID-015 · Isolation and locking — Exercises and lab

## Lab
### MID-015-LAB1 · Last item in stock
**Outcomes:** 1–4 · **Time:** ~3 h
Reproduce overselling in Shop: 50 threads each try to buy the last 10 units. Fix it three ways: (1) atomic `UPDATE ... WHERE qty >= n`, (2) `SELECT ... FOR UPDATE`, (3) `SERIALIZABLE` with a bounded retry. Compare throughput and error rate.
**Acceptance:** a concurrent test never oversells for all three fixes; a short comparison table of throughput.

## Exercises (assessment: anomaly-identification scenarios)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-015-EX01 | 1 | For five short timelines, name the anomaly. |
| MID-015-EX02 | 1 | Fill a table: which anomalies each PostgreSQL level allows. |
| MID-015-EX03 | 2 | Write a transaction that reserves one unit using `FOR UPDATE`; explain what a concurrent session experiences. |
| MID-015-EX04 | 2 | Implement a job claim query with `SKIP LOCKED` and run two workers. |
| MID-015-EX05 | 3 | Create a deadlock with two sessions, read the log message, and fix it with ordering. |
| MID-015-EX06 | 3 | Find a blocked session and its blocker using `pg_locks` / `pg_stat_activity` (or `pg_blocking_pids`). |
| MID-015-EX07 | 4 | Write a retry wrapper (max 3 attempts, backoff) for SQLSTATE `40001` and `40P01`. |

## Solutions
- **EX01** For example: stale re-read = non-repeatable; new rows in a repeated query = phantom; both write from the same read = lost update; two writers on different rows breaking a shared rule = write skew; seeing uncommitted data = dirty read.
- **EX02** `READ COMMITTED` allows all but dirty; `REPEATABLE READ` allows only write skew; `SERIALIZABLE` allows none.
- **EX03** `SELECT ... FOR UPDATE; UPDATE ...; COMMIT`; the other session blocks on its write or lock until commit.
- **EX04** `... FOR UPDATE SKIP LOCKED LIMIT 1` inside a CTE with `UPDATE ... RETURNING`; the workers get different jobs.
- **EX05** Two sessions update rows A,B and B,A; the log shows "deadlock detected"; both update in ascending id order.
- **EX06** `SELECT pid, pg_blocking_pids(pid), query FROM pg_stat_activity WHERE cardinality(pg_blocking_pids(pid)) > 0;`
- **EX07** Loop up to 3 times catching those SQLSTATEs, rerun the whole transaction, sleep with jitter, rethrow at the end.
- The "retrying without limits" mistake is covered by EX07 and lab fix 3.
