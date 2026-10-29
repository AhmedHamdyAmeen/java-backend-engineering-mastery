# SRB-004 · Multi-region systems — Exercises and lab

## Lab
### SRB-004-LAB1 · EU expansion
**Outcomes:** 1, 2, 3, 4 · **Time:** ~4 h
1. Collect requirements: EU warehouses, EU data residency, RPO/RTO, latency.
2. Tier components and pick active-passive or active-active per tier.
3. Design the regional topology, routing, and data flows for Shop and FulfillCo.
4. Estimate cost delta and write the topology review notes.
**Acceptance:** residency enforced by design (no restricted data flows out); cost delta estimated.

## Exercises
| ID | Outcome | Task |
| --- | --- | --- |
| SRB-004-EX01 | 1 | A product owner wants multi-region for prestige. Write the questions you ask. |
| SRB-004-EX02 | 1 | Compare active-passive and active-active for checkout by cost, RPO, RTO, consistency. |
| SRB-004-EX03 | 2 | Design routing and health checks for the order API across two regions. |
| SRB-004-EX04 | 3 | List data flows that could violate EU residency in the FulfillCo design. |
| SRB-004-EX05 | 4 | Tier ten components into must/should/need not be multi-region. |
| SRB-004-EX06 | 4 | Find hidden single-region dependencies in a topology diagram and fix them. |

## Solutions
- **EX01** Which failure or law or latency problem? What RPO/RTO? Budget? Which components?
- **EX02** Active-passive: cheaper, RPO > 0, RTO minutes; active-active: costlier, near-zero RTO, conflict handling needed.
- **EX03** Global load balancer with health checks hitting a deep health endpoint (database and broker reachable), thresholds to avoid flapping, manual override.
- **EX04** Logs, backups, analytics, support tooling, cross-region replication, CI test data.
- **EX05** Checkout and stock reservation tier 1; tracking page tier 2; internal reports tier 3; justify each.
- **EX06** Identity, secrets, CI/CD, DNS, container registry; replicate or provide a degraded path.

**Workplace evidence:** a multi-region or residency design you contributed to.
