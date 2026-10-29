# ARC-020 · Infrastructure governance — Quiz

Outcomes: O1 landing zone · O2 guardrails · O3 tagging · O4 infrastructure as code.

**Q01 (O1)** A landing zone is: A. A runway for aircraft B. A single virtual machine C. A prepared foundation of accounts, network, logging, and security baseline D. A billing report
**Q02 (O1)** Guardrails are best added: A. Before workloads go live B. After an incident C. After the first audit D. Never
**Q03 (O1)** Why design the hierarchy around policy? A. Policies inherit down the tree B. Looks tidy C. It is required by tags D. It avoids IaC
**Q04 (O2)** A preventive guardrail: A. Reports after the fact B. Blocks a non-compliant action C. Only sends email D. Deletes the account
**Q05 (O2)** A detective guardrail: A. Prevents creation B. Finds drift or violations after they happen C. Replaces review D. Encrypts data
**Q06 (O2)** An exception process should have: A. No record B. An owner and an expiry C. Permanent approval D. No review
**Q07 (O3)** Tags without enforcement: A. Stay perfect B. Reduce cost C. Decay and make reports unreliable D. Improve security
**Q08 (O3)** A useful mandatory tag set includes: A. Favorite color B. Owner, cost center, environment, data classification C. Developer nickname D. Random IDs only
**Q09 (O4)** In prod, changes should go through: A. Pull request, review, checks, and pipeline B. Direct console edits C. Verbal agreement D. Personal scripts
**Q10 (O4)** Drift detection compares: A. Costs to budgets B. Users to roles C. Logs to alerts D. Real infrastructure to its code definition

## Answers
Q01 C · Q02 A · Q03 A · Q04 B · Q05 B · Q06 B · Q07 C · Q08 B · Q09 A · Q10 D

## Practical part
Landing zone review of the `ARC-020-LAB1` design and walkthrough plus exercises `ARC-020-EX01` to `EX06`. Pass: quiz at least 8/10, at least five of six exercises correct, and a non-compliant resource blocked or detected in the walkthrough.
