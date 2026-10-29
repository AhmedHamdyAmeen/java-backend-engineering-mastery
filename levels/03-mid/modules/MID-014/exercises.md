# MID-014 · MVCC — Exercises and lab

## Lab
### MID-014-LAB1 · Observe MVCC
**Outcomes:** 1–3 · **Time:** ~2 h
With two `psql` sessions, watch `xmin`/`xmax`/`ctid` change across `INSERT`, `UPDATE`, `DELETE`, and see what each session can see under `READ COMMITTED` and `REPEATABLE READ`. Then create bloat with an idle-in-transaction session and a hot update loop, measure it, and fix it.
**Acceptance:** annotated session transcript covering visibility, bloat creation, detection, and the fix.

## Exercises (assessment: quiz)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-014-EX01 | 1 | Explain in three sentences why a long read does not block a write. |
| MID-014-EX02 | 1 | Predict what session B sees in each of the two isolation levels after session A commits an update mid-transaction, then verify. |
| MID-014-EX03 | 2 | Update one row three times and show the `ctid` and `xmin` each time. |
| MID-014-EX04 | 2 | State what `VACUUM` does that `VACUUM FULL` does differently, and when each is appropriate. |
| MID-014-EX05 | 3 | Query `pg_stat_user_tables` to find the top three tables by dead tuples and their last autovacuum. |
| MID-014-EX06 | 3 | Find the oldest open transaction in `pg_stat_activity` and set `idle_in_transaction_session_timeout` for a role. |

## Solutions
- **EX01** Readers use a snapshot of old versions; writers create new versions; no row lock is needed to read.
- **EX02** `READ COMMITTED`: sees the new value on the next statement; `REPEATABLE READ`: keeps the old value until the transaction ends.
- **EX03** `ctid` changes with each update (new physical location); `xmin` is the updating transaction id.
- **EX04** `VACUUM` reclaims space for reuse without blocking reads/writes; `VACUUM FULL` rewrites the table to return space to the OS under an exclusive lock, so use it rarely and in a window.
- **EX05** `SELECT relname, n_dead_tup, last_autovacuum FROM pg_stat_user_tables ORDER BY n_dead_tup DESC LIMIT 3;`
- **EX06** `ORDER BY xact_start` on `pg_stat_activity`; `ALTER ROLE app SET idle_in_transaction_session_timeout = '30s';` (applies to new sessions).
- Disabling autovacuum and open transactions in application code are demonstrated in the lab and the lecture demo.
