# ARC-P1 — Business and Enterprise Architecture Foundations

**Phase goal:** the architect understands the business before designing for it: the architecture roles around them, the organization's capabilities and value streams, how to discover real requirements, how frameworks and models structure architecture work, how a solution moves from idea to transition, which principles guide choices, how technology options are assessed, how enterprise systems integrate, and how legacy is modernized.

**Running case:** *Larkspur Retail* (fictional). A mid-size retailer with 120 stores and a dated on-premises web shop needs a platform for web and mobile customers, inventory, payments, order fulfillment, customer service, and reporting, integrated with its existing ERP and CRM. The learner is the solution architect engaged to design it. Every lab produces a piece of the Architect capstone package (`ARC-CAP`).

**Format:** case studies, worked architecture sessions, and stakeholder role-play. Solution Architect is a related track to Staff, not a step after it; prerequisites draw on the Senior levels. Each module lists the workplace evidence that demonstrates the role.

**Phase total:** ~12.2 h video · ~33 h practice

---

### ARC-001 · Architecture roles
`n: 255` · **Video:** 67 min · **Practice:** 2.5 h

**Prerequisites:** SRC-010

**Learning outcomes** — the architect can:
1. Distinguish software, solution, enterprise, cloud, and data architects by scope, horizon, and typical deliverables.
2. Explain where a solution architect sits between business stakeholders, enterprise architecture, delivery teams, and vendors.
3. Describe the solution architect's accountabilities on a program and what they are *not* accountable for.
4. Plan a personal transition from senior engineer to solution architect.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| ARC-001-L01 | What architects actually do | 10 |
| ARC-001-L02 | Software, solution, enterprise, cloud, and data architects | 12 |
| ARC-001-L03 | The solution architect in a program | 12 |
| ARC-001-L04 | Accountabilities and boundaries | 10 |
| ARC-001-L05 | From senior engineer to architect | 10 |
| ARC-001-L06 | Demo: mapping the architecture roles on the Larkspur program | 13 |

**Lab** — `ARC-001-LAB1` *Larkspur engagement charter:* a one-page charter defining the solution architect's scope, stakeholders, decision rights, and interfaces with enterprise architecture, delivery teams, and vendors. Acceptance: reviewed by a role-played program sponsor; no overlap or gap with other roles.

**Common mistakes:** acting as the lead developer; owning decisions that belong to the business or enterprise architecture.

**Assessment:** charter review plus role-scenario quiz.

**Workplace evidence:** a program where you held a defined architecture role with written scope and decision rights.

**Career relevance:** frames the whole level and the Staff vs Architect career choice (STF-001).

---

### ARC-002 · Business architecture
`n: 256` · **Video:** 79 min · **Practice:** 3.5 h

**Prerequisites:** SRA-001, ARC-001

**Learning outcomes** — the architect can:
1. Build a business capability map and assess each capability's maturity and strategic importance.
2. Model value streams and the processes that realize them.
3. Map stakeholders by influence and interest and identify their goals and concerns.
4. Trace a proposed solution's components back to the capabilities and value streams they serve.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| ARC-002-L01 | Why architects start with the business | 8 |
| ARC-002-L02 | Business capabilities | 12 |
| ARC-002-L03 | Capability maps and heat maps | 10 |
| ARC-002-L04 | Value streams and processes | 12 |
| ARC-002-L05 | Stakeholder mapping | 8 |
| ARC-002-L06 | Demo: Larkspur's capability map, built live | 15 |
| ARC-002-L07 | Demo: tracing "buy online, pick up in store" across capabilities | 14 |

**Lab** — `ARC-002-LAB1` *Larkspur business architecture:* capability map with maturity heat map, two value streams (order-to-delivery, return-to-refund), and a stakeholder map. Acceptance: role-played business owners agree the heat map reflects their pain points.

**Common mistakes:** capability maps that are org charts; processes modeled in detail before the value stream is agreed.

**Assessment:** capability map defense.

**Workplace evidence:** a capability map or value-stream model used to scope a real initiative.

**Career relevance:** basis for requirements discovery (ARC-003) and solution options (ARC-033).

---

### ARC-003 · Requirements discovery
`n: 257` · **Video:** 93 min · **Practice:** 4 h

**Prerequisites:** SRC-001, ARC-002

**Learning outcomes** — the architect can:
1. Plan and facilitate discovery workshops and stakeholder interviews.
2. Capture functional requirements as use cases or user journeys and nonfunctional requirements as measurable quality scenarios.
3. Identify constraints (budget, regulation, existing systems, skills, timeline) and assumptions.
4. Resolve conflicting requirements by making trade-offs explicit and getting owners to decide.
5. Baseline requirements with traceability for change control.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| ARC-003-L01 | Discovery as the architect's first deliverable | 8 |
| ARC-003-L02 | Planning workshops and interviews | 12 |
| ARC-003-L03 | Facilitation techniques | 12 |
| ARC-003-L04 | Functional requirements and journeys | 10 |
| ARC-003-L05 | Nonfunctional requirements that can be tested | 12 |
| ARC-003-L06 | Constraints, assumptions, and conflicts | 10 |
| ARC-003-L07 | Demo: facilitating Larkspur's discovery workshop | 15 |
| ARC-003-L08 | Demo: resolving "real-time stock" vs "keep the ERP as master" | 14 |

**Lab** — `ARC-003-LAB1` *Larkspur requirements baseline:* run a role-played workshop with store operations, e-commerce, finance, IT, and security; produce the requirements baseline with quality scenarios, constraints, assumptions, and a traceability ID per requirement. Acceptance: every nonfunctional requirement is measurable; conflicts listed with a decision owner.

**Common mistakes:** gathering wish lists; letting the loudest stakeholder set priorities; untestable "must be secure and fast".

**Assessment:** workshop facilitation scored by role-players plus baseline review.

**Workplace evidence:** a requirements baseline you facilitated that was signed off by the business.

**Career relevance:** stakeholder management (ARC-041) and the ARC-CAP requirements section.

---

### ARC-004 · Architecture frameworks
`n: 258` · **Video:** 67 min · **Practice:** 2.5 h

**Prerequisites:** SRB-012, ARC-001

**Learning outcomes** — the architect can:
1. Explain the purpose and main concepts of TOGAF (ADM phases, architecture domains, building blocks, repository) without treating it as a checklist.
2. Use viewpoints and views (e.g., ISO/IEC/IEEE 42010 concepts) to address specific stakeholder concerns.
3. Describe how architecture governance and compliance reviews fit into an organization's delivery process.
4. Tailor a framework to the size and risk of a program.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| ARC-004-L01 | Why architecture frameworks exist | 8 |
| ARC-004-L02 | TOGAF concepts and the ADM | 14 |
| ARC-004-L03 | Architecture domains and building blocks | 10 |
| ARC-004-L04 | Viewpoints, views, and concerns | 12 |
| ARC-004-L05 | Governance and tailoring | 10 |
| ARC-004-L06 | Demo: tailoring a lightweight framework for the Larkspur program | 13 |

**Lab** — `ARC-004-LAB1` *Tailored method:* map the Larkspur engagement onto a tailored set of framework phases, the views each stakeholder needs, and the governance checkpoints. Acceptance: no artifact without a named consumer.

**Common mistakes:** producing every framework artifact; quoting framework vocabulary to business stakeholders.

**Assessment:** tailoring rationale review.

**Workplace evidence:** an architecture method you tailored for a real program.

**Career relevance:** architecture modeling (ARC-005) and review boards (ARC-035).

---

### ARC-005 · Architecture modeling
`n: 259` · **Video:** 66 min · **Practice:** 3.5 h

**Prerequisites:** MID-063, ARC-002

**Learning outcomes** — the architect can:
1. Choose the right notation for the audience: C4 for software structure, UML for behavior and detail, ArchiMate for business–application–technology layering.
2. Draw integration diagrams showing systems, interfaces, protocols, data flows, and ownership.
3. Draw deployment diagrams showing environments, networks, and trust boundaries.
4. Keep models consistent across views and maintained as code where practical.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| ARC-005-L01 | Models answer questions | 8 |
| ARC-005-L02 | C4 for solution architects | 10 |
| ARC-005-L03 | The useful parts of UML | 10 |
| ARC-005-L04 | ArchiMate introduction | 12 |
| ARC-005-L05 | Integration and deployment diagrams | 12 |
| ARC-005-L06 | Demo: one Larkspur model, three audiences | 14 |

**Lab** — `ARC-005-LAB1` *Larkspur current-state model:* system context, ArchiMate layered view of the current landscape (stores, web shop, ERP, CRM), and an integration diagram of today's interfaces. Acceptance: each diagram has a legend, an audience, and the question it answers.

**Common mistakes:** one diagram for everyone; boxes and arrows without labels or legends.

**Assessment:** model review.

**Workplace evidence:** architecture diagrams that business and engineering stakeholders both used.

**Career relevance:** architecture deliverables (ARC-034).

---

### ARC-006 · Solution architecture lifecycle
`n: 260` · **Video:** 64 min · **Practice:** 3 h

**Prerequisites:** ARC-003, ARC-004

**Learning outcomes** — the architect can:
1. Describe the solution architecture lifecycle: discovery, options, design, review, delivery support, transition, and handover.
2. Define the exit criteria and deliverables for each stage.
3. Support delivery teams during build without becoming a bottleneck (design authority, decision log, office hours).
4. Hand a solution over to operations and the owning teams.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| ARC-006-L01 | The lifecycle at a glance | 8 |
| ARC-006-L02 | Discovery and options | 10 |
| ARC-006-L03 | Design and review | 10 |
| ARC-006-L04 | Supporting delivery | 12 |
| ARC-006-L05 | Transition and handover | 10 |
| ARC-006-L06 | Demo: planning Larkspur's architecture lifecycle and checkpoints | 14 |

**Lab** — `ARC-006-LAB1` *Architecture plan:* the Larkspur architecture work plan with stages, deliverables, exit criteria, reviews, and the delivery-support model. Acceptance: aligned with the program plan; every review has a decision-maker.

**Common mistakes:** disappearing after the design is approved; designing the whole solution before any delivery feedback.

**Assessment:** plan review.

**Workplace evidence:** a solution you took from discovery through handover.

**Career relevance:** solution roadmaps (ARC-036) and architecture assurance (ARC-042).

---

### ARC-007 · Architecture principles
`n: 261` · **Video:** 56 min · **Practice:** 2.5 h

**Prerequisites:** SRA-012, ARC-004

**Learning outcomes** — the architect can:
1. Write architecture principles with statement, rationale, and implications.
2. Apply principles for standardization, interoperability, security, and evolvability to design decisions.
3. Resolve conflicts between principles explicitly.
4. Use principles to evaluate options and justify exceptions.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| ARC-007-L01 | What makes a principle useful | 10 |
| ARC-007-L02 | Statement, rationale, implications | 10 |
| ARC-007-L03 | Common principle sets | 12 |
| ARC-007-L04 | When principles conflict | 10 |
| ARC-007-L05 | Demo: drafting Larkspur's principles with the CIO | 14 |

**Lab** — `ARC-007-LAB1` *Larkspur principles:* eight to ten principles agreed with role-played IT leadership, each applied to one real Larkspur decision. Acceptance: at least one principle changes a decision; one conflict resolved on record.

**Common mistakes:** platitudes ("use best practices"); principles without implications.

**Assessment:** principles review.

**Workplace evidence:** principles you wrote that were cited in real design decisions.

**Career relevance:** review boards (ARC-035).

---

### ARC-008 · Technology assessment
`n: 262` · **Video:** 67 min · **Practice:** 3.5 h

**Prerequisites:** SRB-013, SRA-008

**Learning outcomes** — the architect can:
1. Decide build vs buy vs SaaS per capability using fit, differentiation, cost, risk, and time to market.
2. Evaluate vendors on functional fit, architecture fit (APIs, data, security, extensibility), viability, and exit cost.
3. Design a proof of concept that tests the riskiest integration and nonfunctional assumptions.
4. Present a recommendation with weighted criteria and sensitivity.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| ARC-008-L01 | Build, buy, or SaaS | 12 |
| ARC-008-L02 | Differentiating vs commodity capabilities | 10 |
| ARC-008-L03 | Evaluating vendors' architecture fit | 12 |
| ARC-008-L04 | Proofs of concept that reduce risk | 10 |
| ARC-008-L05 | Recommendation and sensitivity | 8 |
| ARC-008-L06 | Demo: commerce platform — build, packaged suite, or SaaS? | 15 |

**Lab** — `ARC-008-LAB1` *Commerce engine decision:* evaluate building on the in-house stack vs a packaged commerce suite vs a SaaS commerce platform for Larkspur, with weighted criteria and a PoC plan. Acceptance: exit cost and integration effort estimated for each option.

**Common mistakes:** feature checklists without architecture fit; ignoring data ownership and exit.

**Assessment:** recommendation defense.

**Workplace evidence:** a build/buy/SaaS recommendation you made and its outcome.

**Career relevance:** vendor and procurement (ARC-040) and financial analysis (ARC-039).

---

### ARC-009 · Enterprise integration
`n: 263` · **Video:** 87 min · **Practice:** 4 h

**Prerequisites:** SRB-002, SRB-007

**Learning outcomes** — the architect can:
1. Compare integration styles: synchronous APIs, events, ESB, iPaaS, batch, and file exchange.
2. Choose an integration style per interface from latency, volume, coupling, ownership, and the capabilities of the systems involved.
3. Design an integration landscape with canonical data where it helps and without it where it doesn't.
4. Plan error handling, monitoring, and ownership for each integration.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| ARC-009-L01 | Integration is where projects fail | 8 |
| ARC-009-L02 | APIs and events | 10 |
| ARC-009-L03 | ESB and iPaaS | 12 |
| ARC-009-L04 | Batch and file exchange still matter | 10 |
| ARC-009-L05 | Canonical models: when and when not | 10 |
| ARC-009-L06 | Operating integrations | 8 |
| ARC-009-L07 | Demo: Larkspur's integration landscape, interface by interface | 15 |
| ARC-009-L08 | Demo: the nightly ERP file that can't go away yet | 14 |

**Lab** — `ARC-009-LAB1` *Larkspur integration architecture:* interface catalog (systems, style, direction, volume, latency, owner, error handling) and target integration diagram covering ERP, CRM, payments, stores, and carriers. Acceptance: every interface justifies its style; failure handling defined.

**Common mistakes:** one style for everything; point-to-point sprawl without ownership; ignoring the ERP's real API limits.

**Assessment:** integration design review.

**Workplace evidence:** an integration architecture you designed across enterprise systems.

**Career relevance:** integration patterns and enterprise systems (ARC-024, ARC-032).

---

### ARC-010 · Legacy modernization
`n: 264` · **Video:** 83 min · **Practice:** 4 h

**Prerequisites:** SRB-008, ARC-009

**Learning outcomes** — the architect can:
1. Apply the modernization options — rehost, replatform, refactor, replace, retire (and retain) — per application.
2. Assess legacy applications by business value, technical condition, risk, and cost to change.
3. Sequence modernization to deliver value early and reduce risk (strangler, coexistence).
4. Build the business case for modernization.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| ARC-010-L01 | Why modernize, and why not | 8 |
| ARC-010-L02 | Rehost, replatform, refactor, replace, retire | 14 |
| ARC-010-L03 | Assessing an application portfolio | 12 |
| ARC-010-L04 | Sequencing and coexistence | 10 |
| ARC-010-L05 | The modernization business case | 10 |
| ARC-010-L06 | Demo: assessing Larkspur's application portfolio | 15 |
| ARC-010-L07 | Demo: replace the web shop, retain the ERP — the case | 14 |

**Lab** — `ARC-010-LAB1` *Portfolio disposition:* assess Larkspur's applications (web shop, store POS integration, order management in ERP, CRM, reporting) and assign a disposition and sequence to each. Acceptance: each decision justified by value, condition, and risk.

**Common mistakes:** rewriting everything; rehosting without addressing the reason for moving.

**Assessment:** disposition defense.

**Workplace evidence:** a modernization decision you led or shaped and its result.

**Career relevance:** migration strategy (ARC-037).
