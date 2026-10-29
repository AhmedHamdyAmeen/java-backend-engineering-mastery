# SRA-004 · Data ownership strategy — Exercises and lab

## Lab
### SRA-004-LAB1 · Ownership map
**Outcomes:** 1–4 · **Time:** ~2 h
1. Inventory the major operational and analytical data sets in Commerce 2030 with current holders and consumers.
2. Assign one owner per data set, mark authoritative sources and copies.
3. Write data contracts for the five most consumed data sets: schema, semantics, quality rules, SLAs, versioning policy.
4. Define a classification and governance model for sensitive data with decision rights.
5. Assess data mesh readiness and choose which ideas to adopt now.
**Acceptance:** every data set has one owner; contracts include quality SLAs.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| SRA-004-EX01 | 1 | Given a map where five teams hold copies of product data, assign one owner and label authoritative source versus copies. |
| SRA-004-EX02 | 1 | Decide ownership for analytical data derived from orders: who owns the warehouse model, and who owns the revenue metric? |
| SRA-004-EX03 | 2 | Write a data contract for `SellerPayoutIssued`: schema, semantics, quality rule, freshness, versioning. |
| SRA-004-EX04 | 2 | A producer plans a breaking change. Write the notice process and automated checks that prevent surprise. |
| SRA-004-EX05 | 3 | Design a governance model for personal and payment data that does not route every request through one team. |
| SRA-004-EX06 | 4 | Score the organization's readiness for data mesh and recommend which ideas to adopt in year one. |

## Solutions
- **EX01** The domain that creates and changes the data owns it (for example Catalog owns product data); others hold labeled copies refreshed from the source with a stated lag.
- **EX02** The Orders team owns the source events; the analytics or Finance team owns the warehouse model; Finance owns the revenue metric definition, with a contract reconciling it with Orders.
- **EX03** Include: payout id, seller id, gross, fees, net, currency, issued time; semantics of each amount; rule that net equals gross minus fees; freshness SLA (agree with consumers); additive changes minor, removals major with notice.
- **EX04** Notice period, version both old and new for an overlap, compatibility check in the producer pipeline, consumer-driven tests, and a named contact for each consumer.
- **EX05** Classify once, apply default controls by class, let owners approve within policy, automate masking and access logging, and escalate only exceptions. Measure time to access and incidents.
- **EX06** Score domain team stability, platform maturity, catalog, and consumer demand. Typical year one: ownership, contracts, and catalog first; self-serve platform and wider mesh later.

Outcome 3 is also covered by the governance step in the lab; outcome 4 by the lab readiness assessment and quiz.

**Workplace evidence:** a data contract or ownership agreement you established between teams.
