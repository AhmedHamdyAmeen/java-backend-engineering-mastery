# SRB-004 · Multi-region systems — Quiz

Outcomes: O1 comparison · O2 routing and failover · O3 residency · O4 selective multi-region.

**Q01 (O1)** RPO measures: A. Acceptable data loss B. Downtime C. Latency D. Cost
**Q02 (O1)** RTO measures: A. Data loss B. Throughput C. Acceptable time to recover D. Error rate
**Q03 (O1)** Active-passive typically has: A. No failover steps B. RPO above zero due to async replication C. Conflicting writes D. Zero cost
**Q04 (O2)** Active-active's main added concern is: A. No health checks B. Lack of DNS C. Single leader D. Write conflicts across regions
**Q05 (O2)** DNS failover is limited by: A. CPU B. Disk C. Resolver caching D. Kafka lag
**Q06 (O2)** A health check should: A. Test critical dependencies B. Only check the process id C. Never fail D. Run once a day
**Q07 (O3)** Residency violations often arise from: A. Using HTTPS B. Using Java C. Using Git D. Logs and backups copied abroad
**Q08 (O3)** Residency is best enforced: A. By policy documents only B. By design with region-scoped stores C. By trust D. By monitoring only after leaks
**Q09 (O4)** Selective multi-region means: A. All components are active-active B. No component is C. Only needed components are made multi-region D. Only databases
**Q10 (O4)** A common hidden dependency is: A. A local logger B. The JVM C. A unit test D. Identity or secrets in one region

## Answers
Q01 A · Q02 C · Q03 B · Q04 D · Q05 C · Q06 A · Q07 D · Q08 B · Q09 C · Q10 D

## Practical part
Topology review: defend your EU design to reviewers. Pass: 70% on the quiz and a topology with enforced residency, tiering, and a cost estimate.
