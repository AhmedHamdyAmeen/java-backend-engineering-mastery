# ARC-023 · Data architecture — Exercises and lab

## Lab
### ARC-023-LAB1 · Larkspur data architecture
**Outcomes:** 1–4 · **Time:** ~3 h
1. List every Larkspur data set from the case brief and interview notes.
2. Draw the conceptual data model and mark one system of record per entity.
3. Draw the data-flow view from stores and web to ERP, CRM, platform, and reporting; label each arrow with data set and trigger.
4. Choose warehouse, lake, or lakehouse for the three reporting needs and justify.
5. Fill the lifecycle table: stages, retention with its source, copies, deletion trigger.
6. Defend the view to a role-played head of reporting.
**Acceptance:** every data set has one system of record and a defined retention.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| ARC-023-EX01 | 1 | The store-ops lead runs a nightly stock report on the production order database and checkout slows at 02:00. Write a half-page note explaining the cause and the target design. |
| ARC-023-EX02 | 2 | For "customer profile", fill a five-stage lifecycle with retention, copies, and deletion trigger. |
| ARC-023-EX03 | 3 | Choose warehouse, lake, or lakehouse for: finance daily sales, store camera footfall counts, demand-forecast training. Justify each in two lines. |
| ARC-023-EX04 | 4 | Draw a conceptual model for returns (Customer, Order, ReturnRequest, Refund, Product) and mark systems of record. |
| ARC-023-EX05 | 1, 4 | Two systems both claim to own product prices. Propose the system of record, the flow, and what the other system may do. |
| ARC-023-EX06 | 2, 3 | Review a data architecture with no deletion stage and a lake holding copies of customer files; give three corrections. |

## Solutions
- **EX01** Long scans compete with checkout for I/O and locks; move reporting to a replica or warehouse fed by change capture; keep the store report on the analytical copy.
- **EX02** Create at sign-up (CRM and platform); use while the account is active; share with the delivery carrier (address only); archive after inactivity period set by policy; delete on request or at the retention end, including warehouse and backups; verify periods with legal.
- **EX03** Finance: warehouse (modeled, reconciled); footfall: lake (raw, semi-structured, exploratory); forecast training: lakehouse or lake with a curated layer, depending on team skills.
- **EX04** Customer, Order, ReturnRequest (platform), Refund (payment provider and ERP posting), Product (ERP); relations Order 1-many ReturnRequest, ReturnRequest 1-1 Refund.
- **EX05** ERP is system of record; platform consumes prices through an interface and caches; platform may propose promotions through ERP, not edit prices locally.
- **EX06** Add deletion and archive stages; list all copies with owners; apply the same retention to the lake as to the source; add classification to lake folders.

All four outcomes are also covered by the lab acceptance and the quiz.

**Workplace evidence:** a data architecture view you produced that guided a reporting or platform decision.
