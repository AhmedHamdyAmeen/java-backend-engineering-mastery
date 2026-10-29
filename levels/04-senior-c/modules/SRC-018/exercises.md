# SRC-018 · Security reviews — Exercises and lab

## Lab
### SRC-018-LAB1 · Secure design review
**Outcomes:** 1–4 · **Time:** ~3.5 h
Review a peer's redesign: data flow diagram with trust boundaries, threat list, authorization matrix across all paths, rated findings, and agreed actions with owners. Present to the peer and a role-played security lead.
**Acceptance:** review accepted by the peer and a role-played security lead.

## Exercises (assessment: review-quality rubric)
| ID | Outcome | Task |
| --- | --- | --- |
| SRC-018-EX01 | 1 | Draw the data flow and trust boundaries for orders, payments, and Kafka; list five threats with STRIDE categories. |
| SRC-018-EX02 | 1 | Adapt a generic checklist for a payment-handling, multi-tenant subsystem: choose ten items and explain the adaptation. |
| SRC-018-EX03 | 2 | Build an authorization matrix for six access paths to order data and write negative tests. |
| SRC-018-EX04 | 3 | Rate three findings by likelihood and impact, choose responses, and write an acceptance record for one. |
| SRC-018-EX05 | 4 | Case: the security lead rejects your design late. Write your response and working agreement for next time. |
| SRC-018-EX06 | 2 | Case: internal endpoint `/internal/orders/{id}` trusts any service in the cluster. Explain the risk and fix. |

## Solutions
- **EX01** Boundaries at gateway and provider; threats such as spoofing a service caller, tampering with events, information disclosure through logs, denial of service at the gateway, elevation through the admin tool.
- **EX02** Add payment data handling and tokenization, tenant isolation, secrets, logging of personal data, idempotency of payment calls, rate limiting, dependency scanning, audit trail, backups encryption, admin access.
- **EX03** Paths: public API, internal API, event consumers, batch jobs, admin tool, database access. Negative tests: another customer's ID, missing token, wrong role, forged internal call.
- **EX04** Ratings with rationale; mitigate high ones; accepted risk record has owner, rationale, compensating control, expiry.
- **EX05** Ask for specifics, compare against the agreed severity definitions, propose options with cost, and agree an early checkpoint and prepared package for next time.
- **EX06** Any compromised workload could read any order (confused deputy and lateral movement). Use service identity with scoped authorization and verify the end-user identity propagated.
- Outcome 4 is also covered by the lab acceptance and Q09-Q10.

**Workplace evidence:** a security review you led and its tracked outcomes.
