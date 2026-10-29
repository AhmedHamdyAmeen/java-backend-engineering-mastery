# ARC-042 · Architecture assurance — Quiz

Outcomes: O1 design reviews and drift · O2 NFR testing evidence · O3 operational acceptance · O4 go-live decision.

**Q01 (O1)** The ARB approved the design in March. In June a team's batch job reads ERP tables directly, against the HLD. This is: A. Acceptable because it works B. Not your concern after approval C. Architecture drift to be logged and resolved or consciously accepted D. A testing defect only
**Q02 (O1)** Best way to detect drift in a team's design? A. Read their slide summary B. Wait for go-live C. Ask the sponsor D. Inspect actual configuration and flows in a review
**Q03 (O1)** Assurance that ends at design approval is a mistake because: A. Approval is optional B. The built system can differ from the approved design C. Teams dislike it D. Tests are cheaper later
**Q04 (O2)** "Checkout p95 under 2 s at peak" is best evidenced by: A. A developer's statement B. A single request timing C. A load test at peak volume with realistic data, reported against the target D. Code review
**Q05 (O2)** A resilience requirement states the shop must keep taking orders when the ERP is unavailable. Evidence is: A. A fault test taking ERP down and showing orders continue as designed B. An architecture diagram C. ERP vendor SLA D. A unit test of the order class
**Q06 (O2)** Which evidence is weakest? A. Penetration test report with retest B. Reproducible load test report C. Restore test log with timings D. "Security looked at it and it was fine"
**Q07 (O3)** Which operational acceptance check is verified by doing, not reading? A. Runbook exists B. Backup and restore performed and timed against RTO C. Diagram approved D. Contract signed
**Q08 (O3)** Which item belongs in operational acceptance for a mixed SaaS and owned estate? A. Vendor escalation path tested with the vendor B. Choice of IDE C. UI colours D. Sprint length
**Q09 (O4)** Functional and performance tests pass, but a high security finding is open and restore was never tested. The most defensible recommendation is: A. Go, and fix later B. Conditional go or no-go, with named conditions, owners, and dates traceable to evidence C. Ignore the finding because it is one D. Cancel the project
**Q10 (O4)** Who accepts residual risk at go-live? A. The architect silently B. The delivery team C. The accountable business owner, explicitly, with risks documented D. Nobody

## Answers
Q01 C · Q02 D · Q03 B · Q04 C · Q05 A · Q06 D · Q07 B · Q08 A · Q09 B · Q10 C

## Practical part
Go/no-go decision review on the Larkspur lab: assurance checkpoints, NFR evidence per requirement, operational acceptance checklist, and a recommendation traceable to the provided test results. Pass: quiz at least 8/10, at least four of five exercises correct, and a lab with a justified recommendation.
