# ARC-034 · Architecture deliverables — Quiz

Outcomes: O1 HLD and LLD · O2 ADRs · O3 interface contracts · O4 deployment diagrams.

**Q01 (O1)** The primary reader of an HLD is: A. The compiler B. The delivery team's newest developer C. Reviewers and sponsors who approve direction D. Only operations
**Q02 (O1)** Which content belongs in an LLD rather than an HLD? A. Context view B. Sequence flow with retry limits and failure cases C. Business goals D. Key decisions summary
**Q03 (O1)** A team estimates from an LLD and keeps asking what is in scope. The LLD most likely lacks: A. Colors B. Page numbers C. A table of contents D. Clear scope, boundaries, and edge cases
**Q04 (O2)** An ADR should be written: A. When the decision is made B. After go-live C. Only for failed decisions D. Never for small teams
**Q05 (O2)** Which element is essential in an ADR? A. Vendor logo B. Options considered and consequences C. Meeting attendee list D. Sprint number
**Q06 (O3)** A contract precise enough for parallel delivery states: A. Only the endpoint name B. Only the team name C. Operations, schemas, error codes, authentication, versioning, and owner D. A screenshot of the UI
**Q07 (O3)** Why publish a contract as a machine-readable file? A. Both teams can build stubs and tests from the same definition B. It is shorter C. It avoids ownership D. It removes the need for versioning
**Q08 (O4)** A deployment diagram that operations can use shows: A. Class hierarchies B. Requirements only C. Runtime nodes, zones, networks, and failover paths D. User personas
**Q09 (O1)** Which is a common HLD mistake? A. Linking to detail B. Listing risks C. Stating quality targets D. Including implementation detail such as class names
**Q10 (O2)** Larkspur chose events over nightly batch for ERP posting. The ADR consequences should mention: A. Colors of the dashboard B. The number of developers C. Needed replay, ordering rules, and monitoring D. Nothing; the decision is obvious

## Answers
Q01 C · Q02 B · Q03 D · Q04 A · Q05 B · Q06 C · Q07 A · Q08 C · Q09 D · Q10 C

## Practical part
Deliverable review against a checklist on the Larkspur lab: HLD without implementation detail, LLD with failure cases, five ADRs, two contracts, and a deployment diagram. Pass: quiz at least 8/10, at least five of six exercises correct, and a lab where the role-played delivery lead can estimate without scope clarifications.
