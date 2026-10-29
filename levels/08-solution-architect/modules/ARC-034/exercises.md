# ARC-034 · Architecture deliverables — Exercises and lab

## Lab
### ARC-034-LAB1 · Larkspur HLD and LLD
**Outcomes:** 1–4 · **Time:** ~4 h
1. Write the platform HLD: scope, constraints, context and container views, quality attribute targets, risks, and open questions.
2. Write ADRs for the five biggest decisions, each with context, options, decision, and consequences.
3. Write the LLD for order fulfillment: state model, sequence flows, failure cases, and non-functional specifics.
4. Write interface contracts for the ERP order posting and the payment provider, with schemas, error codes, and versioning.
5. Draw the deployment diagram with zones, environments, and the link to on-premises ERP.
6. Hand the LLD to a role-played delivery lead and resolve every clarification asked.
**Acceptance:** a role-played delivery lead can estimate from the LLD without asking for clarifications on scope.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| ARC-034-EX01 | 1 | A 60-page Larkspur HLD contains table definitions and Spring configuration, and the board has not read it. Write a review note listing what to move out and what to keep. |
| ARC-034-EX02 | 1 | Take the LLD for "click and collect orders" and list ten failure and edge cases it must cover. |
| ARC-034-EX03 | 2 | Write an ADR for "use event notifications from the platform to ERP instead of nightly batch", with at least two rejected options. |
| ARC-034-EX04 | 2 | A team wrote its ADR three months after the decision. Explain the risks and set a rule for when ADRs are written. |
| ARC-034-EX05 | 3 | Write the contract for "post order to ERP": fields, required/optional, errors, idempotency, version policy, owner. |
| ARC-034-EX06 | 4 | Draw a deployment diagram for the Larkspur platform in two environments and list five facts operations needs that a logical diagram omits. |

## Solutions
- **EX01** Keep purpose, context, decisions, quality targets, risks; move schemas and configuration to the LLD or repositories; link rather than embed; one-page summary on top.
- **EX02** Examples: stock changes between order and pick; store closed at pickup time; customer misses the pickup window; duplicate order submission; payment captured but ERP unreachable; partial pickup; ID check fails; item damaged at the store; carrier or store system timeout; refund after expiry.
- **EX03** Context: ERP outages blocked nightly batch and orders arrived late; options: nightly batch, event notifications, direct synchronous calls; decision: events with ERP adapter; consequences: needs replay, ordering rules, and monitoring.
- **EX04** Reasons are forgotten and the record is rewritten to look rational; rule: draft the ADR when the options are compared, mark it proposed, and accept it at decision time.
- **EX05** Operation POST orders with orderId and idempotency key required; lines, totals, tax required; errors for validation (400), duplicate (409 with original id), unavailable (503); versioned in the path or schema version header; owner named on both sides.
- **EX06** Zones, networks and ports, hostnames or services, failover and replica placement, backup targets, secrets location, and environment differences.

All four outcomes are also covered by the lab acceptance and the quiz.

**Workplace evidence:** an HLD or LLD you wrote that a team delivered from.
