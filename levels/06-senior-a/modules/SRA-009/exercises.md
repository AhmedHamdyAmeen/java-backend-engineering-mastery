# SRA-009 · Security and compliance — Exercises and lab

## Lab
### SRA-009-LAB1 · Marketplace compliance
**Outcomes:** 1–4 · **Time:** ~2 h
1. Build a data inventory for marketplace seller data, buyer data, and payout data with purposes, retention, and systems holding copies.
2. Translate privacy and payment obligations (confirm with the role-played compliance officer) into architecture requirements with controls and evidence.
3. Design the audit trail for access and changes to seller and payout data.
4. Reduce payment scope with tokenization and segmentation; show the before and after boundary.
5. Design right-to-erasure across services, including derived stores and backups.
**Acceptance:** reviewed with a role-played compliance officer.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| SRA-009-EX01 | 1 | For a seller onboarding form, apply minimization, purpose, retention, and consent: list what to collect, keep, and delete. |
| SRA-009-EX02 | 1 | Review a proposal to copy full customer records into an analytics lake; propose a privacy-by-design alternative. |
| SRA-009-EX03 | 2 | Design an audit event schema and storage for payout approvals; state who can read and who cannot alter. |
| SRA-009-EX04 | 3 | Take three obligations given in plain language and write the requirement, control, test, and evidence for each. |
| SRA-009-EX05 | 4 | Draw the before and after payment data flow with tokenization and list which services leave scope. |
| SRA-009-EX06 | 4 | Write the erasure design for 30 services including derived stores, backups, legal retention, and a verification test. |

## Solutions
- **EX01** Collect identity and payout details required for the contract and tax; do not collect extra attributes; tag purpose; set retention after contract end, subject to legal rules; record consent for optional marketing separately.
- **EX02** Pseudonymize identifiers, exclude unneeded fields, limit by purpose, apply retention, restrict access, and publish a data contract with the owner.
- **EX03** Fields: actor, action, subject, time, source, result, request id; append-only store; read access to auditors; writers cannot edit; avoid logging sensitive values; retention per policy.
- **EX04** Pattern example: access request → system can locate and export a subject's data → export tool and test with synthetic subject → report and audit evidence, with an owner. Verify obligations with compliance.
- **EX05** Before: card data passes through many services. After: browser sends data directly to a hosted field; back end sees tokens; only the provider integration remains in scope; confirm with the compliance officer.
- **EX06** Event-driven deletion with coordinator, per-service confirmation, derived stores and search covered, backups expire on schedule, legally required records retained with restricted use, and a synthetic-user test.

Outcome 2 is also covered by the lab audit design and the quiz.

**Workplace evidence:** an architecture change you led that reduced compliance risk or scope.
