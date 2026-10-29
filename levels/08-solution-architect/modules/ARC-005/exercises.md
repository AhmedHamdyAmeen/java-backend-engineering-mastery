# ARC-005 · Architecture modeling — Exercises and lab

## Lab
### ARC-005-LAB1 · Larkspur current-state model
**Outcomes:** 1–4 · **Time:** ~3.5 h
1. Draw the system context diagram of today's landscape (stores, web shop, ERP, CRM, payment provider, carriers).
2. Create an ArchiMate layered view: business processes, applications, technology.
3. Draw an integration diagram of today's interfaces with protocol, direction, data, and owner.
4. Add a deployment sketch with environments and trust boundaries.
5. Add header blocks (audience, question, legend) and check names are consistent across diagrams.
**Acceptance:** each diagram has a legend, an audience, and the question it answers.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| ARC-005-EX01 | 1 | For five Larkspur questions, choose the notation (C4, UML, ArchiMate) and justify. |
| ARC-005-EX02 | 1 | Draw a C4 context diagram for the new commerce platform with six neighbours. |
| ARC-005-EX03 | 2 | Draw a sequence diagram for order payment with provider timeout and retry. |
| ARC-005-EX04 | 3 | Draw a deployment diagram with store LAN, data center, and cloud zones; mark where payment data crosses a boundary. |
| ARC-005-EX05 | 4 | Review a given diagram set for naming inconsistencies and missing legends; list fixes. |
| ARC-005-EX06 | 4 | Propose how to keep the Larkspur model as code (text source, generated views, version control) and what you would not model. |

## Solutions
- **EX01** Structure of the platform → C4; payment call order and failure → UML sequence; which applications support which processes → ArchiMate; order lifecycle → UML state; which environments hold data → deployment diagram.
- **EX02** Neighbours: customers, store staff, ERP, CRM, payment provider, carrier service; each labelled with purpose and protocol.
- **EX03** Order service calls provider; on timeout, query status by idempotency key before retrying; show alt and failure branches.
- **EX04** Trust boundary lines between store LAN, data center, cloud; the payment provider link crossing the boundary is labelled with TLS and tokenized card data.
- **EX05** Typical issues: the same system named "ERP", "SAP", and "Finance system"; arrows without direction; no legend. Fix with a shared glossary and standard legend.
- **EX06** Text-based sources (for example C4 DSL or diagram-as-code), generated images, kept in a repo with review; do not model every class or every minor interface.

Outcome 2 is also covered by the lab integration diagram.

**Workplace evidence:** architecture diagrams that business and engineering stakeholders both used.
