# ARC-030 · Data governance — Exercises and lab

## Lab
### ARC-030-LAB1 · Larkspur data governance
**Outcomes:** 1–4 · **Time:** ~2.5 h
1. Name owners and stewards for the key data sets (products, prices, customers, orders, stock, payments, sales).
2. Write ten data quality rules with dimension, measure, threshold, owner, and reporting place.
3. Draw lineage for the daily sales report from till and web order to board report.
4. Write analytics access policies by role and data class, including masking.
5. Review with a role-played head of finance and data owner.
**Acceptance:** lineage complete from till and web order to board report.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| ARC-030-EX01 | 1 | Larkspur has a governance committee but nobody can say who owns customer addresses. Propose the ownership model for the customer data set. |
| ARC-030-EX02 | 1 | Separate the roles of owner, steward, and custodian for the product price list and give an example decision for each. |
| ARC-030-EX03 | 2 | Write five quality rules for stock levels with measure and threshold. |
| ARC-030-EX04 | 2 | A quality dashboard exists but nobody acts on it. Redesign how breaches are reported and handled. |
| ARC-030-EX05 | 3 | Draw lineage for "returns rate by store" from till to report and mark where a defect would most likely enter. |
| ARC-030-EX06 | 4 | A marketing analyst asks for the full customer table. Write the access decision and the policy for analytics consumers. |

## Solutions
- **EX01** Owner: head of customer service or CRM business lead, accountable for rules; stewards per channel; custodians are the CRM and platform teams; system of record named; decisions logged.
- **EX02** Owner decides price rules and approvals; steward maintains price lists and fixes errors; custodian (ERP team) runs the system and backups.
- **EX03** Examples: no negative stock; every SKU has a location; stock count updated within 15 minutes for store scans (timeliness); stock difference between platform and ERP under 0.5 percent; no duplicate SKU-location rows. Thresholds are examples to agree with the owner.
- **EX04** Add owner and threshold per rule, alerts to steward, ticketing with deadline, weekly review, escalation to owner; track trend and closure.
- **EX05** Till sale → platform return event → ERP posting → warehouse fact → report; defects often enter at return reason mapping and store code mismatch between systems.
- **EX06** Give a pseudonymized, minimal view (segment, region, purchase categories) approved by the data owner; no direct identifiers; access logged; request a new approval for anything more.

**Workplace evidence:** a data quality or lineage improvement you led.
