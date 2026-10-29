# ARC-016 · Database architecture — Quiz

Outcomes: O1 select stores · O2 replication and failover · O3 backup, PITR, DR · O4 migration.

**Q01 (O1)** With a managed relational database, the customer still owns: A. Hardware B. Engine patching C. Hypervisor D. Schema, indexes, and access
**Q02 (O1)** Which is a source of truth? A. The relational order store B. A cache C. A search index built from it D. A CDN
**Q03 (O1)** One database for every workload is: A. Always best B. A common mistake C. Required D. Cheaper without exception
**Q04 (O2)** A multi-AZ synchronous standby mainly provides: A. Read scaling B. Cheaper storage C. Automatic failover within the region D. Cross-region DR
**Q05 (O2)** Read replicas may: A. Lag behind the primary B. Never be stale C. Replace backups D. Remove the need for failover
**Q06 (O2)** After failover, applications should: A. Crash B. Assume no errors C. Keep old connections forever D. Reconnect and handle brief errors
**Q07 (O3)** PITR lets you: A. Restore to a moment before a mistake B. Scale reads C. Avoid backups D. Encrypt data
**Q08 (O3)** RPO describes: A. How long you can be down B. How much data you can lose C. The cost D. The region
**Q09 (O4)** Replication-based migration is chosen mainly for: A. Larger downtime B. Minimal downtime during cutover C. Skipping validation D. Avoiding rehearsal
**Q10 (O4)** Before cutover you should have: A. No rollback plan B. Only a plan for success C. A rehearsed migration and a rollback path D. A single attempt in production

## Answers
Q01 D · Q02 A · Q03 B · Q04 C · Q05 A · Q06 D · Q07 A · Q08 B · Q09 B · Q10 C

## Practical part
Design review of the `ARC-016-LAB1` data platform plus exercises `ARC-016-EX01` to `EX06`. Pass: quiz at least 8/10, at least five of six exercises correct, and each store's RPO/RTO either meeting requirements or flagged as a gap.
