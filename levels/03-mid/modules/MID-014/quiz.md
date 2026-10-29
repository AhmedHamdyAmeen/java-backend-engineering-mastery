# MID-014 · MVCC — Quiz

Outcomes: O1 MVCC and visibility · O2 row versions and vacuum · O3 bloat and long transactions.

**Q01 (O1)** In MVCC a reader: A. Locks the row B. Blocks all writers C. Reads a snapshot without blocking writers D. Must wait for commits
**Q02 (O1)** `xmin` on a row version is: A. The transaction that created it B. The row count C. The minimum value D. The table id
**Q03 (O1)** `REPEATABLE READ` takes its snapshot: A. Per statement B. Per transaction C. Per row D. Never
**Q04 (O2)** An `UPDATE` in PostgreSQL: A. Overwrites the row in place B. Locks the table C. Deletes the table D. Creates a new row version
**Q05 (O2)** Plain `VACUUM` mainly: A. Marks dead versions reusable B. Returns disk space to the OS C. Rebuilds all indexes with a lock D. Drops old rows of live data
**Q06 (O2)** Autovacuum should be: A. Disabled on busy tables B. Run only yearly C. Kept on and tuned D. Replaced by `TRUNCATE`
**Q07 (O3)** The most common cause of vacuum being unable to clean: A. Small tables B. A long-running or idle-in-transaction session C. Many indexes D. Using UUIDs
**Q08 (O3)** Where do you find idle transactions? A. `information_schema.tables` B. `pg_stats` C. `pg_class` only D. `pg_stat_activity`
**Q09 (O3)** A good safeguard for application mistakes: A. More replicas B. Bigger `work_mem` C. `idle_in_transaction_session_timeout` D. `fsync = off`
**Q10 (O3)** Dead tuples counted high and `last_autovacuum` very old suggest: A. Vacuum is blocked or misconfigured B. Healthy table C. Missing primary key D. Too few columns

## Answers
Q01 C · Q02 A · Q03 B · Q04 D · Q05 A · Q06 C · Q07 B · Q08 D · Q09 C · Q10 A

## Practical part
Quiz is the assessment, plus the annotated session transcript from `MID-014-LAB1` and exercises `MID-014-EX01` to `EX06`. Pass: quiz 8/10 and a transcript that shows visibility changes, bloat creation, and the fix.
