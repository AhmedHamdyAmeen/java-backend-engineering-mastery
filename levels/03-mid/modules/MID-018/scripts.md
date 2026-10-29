# MID-018 · Database operations — Lecture scripts

**Video:** 62 min · **Running project:** Shop Platform (production-like PostgreSQL for Shop)
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-018-L01 · Backups: logical vs physical (10 min)
**Goal:** choose the right backup type.

**Key points**
- Logical backup (`pg_dump`, `pg_dumpall`): SQL or archive of data and schema; portable across versions; slow to restore on big databases; consistent snapshot of one database.
- Physical backup (`pg_basebackup`, file-level): a copy of the data directory; fast restore; same major version only; the basis for point-in-time recovery.
- A backup is useful only if restored; schedule and monitor both.
- Store backups off the database host; encrypt them.

**Show**
```bash
pg_dump -Fc -f shop.dump shop
pg_basebackup -D /backup/base -Fp -X stream
```

**Check:** Which backup type allows point-in-time recovery? *(Physical backup plus archived WAL.)*

---

## MID-018-L02 · Restore drills (8 min)
**Goal:** prove backups work by restoring them regularly.

**Key points**
- Restore a custom-format dump with `pg_restore -d newdb`; use `--jobs` for parallelism.
- Restore into a separate database or host, never over production first.
- Check the result: row counts, application smoke test, and elapsed time (your real recovery time).
- Automate the drill and alert on failure.
- Record the steps in a runbook.

**Show**
```bash
createdb shop_restore
pg_restore -d shop_restore --jobs 4 shop.dump
psql shop_restore -c "SELECT count(*) FROM orders;"
```

**Check:** What number does a restore drill give you that a backup job does not? *(The real recovery time, and proof the backup is usable.)*

---

## MID-018-L03 · WAL and point-in-time recovery (12 min)
**Goal:** explain how WAL enables recovery to any moment.

**Key points**
- WAL (write-ahead log): every change is written to the log before the data files; used for crash recovery and replication.
- WAL archiving copies finished WAL segments to safe storage (`archive_mode`, `archive_command`).
- PITR: restore a base backup, then replay archived WAL up to a target time (`recovery_target_time`).
- Recovery time depends on the base backup age and the WAL volume since.
- Settings and signal files changed over versions (`recovery.signal` since PostgreSQL 12); verify version before recording.

**Show:** a timeline: base backup at 02:00, WAL archived continuously, bad `DELETE` at 14:05, recover to 14:00.

**Check:** What two things do you need for PITR? *(A base backup and the archived WAL after it.)*

---

## MID-018-L04 · Replication and read replicas (12 min)
**Goal:** understand streaming replication and its lag.

**Key points**
- Streaming replication ships WAL from the primary to standbys, which replay it continuously.
- Standbys can serve read-only queries (read replicas) and can be promoted on failure.
- Asynchronous replication can lag; synchronous replication waits for the standby but adds write latency.
- Reading your own write from a lagging replica returns stale data; route such reads to the primary or wait for the LSN.
- Replication is not a backup: a bad `DELETE` replicates too.

**Show**
```sql
-- on primary
SELECT client_addr, state, replay_lag FROM pg_stat_replication;
```

**Check:** Does a replica protect against an accidental `DROP TABLE`? *(No; the change replicates.)*

---

## MID-018-L05 · What to monitor (8 min)
**Goal:** know the key database health indicators.

**Key points**
- Connections: used vs `max_connections`; idle in transaction count.
- Locks and long-running queries (`pg_stat_activity`, `pg_locks`).
- Cache hit ratio from `pg_stat_database` (blks_hit vs blks_read); low means too little memory or bad queries.
- Replication lag (bytes and seconds) and archive success.
- Disk free space and WAL directory growth; dead tuples and autovacuum activity.

**Show:** a dashboard sketch with six panels and an alert threshold for each; mention `postgres_exporter` with Prometheus (verify choice before recording).

**Check:** Which indicator warns you that WAL is piling up before the disk fills? *(Disk or WAL directory growth, often from a stuck archive or lagging replica slot.)*

---

## MID-018-L06 · Demo: restoring to five minutes before a bad `DELETE` (12 min)
**Goal:** perform a PITR end to end.

**Steps**
1. Enable WAL archiving and take a base backup; write down the time.
2. Run workload, note a safe timestamp, then run `DELETE FROM orders` without a `WHERE` clause.
3. Stop the server and move the damaged data directory aside; restore the base backup.
4. Set `recovery_target_time` to five minutes before the delete, create `recovery.signal`, and start.
5. **Planned mistake:** target a time after the delete; the rows are gone again. Fix: choose an earlier target and repeat.
6. Verify row counts, promote, and record the elapsed recovery time.

Prepares MID-018-LAB1.

**Check:** Why recover to a time before the delete rather than after? *(Replay stops at the target, so the delete is never applied.)*
