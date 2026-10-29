# ARC-038 · Operational architecture — Exercises and lab

## Lab
### ARC-038-LAB1 · Larkspur operations
**Outcomes:** 1–4 · **Time:** ~3 h
1. Design monitoring, alerting, and logging for owned, SaaS, and on-premises components.
2. Define the support model: tiers, hours, escalation.
3. Build the ownership map for services and integrations.
4. Define vendor escalation paths and the incident and change alignment.
5. Write operational acceptance criteria for handover.
6. Review with a role-played head of IT operations.
**Acceptance:** reviewed by a role-played head of IT operations.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| ARC-038-EX01 | 1 | Design monitoring for the checkout journey across the platform, a payment SaaS, and the on-premises ERP. Include business metrics and a synthetic check. |
| ARC-038-EX02 | 1 | Support complains they cannot trace an order across systems. Define the correlation and logging approach. |
| ARC-038-EX03 | 2 | Define the support tiers, hours, and escalation for web checkout and for store tills. |
| ARC-038-EX04 | 2 | The order-to-ERP integration is "owned" by both platform and ERP teams. Resolve ownership. |
| ARC-038-EX05 | 3 | The payment vendor promises 4-hour response for priority 1. Larkspur's severity-1 expects 15-minute engagement. Align the processes. |
| ARC-038-EX06 | 4 | Write ten operational acceptance criteria for go-live handover. |

## Solutions
- **EX01** Signals: order rate, payment success rate, ERP queue lag, latency; synthetic checkout every few minutes; SaaS status feed; alerts to on-call with severity; owners per signal.
- **EX02** Correlation ID created at entry and passed through events and API calls; structured logs; central search; sensitive data excluded; retention set; support given a lookup tool.
- **EX03** Web: 24x7 monitoring with on-call for severity 1-2, service desk first line; tills: support aligned to store trading hours, field support and a hotline; escalation times per severity.
- **EX04** Assign the platform team as owner (it runs the integration code and monitoring) with the ERP team as named contact and an agreed interface contract; document in the ownership map.
- **EX05** Ask the vendor for a faster priority tier or a premium support contract; internal bridge while waiting; fallback provider or degraded mode so Larkspur does not depend on the vendor's response; record in the contract review.
- **EX06** Examples: monitoring and alerts live with tested routing; runbooks written and walked through; backup and restore tested; support trained; owners named; escalation tested; capacity and failover tested; access in place; documentation handed over; known issues accepted by operations.

**Workplace evidence:** an operating or support model you designed for a solution.
