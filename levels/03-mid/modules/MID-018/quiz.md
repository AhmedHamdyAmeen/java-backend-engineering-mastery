# MID-018 · Database operations — Quiz

Outcomes: O1 backups and restore · O2 WAL and PITR · O3 replication and lag · O4 monitoring.

**Q01 (O1)** `pg_dump` produces a: A. Physical copy of the data directory B. WAL segment C. Logical backup of one database D. Replica
**Q02 (O1)** The best proof that a backup works is: A. A successful restore drill B. Its file size C. The cron log D. The backup name
**Q03 (O1)** A physical backup can usually be restored to: A. Any PostgreSQL version B. The same major version C. MySQL D. A different OS only
**Q04 (O2)** PITR needs: A. Only a dump B. Vacuum C. A replica only D. A base backup plus archived WAL
**Q05 (O2)** WAL is: A. A log of changes written before data files B. A user table C. An index type D. A backup tool
**Q06 (O2)** To undo a bad `DELETE` at 14:05 you set the recovery target to: A. 14:06 B. 15:00 C. 14:04 D. Tomorrow
**Q07 (O3)** Asynchronous replication means the replica: A. Is always identical B. May lag behind the primary C. Cannot be queried D. Replaces backups
**Q08 (O3)** A replica protects against an accidental `DROP TABLE`: A. Always B. Sometimes C. Yes, if read-only D. No, the drop replicates
**Q09 (O3)** Reading your own write from a lagging replica may return: A. A syntax error B. A deadlock C. Stale data D. Faster data
**Q10 (O4)** Which is a key health indicator? A. Replication lag B. Number of columns C. Font size D. Comment count

## Answers
Q01 C · Q02 A · Q03 B · Q04 D · Q05 A · Q06 C · Q07 B · Q08 D · Q09 C · Q10 A

## Practical part
Runbook review: find the gaps in a restore runbook (untested, untimed, same-host backups, missing WAL archive check). Pass: quiz 8/10, all gaps named with fixes, and the lab runbook with a measured recovery time.
