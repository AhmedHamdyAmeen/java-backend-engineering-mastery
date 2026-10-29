# ARC-015 · Storage architecture — Quiz

Outcomes: O1 storage types · O2 backups and immutability · O3 lifecycle and tiers · O4 securing stored data.

**Q01 (O1)** Which storage best serves millions of product images? A. Block B. File C. Object D. Tape on site
**Q02 (O1)** Block storage is mainly used for: A. Static website assets B. Database volumes and boot disks C. Email D. Public downloads
**Q03 (O1)** Shared folders for a legacy app are usually served by: A. File storage B. Object storage only C. Queues D. Caches
**Q04 (O2)** Replication alone is not a backup because: A. It is too slow B. It is too expensive C. It copies deletions and corruption too D. It needs no storage
**Q05 (O2)** Immutable backup storage helps against: A. Slow queries B. Attackers with admin credentials deleting backups C. DNS failure D. Rendering bugs
**Q06 (O2)** Backups should be kept in: A. The production account with the same admin B. A separate account with separate credentials C. The developer laptop D. The same bucket as logs
**Q07 (O3)** Lifecycle rules mainly: A. Move data to cheaper tiers or delete it by age B. Encrypt data C. Create backups D. Add public access
**Q08 (O3)** A caution about archive tiers is: A. They are unreliable B. They cannot be encrypted C. They have retrieval fees and minimum storage durations D. They have no retention
**Q09 (O4)** The safest default for storage public access is: A. Blocked B. Open for reads C. Open for writes D. Controlled by developers per file
**Q10 (O4)** Which is a sound practice for stored data? A. Shared long-lived keys B. Disable logging C. Skip classification D. Encrypt at rest and grant least-privilege roles

## Answers
Q01 C · Q02 B · Q03 A · Q04 C · Q05 B · Q06 B · Q07 A · Q08 C · Q09 A · Q10 D

## Practical part
Design review of the `ARC-015-LAB1` storage design plus exercises `ARC-015-EX01` to `EX06`. Pass: quiz at least 8/10, at least five of six exercises correct, retention matching requirements, and backups isolated from production credentials.
