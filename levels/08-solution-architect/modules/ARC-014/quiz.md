# ARC-014 · Compute choices — Quiz

Outcomes: O1 compare options · O2 match to workload shape · O3 decide on Kubernetes.

**Q01 (O1)** Which option gives the most control and the most operating work? A. Functions B. Managed containers C. Virtual machines D. SaaS
**Q02 (O1)** Serverless functions typically: A. Run forever without limits B. Need a cluster C. Cannot be event-triggered D. Scale to zero and charge per execution
**Q03 (O1)** A managed container platform removes the need to: A. Build container images B. Administer the underlying servers or cluster C. Monitor the application D. Handle deployments
**Q04 (O2)** A nightly restartable batch job fits best on: A. A scheduled job on on-demand or discounted capacity B. An always-on large VM C. A Kubernetes cluster built for it D. A database trigger
**Q05 (O2)** Steady predictable load is usually cheapest on: A. Functions B. Reserved or committed containers or VMs C. Burst-only capacity D. Manual servers
**Q06 (O2)** A known risk of spiky function workloads is: A. Never scaling B. Overwhelming downstream databases C. No pay-per-use D. Requiring VMs
**Q07 (O3)** Kubernetes is most justified when there are: A. Two services and three engineers B. No platform team C. Many services, several teams, and a platform team D. A desire to learn it
**Q08 (O3)** The default for a small team with simple workloads is: A. Self-managed Kubernetes B. A managed container service or PaaS C. Bare metal D. Custom orchestration
**Q09 (O3)** A good ADR for compute includes: A. Only the product name B. The team's skills, on-call capacity, and revisit trigger C. A vendor logo D. No consequences
**Q10 (O3)** "Serverless for long-running steady load" is a mistake because: A. Functions cannot run at all B. Pay-per-run pricing is usually costlier than steady capacity and limits apply C. Functions are insecure D. They need Kubernetes

## Answers
Q01 C · Q02 D · Q03 B · Q04 A · Q05 B · Q06 B · Q07 C · Q08 B · Q09 B · Q10 B

## Practical part
ADR review of the `ARC-014-LAB1` compute decisions plus exercises `ARC-014-EX01` to `EX06`. Pass: quiz at least 8/10, at least five of six exercises correct, and each ADR including the team's skills and operating capacity.
