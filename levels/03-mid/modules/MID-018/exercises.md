# MID-018 · Database operations — Exercises and lab

## Lab
### MID-018-LAB1 · Restore drill
**Outcomes:** 1–4 · **Time:** ~3 h
Back up Shop's database (logical and physical with WAL archiving), simulate data loss with a bad `DELETE`, restore with PITR to before the loss, and time every step. Set up a standby or read replica if your environment allows, and observe replication lag.
**Acceptance:** a runbook plus a measured recovery time.

## Exercises (assessment: runbook review)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-018-EX01 | 1 | Take a `pg_dump` in custom format and restore it into a new database with parallel jobs. |
| MID-018-EX02 | 1 | Compare logical and physical backups for a 2 TB database: size, restore time, portability. |
| MID-018-EX03 | 2 | List the settings and files needed to enable WAL archiving and recover to a point in time. |
| MID-018-EX04 | 2 | Given a base backup at 02:00 and a bad change at 14:05, give the recovery target and expected steps. |
| MID-018-EX05 | 3 | Explain why a read replica can return stale data after a write and propose two handling options. |
| MID-018-EX06 | 4 | Write a monitoring checklist of six indicators with a warning threshold for each. |
| MID-018-EX07 | 4 | Review a short runbook with three flaws (never tested, no timing, backups on the same disk) and correct it. |

## Solutions
- **EX01** `pg_dump -Fc -f shop.dump shop`; `createdb shop2; pg_restore -d shop2 -j 4 shop.dump`.
- **EX02** Logical: smaller to store maybe, slow restore (rebuilds indexes), portable across versions. Physical: fast, same major version, enables PITR.
- **EX03** `wal_level` suitable for archiving, `archive_mode = on`, `archive_command` (or library), a base backup; on restore `restore_command`, `recovery_target_time`, and `recovery.signal` (verify version).
- **EX04** Restore the 02:00 base backup, replay WAL to a target a little before 14:05 (for example 14:04), then promote.
- **EX05** Replication is asynchronous so the replica has not yet replayed the write. Options: read your own writes from the primary, or route by session or wait until the replica reaches the write's LSN.
- **EX06** For example: connections over 80%, replication lag over 30 s, disk over 80%, cache hit ratio under 99% for OLTP, idle-in-transaction over 1 minute, failed archive command. Thresholds are examples.
- **EX07** Add a scheduled restore test, record the measured time, copy backups to separate storage, and name an owner.
- "Backups never restored" is addressed by EX01, EX07, and the lab.
