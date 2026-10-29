# MID-044 · Data selection — Quiz

Outcomes: O1 characterize a workload · O2 select and justify · O3 operational cost.

**Q01 (O1)** Which is NOT part of workload characterization? A. Access patterns B. Volume C. Database logo popularity D. Consistency needs
**Q02 (O1)** Evidence for a workload should come from: A. Measurements such as logs and metrics B. Blog posts only C. Guesses D. The newest tool
**Q03 (O1)** "Query flexibility" asks: A. How many unknown future queries are likely B. How fast the CPU is C. The key length D. The number of replicas
**Q04 (O2)** A sensible default store for orders is: A. PostgreSQL B. A cache only C. A graph database D. A search index
**Q05 (O2)** An ADR must include: A. Only the decision B. Context, options, consequences, and a revisit trigger C. The vendor's brochure D. Source code
**Q06 (O2)** "PostgreSQL is enough" as an ADR conclusion is: A. Never valid B. Valid when evidence shows it meets the workload C. Valid only for small teams D. A sign of no analysis
**Q07 (O2)** Rate-limit counters with TTL fit best: A. A graph database B. Redis C. A data warehouse D. A search engine
**Q08 (O3)** Which is an operational cost of another database? A. Backup, monitoring, and on-call skills B. Smaller code C. Faster joins D. None
**Q09 (O3)** Keeping a second store in sync adds: A. Nothing B. Risk of divergence and extra failure modes C. Free consistency D. Less testing
**Q10 (O3)** Which choice rationale is weakest? A. Measured read/write ratio B. Query plan evidence C. Tested restore procedure D. "Everyone uses it"

## Answers
Q01 C · Q02 A · Q03 A · Q04 A · Q05 B · Q06 B · Q07 B · Q08 A · Q09 B · Q10 D

## Practical part
ADR review (`MID-044-EX04`) plus lab `MID-044-LAB1` (five ADRs). Pass: quiz at least 8/10, every ADR citing evidence, and at least one concluding that PostgreSQL is enough.
