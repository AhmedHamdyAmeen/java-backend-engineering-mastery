# ARC-029 · Privacy and compliance — Exercises and lab

## Lab
### ARC-029-LAB1 · Larkspur compliance architecture
**Outcomes:** 1–5 · **Time:** ~3.5 h
1. Classify Larkspur's data sets and fields; attach handling rules per class.
2. Write the retention schedule (periods supplied by role-played legal) including backups and analytics copies.
3. Design the data-subject-request flow across platform, ERP, and CRM, with confirmations and an audit entry.
4. Mark residency and cross-border flows on the system map and state controls.
5. Reduce payment scope with a hosted payment page and tokens; show the before and after scope.
6. Present to a role-played data protection officer.
**Acceptance:** reviewed by a role-played data protection officer; no card data stored in Larkspur systems.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| ARC-029-EX01 | 1 | Classify twelve Larkspur fields (email, card token, basket contents, store sales total, employee roster, delivery address, and others) and write one handling rule per class. |
| ARC-029-EX02 | 2 | Build a lifecycle and deletion table for orders, support chats, and marketing lists, including backups and the analytics warehouse. |
| ARC-029-EX03 | 2 | A deletion job removes customers from the platform database nightly. List five other places personal data may remain. |
| ARC-029-EX04 | 3 | Design the request workflow for an access request spanning platform, ERP, and CRM; define system owners, the deadline clock, and the audit entry. |
| ARC-029-EX05 | 4 | The CRM SaaS has support staff in another region and the analytics team wants to use a foreign cloud. Write the residency and transfer assessment questions and the architectural options. |
| ARC-029-EX06 | 5 | Support agents sometimes paste card numbers into case notes, and request logs capture full payloads. Propose controls so audit trails stay useful without sensitive data. |

## Solutions
- **EX01** Email, delivery address: personal; card token: payment-related (no card number allowed anywhere); basket: internal/personal when linked; store sales total: internal; roster: confidential/personal. Rules cover access role, encryption, log masking, allowed copies.
- **EX02** Orders: kept per finance requirement (periods from legal), personal fields anonymized afterwards; chats: short retention, redacted; marketing lists: until consent withdrawn; backups expire by schedule; analytics receives pseudonymous IDs and follows the same retention.
- **EX03** Search index, cache, analytics warehouse, CRM, ERP, email and marketing tools, exports, backups, logs.
- **EX04** One request intake; identity check; fan-out tasks to each system owner; confirmation recorded; deadline tracked from receipt; audit entry holds request ID, systems, outcome, not the personal data.
- **EX05** Questions: which laws apply, what data, which transfer mechanism, who has access. Options: regional deployment, restrict support access, tokenize or pseudonymize before export, contract safeguards. Legal confirms.
- **EX06** Hosted capture so cards never enter the platform; input masking and pattern detection in notes; log filters and field allowlists; audit log stores who, what, when, and IDs rather than payloads; scan logs periodically.

**Workplace evidence:** a compliance requirement you turned into architecture that passed an audit.
