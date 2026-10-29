# SRC-013 · Disaster recovery — Quiz

Outcomes: O1 RPO and RTO · O2 backup, replication, failover · O3 recovery exercises · O4 region or account loss.

**Q01 (O1)** RPO measures: A. How long you can be down B. The cost of backups C. How much data loss, in time, is acceptable D. Recovery team size
**Q02 (O1)** RTO measures: A. Acceptable downtime B. Data loss C. Backup size D. Network latency
**Q03 (O1)** RPO and RTO should be derived from: A. Business impact and cost B. Vendor defaults C. Database brand D. Team preference only
**Q04 (O2)** Why does replication not replace backups? A. It is slower B. It is unencrypted C. It copies mistakes such as dropped tables D. It only works for caches
**Q05 (O2)** Split brain means: A. Two nodes both acting as primary B. A cache miss C. A slow query D. A failed backup
**Q06 (O2)** Which topology has the lowest cost and the longest RTO? A. Active-active B. Warm standby C. Pilot light D. Backup and restore
**Q07 (O3)** A drill's RTO is measured from failure until: A. The database process starts B. Verified service is restored C. The report is written D. The alarm sounds
**Q08 (O3)** The most important output of a drill is: A. A celebration B. Measured results and tracked remediation C. A longer RTO D. A new tool
**Q09 (O2)** After Kafka loss, derived stores should be rebuilt from: A. Another cache B. Guesswork C. The latest consumer offset only D. The source of truth
**Q10 (O4)** Which must be prepared in advance for region loss? A. Replicated secrets, config, and a traffic switch path B. Only a faster laptop C. Nothing, improvise D. A larger log file

## Answers
Q01 C · Q02 A · Q03 A · Q04 C · Q05 A · Q06 D · Q07 B · Q08 B · Q09 D · Q10 A

## Practical part
Drill report review (SRC-013 assessment): critique a drill report and present `SRC-013-LAB1` results. Pass: at least 8/10 on the quiz, RPO and RTO measured with timestamps, and gaps with a remediation plan.
