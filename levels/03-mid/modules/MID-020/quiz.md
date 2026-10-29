# MID-020 · Database migrations — Quiz

Outcomes: O1 expand-contract · O2 lock-safe DDL · O3 batched backfills · O4 rollback planning.

**Q01 (O1)** Safe way to rename a column with old and new app versions running: A. Add the new column, dual-write, backfill, switch, then drop the old B. Rename in one step C. Drop and recreate D. Restart the database
**Q02 (O1)** The contract step means: A. Adding the new column B. Backfilling C. Removing the old column after nothing uses it D. Adding an index
**Q03 (O1)** Why can the app and schema change not be deployed at the same instant? A. Caches B. SQL is slow C. Flyway forbids it D. Old and new app instances run together during a deploy
**Q04 (O2)** A waiting `ALTER TABLE` can cause an outage because it: A. Deletes data B. Blocks queries queued behind its lock request C. Uses disk D. Restarts connections
**Q05 (O2)** To create an index without blocking writes: A. `REINDEX` B. `CREATE INDEX` in a transaction C. `CREATE INDEX CONCURRENTLY` D. `VACUUM`
**Q06 (O2)** `ADD CONSTRAINT ... NOT VALID` followed by `VALIDATE CONSTRAINT` is used to: A. Reduce lock time on large tables B. Skip checking forever C. Rename columns D. Create partitions
**Q07 (O2)** `lock_timeout` makes a migration: A. Faster B. Skip locks C. Atomic D. Give up instead of queueing indefinitely
**Q08 (O3)** Backfill a huge table: A. In one `UPDATE` B. In small resumable batches C. During the app startup D. Only by dropping the table
**Q09 (O3)** A good backfill condition is: A. `WHERE new_col IS NULL` for idempotency B. None C. `LIMIT 0` D. `ORDER BY random()`
**Q10 (O4)** The point of no return in expand-contract is usually: A. Adding the column B. The backfill C. Dropping the old column D. The dual write

## Answers
Q01 A · Q02 C · Q03 D · Q04 B · Q05 C · Q06 A · Q07 D · Q08 B · Q09 A · Q10 C

## Practical part
Migration plan review: find the risky steps in a given plan and rewrite them as safe, reversible steps with rollbacks. Pass: quiz 8/10, all risky steps fixed, and the lab with zero failed requests.
