# ARC-012 · Cloud architecture — Exercises and lab

## Lab
### ARC-012-LAB1 · Larkspur target architecture
**Outcomes:** 1–4 · **Time:** ~4 h (written for one provider; verify service names before recording)
1. Collect the requirements from `ARC-003-LAB1`: availability, residency, peak load, ERP link, store connectivity.
2. Choose region and zones with reasons; note the DR option.
3. Design the account/subscription and environment structure.
4. Draw the target architecture diagram (edge, application, data, integration) with trust boundaries.
5. Add a traceability table: each element to its requirement.
**Acceptance:** each element traceable to a requirement from `ARC-003-LAB1`.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| ARC-012-EX01 | 1 | Larkspur's customers are in one country and the law requires customer data to stay in it. Choose a region strategy and explain the DR implication. |
| ARC-012-EX02 | 1 | Compare single-zone, multi-zone, and multi-region for the storefront: what each survives and what it costs. |
| ARC-012-EX03 | 2 | A reference architecture includes a global database, a streaming pipeline, and a CDN. Classify each as adopt, adapt, or reject for Larkspur. |
| ARC-012-EX04 | 3 | Propose an account structure for Larkspur and justify each account. |
| ARC-012-EX05 | 3 | A developer's leaked key was used in a one-account setup. Describe the blast radius there versus in your structure. |
| ARC-012-EX06 | 4 | Review a draft diagram with no trust boundaries; list the boundaries to add and what crosses each. |

## Solutions
- **EX01** Primary region in-country; keep DR in-country (a second region or a second site) or confirm legal permission before replicating abroad; edge caching holds no personal data.
- **EX02** Single zone: survives nothing structural; cheap. Multi-zone: survives a data center loss; moderate cost. Multi-region: survives a regional outage; highest cost and complexity (data replication, failover).
- **EX03** Global database: reject (no requirement). Streaming pipeline: reject unless real-time analytics is a requirement. CDN: adopt for media and static assets.
- **EX04** Prod, non-prod (dev/test), shared-network, security-logging (read-only for most), sandbox with budget cap. Each isolates identity, billing, and failure.
- **EX05** One account: the key reaches prod data and everything. Split: the key is limited to non-prod, no path to prod data; detection through central logging.
- **EX06** Internet to edge; edge to application; application to data tier; platform to on-premises ERP; platform to third-party payment provider. Note authentication and encryption at each crossing.

**Workplace evidence:** a cloud architecture you designed that went to production.

---
Outcome coverage: all outcomes covered by exercises and the lab.
