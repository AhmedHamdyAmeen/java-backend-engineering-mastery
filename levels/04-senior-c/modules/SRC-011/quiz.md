# SRC-011 · Production readiness — Quiz

Outcomes: O1 readiness review · O2 deployment safety · O3 go/no-go · O4 data rollback.

**Q01 (O1)** A readiness finding is strongest when it cites: A. A team's confidence B. A checkable result or link C. The release date D. A manager's opinion
**Q02 (O1)** Which is NOT one of the five review areas used here? A. Observability B. Capacity C. Marketing copy D. Support
**Q03 (O2)** A canary is: A. A load test in staging B. A small share of traffic on the new version compared to the old C. A database backup D. A code review
**Q04 (O2)** Feature flags let you: A. Skip testing B. Separate deploy from release C. Avoid monitoring D. Remove rollback needs
**Q05 (O2)** Automated analysis should abort when: A. A human gets bored B. The build is old C. Traffic rises D. Guard metrics breach agreed tolerance against baseline
**Q06 (O3)** Go/no-go criteria should be set: A. After the review B. Before the review C. After launch D. Never in writing
**Q07 (O3)** An accepted risk should have: A. No record B. A secret location C. An owner and an expiry date D. A lower severity automatically
**Q08 (O2)** Why include a business metric in canary analysis? A. A change can return 200s yet break outcomes B. Technical metrics are always wrong C. It is cheaper D. Kubernetes requires it
**Q09 (O4)** In expand and contract, when is the old column dropped? A. First B. During the first deploy C. Never allowed D. Later, after the new path is proven
**Q10 (O4)** Which makes rollback of a data change possible? A. Deleting backups B. Skipping migration tests C. Deploying on Fridays D. New code that tolerates the old schema

## Answers
Q01 B · Q02 C · Q03 B · Q04 B · Q05 D · Q06 B · Q07 C · Q08 A · Q09 D · Q10 D

## Practical part
Run a readiness review for a peer's service and write the go/no-go record (SRC-011 assessment), plus `SRC-011-LAB1` evidence. Pass: at least 8/10 on the quiz, a review with evidence-based findings and owners, and a seeded regression halted in the lab.
