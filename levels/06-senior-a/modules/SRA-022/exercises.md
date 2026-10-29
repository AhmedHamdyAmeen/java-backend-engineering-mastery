# SRA-022 · Responsible AI and AI compliance — Exercises and lab

## Lab
### SRA-022-LAB1 · Responsible AI controls
**Outcomes:** 1–4 · **Time:** ~2 h
1. Build a register of Commerce 2030 marketplace AI features and propose a risk class for each.
2. Draw the data flow and residency analysis for each feature: what is sent to which model, where, and retention.
3. Draft transparency notices and design human oversight with an appeal path for high-impact decisions.
4. Design audit records and evidence for AI-assisted outcomes.
5. Review with a role-played legal and compliance advisor and revise.
**Acceptance:** reviewed with a role-played legal and compliance advisor; every high-risk use has human oversight and an audit trail.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| SRA-022-EX01 | 1 | Map the four principles to concrete controls, owners, and tests for a seller-listing assistant. |
| SRA-022-EX02 | 2 | A team wants to send full support chats to a hosted model. Write the review: data classes, terms to check, redaction, residency. |
| SRA-022-EX03 | 3 | Classify five marketplace AI uses by risk and justify each class; list what you need legal to confirm. |
| SRA-022-EX04 | 3 | Decide which uses need a transparency notice and write the notice text for the support assistant. |
| SRA-022-EX05 | 1 | Design human oversight and appeal for automatic seller account suspension, including reviewer evidence and time limits. |
| SRA-022-EX06 | 4 | Define the audit record and retention for AI-assisted refund decisions and explain how it supports an appeal. |

## Solutions
- **EX01** Transparency: label AI drafts. Fairness: evaluate quality across languages. Oversight: seller reviews before publishing. Accountability: named owner, incident process, logging. Each has a test or metric.
- **EX02** Allow only needed fields; redact personal identifiers; check provider retention, location, and training use (verify); use regional or self-hosted options if residency requires; get legal sign-off.
- **EX03** Examples: listing assistant minimal or limited risk; support assistant limited (disclosure); search ranking minimal; fraud scoring and seller suspension higher scrutiny because they affect income. Legal confirms class and obligations.
- **EX04** Notices where people interact with AI or receive AI-generated content, for example "This reply was drafted by an AI assistant; you may ask for a human agent."
- **EX05** Model recommends; trained reviewer decides for material actions; reviewer sees evidence and explanation; notice with reasons; appeal decided by a different human within a set time; metrics on overturns.
- **EX06** Record request id, time, model and prompt versions, inputs reference, output, reviewer and decision, reason; tamper-resistant storage; retention per legal advice; allows reconstructing why the refund was decided.

Outcome 1 is also covered by the quiz; outcome 4 by the lab audit design.

**Workplace evidence:** a responsible-AI or AI privacy control you designed and got adopted.
