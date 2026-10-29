# ARC-018 · Network security — Exercises and lab

## Lab
### ARC-018-LAB1 · Larkspur network security
**Outcomes:** 1–4 · **Time:** ~3 h
1. Inventory public endpoints and external connections.
2. Design the layered controls: edge, WAF, security groups, firewalls.
3. Write the segmentation plan and flow matrix with the payment segment isolated.
4. Define WAF rules and DDoS posture for every public endpoint.
5. Define controls around the payment flow and the private connectivity to the payment provider and partners.
6. Add a note on which risks are covered by identity controls instead.
**Acceptance:** payment-related components isolated; every public endpoint protected.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| ARC-018-EX01 | 1 | List the layers a request passes from a customer to the order database and the control at each. |
| ARC-018-EX02 | 1 | Write security group rules for the order service (inbound, outbound). |
| ARC-018-EX03 | 2 | Draw a flow matrix for web, app, data, payment, and management segments. |
| ARC-018-EX04 | 2 | A flat network is audited for card-payment scope and the whole platform is in scope. Propose a fix. |
| ARC-018-EX05 | 3 | Design how Larkspur connects to a logistics partner that offers only an internet API. |
| ARC-018-EX06 | 4 | An attacker with a stolen staff token reaches the back office from an allowed network. Explain which controls still matter and what network controls cannot stop. |

## Solutions
- **EX01** CDN/DDoS, WAF, load balancer, service security group, service authorization, database security group, database authentication and encryption.
- **EX02** Inbound: only from the load balancer's group on the service port. Outbound: only the database group, ERP adapter, and approved endpoints; deny the rest.
- **EX03** Web to app allowed on the service port; app to data on database ports; app to payment segment on specific ports only; management from a bastion/SSO path; everything else denied.
- **EX04** Isolate payment components in a dedicated segment, tokenize card data via the provider so the rest of the platform never holds it, and re-scope the audit to the small segment.
- **EX05** TLS with mutual authentication or strong API credentials, IP allow-list both ways, rate limits, logging, signed payloads; revisit private connectivity if volume or sensitivity grows.
- **EX06** Identity controls: MFA, conditional access, short token life, least-privilege roles, anomaly detection, audit logs. Network controls cannot judge a valid token from an allowed network.

**Workplace evidence:** a network security design you implemented or reviewed.

---
Outcome coverage: all outcomes covered by exercises and the lab.
