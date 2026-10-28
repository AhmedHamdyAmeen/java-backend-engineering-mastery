# ARC-P4 — Solution Design, Governance, and Delivery

**Phase goal:** the architect turns everything designed so far into a decision-ready solution: comparing real options, producing the deliverables reviewers and delivery teams need, passing governance, planning a phased roadmap and migration, designing operations, making the financial case, running vendor selection, managing stakeholders, assuring the solution before go-live, and presenting it convincingly.

**Running case:** *Larkspur Retail* continues. This phase assembles the complete Solution Architect capstone package (`ARC-CAP`): options analysis, HLD and LLD, ADRs and risk register, roadmap and migration plan, cost and build-vs-buy, and the executive presentation and design defense.

**Format:** case studies, worked architecture sessions, governance and stakeholder role-play. Each module lists the workplace evidence that demonstrates the role.

**Phase total:** ~13.6 h video · ~44 h practice

---

### ARC-033 · Solution options
`n: 287` · **Video:** 71 min · **Practice:** 4 h

**Prerequisites:** SRC-003, ARC-006

**Learning outcomes** — the architect can:
1. Generate genuinely different solution options (e.g., commerce SaaS, packaged platform, custom build, hybrid).
2. Define evaluation criteria and weights with stakeholders before scoring.
3. Score options in a decision matrix and test the result's sensitivity to weights.
4. Recommend an option and record why the others were rejected.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| ARC-033-L01 | Why one option is no option | 10 |
| ARC-033-L02 | Generating real alternatives | 10 |
| ARC-033-L03 | Criteria and weights with stakeholders | 12 |
| ARC-033-L04 | Decision matrices and sensitivity | 12 |
| ARC-033-L05 | Demo: four options for Larkspur's commerce platform | 14 |
| ARC-033-L06 | Demo: when changing one weight flips the recommendation | 13 |

**Lab** — `ARC-033-LAB1` *Larkspur options analysis:* at least three options, weighted criteria agreed with role-played stakeholders, decision matrix with sensitivity analysis, and recommendation. Acceptance: rejected options documented with their honest strengths.

**Common mistakes:** strawman options; criteria chosen after the favorite; no sensitivity check.

**Assessment:** options defense with assessor challenges.

**Workplace evidence:** an options analysis you led that produced a decision.

**Career relevance:** options analysis is the heart of solution architecture.

---

### ARC-034 · Architecture deliverables
`n: 288` · **Video:** 71 min · **Practice:** 4 h

**Prerequisites:** ARC-005, ARC-033

**Learning outcomes** — the architect can:
1. Write a high-level design (HLD) that reviewers can approve and a low-level design (LLD) that teams can build from.
2. Write ADRs for significant decisions.
3. Specify interface contracts precisely enough for parallel delivery.
4. Produce deployment diagrams that operations teams can use.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| ARC-034-L01 | Deliverables and their readers | 10 |
| ARC-034-L02 | The high-level design | 12 |
| ARC-034-L03 | The low-level design | 12 |
| ARC-034-L04 | Interface contracts and deployment diagrams | 10 |
| ARC-034-L05 | Demo: writing Larkspur's HLD section by section | 14 |
| ARC-034-L06 | Demo: turning an HLD component into an LLD a team can build | 13 |

**Lab** — `ARC-034-LAB1` *Larkspur HLD and LLD:* HLD for the platform, LLD for order fulfillment, ADRs for the five biggest decisions, interface contracts for ERP and payments, and a deployment diagram. Acceptance: a role-played delivery lead can estimate from the LLD without asking for clarifications on scope.

**Common mistakes:** HLDs full of implementation detail; LLDs missing error and edge cases; ADRs written after the fact.

**Assessment:** deliverable review against a checklist.

**Workplace evidence:** an HLD or LLD you wrote that a team delivered from.

**Career relevance:** deliverables are how architects' decisions reach delivery teams.

---

### ARC-035 · Architecture review boards
`n: 289` · **Video:** 56 min · **Practice:** 2.5 h

**Prerequisites:** ARC-007, ARC-034

**Learning outcomes** — the architect can:
1. Prepare a solution for an architecture review board (ARB) submission.
2. Demonstrate compliance with architecture principles and standards.
3. Request and justify design exceptions with mitigations and expiry dates.
4. Act on ARB conditions and track them to closure.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| ARC-035-L01 | What review boards are for | 10 |
| ARC-035-L02 | Preparing a submission | 12 |
| ARC-035-L03 | Compliance checks | 10 |
| ARC-035-L04 | Exceptions and conditions | 10 |
| ARC-035-L05 | Demo: a Larkspur ARB session with conditions | 14 |

**Lab** — `ARC-035-LAB1` *ARB submission:* submit the Larkspur solution to a role-played ARB, including one exception request; respond to the conditions raised. Acceptance: approval or conditional approval with a closure plan.

**Common mistakes:** surprising the board; exceptions without expiry; ignoring conditions after approval.

**Assessment:** ARB simulation.

**Workplace evidence:** a solution you took through formal architecture governance.

**Career relevance:** governance is a routine part of enterprise architecture work.

---

### ARC-036 · Solution roadmaps
`n: 290` · **Video:** 56 min · **Practice:** 3 h

**Prerequisites:** SRA-002, ARC-033

**Learning outcomes** — the architect can:
1. Break a solution into phases that each deliver business value.
2. Map dependencies (technical, organizational, vendor, contractual) between phases.
3. Define milestones with measurable exit criteria.
4. Keep the roadmap current as delivery and priorities change.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| ARC-036-L01 | Roadmaps that deliver value early | 10 |
| ARC-036-L02 | Phasing a solution | 12 |
| ARC-036-L03 | Dependency mapping | 10 |
| ARC-036-L04 | Milestones and exit criteria | 10 |
| ARC-036-L05 | Demo: Larkspur's 18-month roadmap, phase by phase | 14 |

**Lab** — `ARC-036-LAB1` *Larkspur roadmap:* phased 18-month roadmap with dependencies, milestones, exit criteria, and the first release scoped. Acceptance: phase one delivers measurable business value on its own.

**Common mistakes:** roadmaps where value arrives only at the end; dependencies on vendors left implicit.

**Assessment:** roadmap review.

**Workplace evidence:** a solution roadmap you built that delivery followed.

**Career relevance:** roadmaps connect architecture to delivery plans and budgets.

---

### ARC-037 · Migration strategy
`n: 291` · **Video:** 71 min · **Practice:** 4 h

**Prerequisites:** SRB-017, ARC-010

**Learning outcomes** — the architect can:
1. Choose a cutover approach (big bang, phased by capability, phased by store or region, parallel run) and justify it.
2. Design coexistence between old and new systems during migration.
3. Plan data migration: mapping, cleansing, trial loads, validation, and final load.
4. Define rollback plans and go/no-go criteria for each cutover.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| ARC-037-L01 | Cutover approaches | 12 |
| ARC-037-L02 | Coexistence of old and new | 10 |
| ARC-037-L03 | Data migration | 12 |
| ARC-037-L04 | Rollback and go/no-go | 10 |
| ARC-037-L05 | Demo: migrating Larkspur's customers and orders from the old web shop | 14 |
| ARC-037-L06 | Demo: a pilot-store rollout and its rollback plan | 13 |

**Lab** — `ARC-037-LAB1` *Larkspur migration plan:* cutover strategy, coexistence design, data migration plan with trial loads and validation, and rollback criteria. Acceptance: every cutover step has a rollback and a decision owner.

**Common mistakes:** one untested final data load; no coexistence plan; rollback that ignores data written after cutover.

**Assessment:** migration plan defense.

**Workplace evidence:** a migration or cutover you planned and executed.

**Career relevance:** most enterprise solutions replace something that is already running.

---

### ARC-038 · Operational architecture
`n: 292` · **Video:** 58 min · **Practice:** 3 h

**Prerequisites:** SRC-011, ARC-036

**Learning outcomes** — the architect can:
1. Design monitoring, alerting, and logging for a solution that spans owned, SaaS, and on-premises components.
2. Define support models (tiers, hours, escalation) and service ownership.
3. Align incident and change processes between the organization and its vendors.
4. Specify operational acceptance criteria for handover to operations.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| ARC-038-L01 | Designing for operations | 10 |
| ARC-038-L02 | Monitoring a mixed estate | 12 |
| ARC-038-L03 | Support models and service ownership | 12 |
| ARC-038-L04 | Incident and change processes with vendors | 10 |
| ARC-038-L05 | Demo: Larkspur's operating model on a single page | 14 |

**Lab** — `ARC-038-LAB1` *Larkspur operations:* monitoring design, support model, ownership map, vendor escalation paths, and operational acceptance criteria. Acceptance: reviewed by a role-played head of IT operations.

**Common mistakes:** operations designed after go-live; SaaS components with no monitoring; no owner for integrations.

**Assessment:** operating model review.

**Workplace evidence:** an operating or support model you designed for a solution.

**Career relevance:** operations is where solution designs are tested every day.

---

### ARC-039 · Financial analysis
`n: 293` · **Video:** 69 min · **Practice:** 4 h

**Prerequisites:** SRA-008, ARC-021

**Learning outcomes** — the architect can:
1. Build a total cost of ownership model (build, run, licences, support, people) over several years.
2. Estimate ROI and payback with the business, keeping assumptions explicit.
3. Compare capital and operating expenditure profiles of options.
4. Present a cost-benefit analysis that finance can verify.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| ARC-039-L01 | Finance for architects | 10 |
| ARC-039-L02 | Total cost of ownership | 12 |
| ARC-039-L03 | ROI, payback, and benefits | 10 |
| ARC-039-L04 | Licensing and operating costs | 10 |
| ARC-039-L05 | Demo: a five-year TCO for Larkspur's options | 14 |
| ARC-039-L06 | Demo: a finance review of the business case | 13 |

**Lab** — `ARC-039-LAB1` *Larkspur business case:* five-year TCO for the top two options, benefits with owners, ROI and payback, and sensitivity to key assumptions. Acceptance: a role-played finance partner can reproduce every number.

**Common mistakes:** licence cost compared with zero; benefits nobody owns; hiding assumptions.

**Assessment:** business case review.

**Workplace evidence:** a cost model or business case you produced that was used in a funding decision.

**Career relevance:** solutions are funded on their financial case.

---

### ARC-040 · Vendor and procurement
`n: 294` · **Video:** 58 min · **Practice:** 3 h

**Prerequisites:** ARC-008, ARC-039

**Learning outcomes** — the architect can:
1. Write the technical sections of an RFI and an RFP.
2. Design a technical evaluation (requirements coverage, demos, proof of concept, references).
3. Review SLAs and contract terms for architectural risk (exit, data ownership, availability, support).
4. Work with procurement and legal as a technical advisor.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| ARC-040-L01 | The procurement process | 10 |
| ARC-040-L02 | RFIs and RFPs | 12 |
| ARC-040-L03 | Technical evaluation | 12 |
| ARC-040-L04 | SLAs and contracts from an architect's view | 10 |
| ARC-040-L05 | Demo: scoring two vendor RFP responses | 14 |

**Lab** — `ARC-040-LAB1` *Commerce platform RFP:* technical RFP sections for Larkspur's commerce platform, an evaluation scorecard, and an SLA and exit-clause review of a provided sample contract. Acceptance: scorecard traceable to requirements; exit risks identified.

**Common mistakes:** RFPs that describe a product instead of needs; ignoring exit and data-return terms.

**Assessment:** RFP and evaluation review.

**Workplace evidence:** a vendor evaluation you ran or contributed to.

**Career relevance:** buy decisions are frequent in enterprise solutions.

---

### ARC-047 · AI vendor and model evaluation
`n: new (added in v2.0)` · **Video:** 70 min · **Practice:** 3.5 h

**Prerequisites:** ARC-040, ARC-045

**Learning outcomes** — the architect can:
1. Define evaluation criteria for AI vendors and models: quality on your own tasks, latency, cost, data terms, security, support, and exit.
2. Explain why public benchmarks are not enough and build a task-specific evaluation set.
3. Run a time-boxed AI proof of concept that answers the riskiest questions.
4. Compare total cost over several years, including usage growth and switching costs.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| ARC-047-L01 | Evaluating AI vendors and models | 12 |
| ARC-047-L02 | Benchmarks vs your own evaluations | 12 |
| ARC-047-L03 | AI proofs of concept | 10 |
| ARC-047-L04 | Multi-year AI cost and exit planning | 10 |
| ARC-047-L05 | Demo: scoring three AI vendors for Larkspur | 14 |
| ARC-047-L06 | Demo: building a 50-question evaluation set from support tickets | 12 |

**Lab** — `ARC-047-LAB1` *AI vendor choice:* evaluate three candidate approaches for the Larkspur assistant (two hosted providers and one self-hosted open-weight model) with a task-specific evaluation set, cost model, and terms review. Acceptance: recommendation with evaluation scores, three-year cost, and exit plan.

**Common mistakes:** choosing on public leaderboard rank; PoCs on toy questions; ignoring data terms until contracting.

**Assessment:** evaluation report review.

**Workplace evidence:** an AI vendor or model evaluation you ran and its outcome.

**Career relevance:** vendor and procurement work in every AI-enabled solution.

---

### ARC-041 · Stakeholder management
`n: 295` · **Video:** 56 min · **Practice:** 3 h

**Prerequisites:** SRA-015, ARC-003

**Learning outcomes** — the architect can:
1. Map stakeholders (business, engineering, security, operations, vendors) by influence and interest.
2. Tailor engagement and communication to each group.
3. Resolve conflicting requirements with explicit trade-offs and decision owners.
4. Keep stakeholders aligned through the solution lifecycle.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| ARC-041-L01 | Stakeholder mapping | 10 |
| ARC-041-L02 | Engagement plans | 10 |
| ARC-041-L03 | Resolving conflicting requirements | 12 |
| ARC-041-L04 | Keeping alignment over time | 10 |
| ARC-041-L05 | Demo: mediating between store operations and e-commerce | 14 |

**Lab** — `ARC-041-LAB1` *Larkspur stakeholders:* stakeholder map, engagement plan, and a recorded session resolving a conflict between e-commerce (speed) and security (controls). Acceptance: conflict resolved with a documented trade-off and decision owner.

**Common mistakes:** engaging only with the sponsor; avoiding conflicts until they block delivery.

**Assessment:** stakeholder simulation.

**Workplace evidence:** a stakeholder conflict you resolved on a real solution.

**Career relevance:** architects spend much of their time aligning people.

---

### ARC-042 · Architecture assurance
`n: 296` · **Video:** 58 min · **Practice:** 3 h

**Prerequisites:** SRC-011, ARC-035

**Learning outcomes** — the architect can:
1. Run design reviews during delivery to catch drift from the approved architecture.
2. Define the testing evidence needed for non-functional requirements (performance, security, resilience).
3. Specify and verify operational acceptance before go-live.
4. Decide go-live readiness from evidence.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| ARC-042-L01 | Assurance during delivery | 10 |
| ARC-042-L02 | Architecture drift | 10 |
| ARC-042-L03 | Non-functional testing evidence | 12 |
| ARC-042-L04 | Operational acceptance and go-live readiness | 12 |
| ARC-042-L05 | Demo: finding drift in a delivery team's design | 14 |

**Lab** — `ARC-042-LAB1` *Larkspur assurance plan:* assurance checkpoints, required NFR evidence per requirement, and an operational acceptance checklist; assess a provided set of test results for go-live. Acceptance: go/no-go recommendation traceable to evidence.

**Common mistakes:** assurance that ends at design approval; go-live without NFR evidence.

**Assessment:** go/no-go decision review.

**Workplace evidence:** an assurance review or go-live decision you led.

**Career relevance:** assurance protects the business after the design is approved.

---

### ARC-043 · Solution documentation
`n: 297` · **Video:** 54 min · **Practice:** 3 h

**Prerequisites:** ARC-034

**Learning outcomes** — the architect can:
1. Assemble an architecture pack that serves executives, reviewers, delivery, and operations.
2. Maintain a decision log, assumptions log, and risk register.
3. Keep documentation current through delivery with clear ownership.
4. Hand over documentation to operations and future architects.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| ARC-043-L01 | The architecture pack | 10 |
| ARC-043-L02 | Decision and assumption logs | 10 |
| ARC-043-L03 | Risk registers | 10 |
| ARC-043-L04 | Keeping documentation alive | 10 |
| ARC-043-L05 | Demo: assembling Larkspur's architecture pack | 14 |

**Lab** — `ARC-043-LAB1` *Larkspur architecture pack:* the complete pack with decision log, assumptions, and risk register, structured by audience. Acceptance: a role-played new architect answers ten questions using the pack alone.

**Common mistakes:** one document for every audience; risk registers without owners or dates.

**Assessment:** pack review.

**Workplace evidence:** an architecture pack you maintained through delivery.

**Career relevance:** documentation is the lasting record of an architect's decisions.

---

### ARC-044 · Architecture communication
`n: 298` · **Video:** 70 min · **Practice:** 4 h

**Prerequisites:** SRA-019, ARC-043

**Learning outcomes** — the architect can:
1. Present a solution to executives in business terms with a clear ask.
2. Present the same solution to engineering teams with the technical depth they need.
3. Defend a design under challenge, separating facts, assumptions, and trade-offs.
4. Use diagrams and narratives that fit each audience.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| ARC-044-L01 | One solution, many audiences | 10 |
| ARC-044-L02 | Presenting to executives | 12 |
| ARC-044-L03 | Presenting to engineering teams | 10 |
| ARC-044-L04 | Defending a design | 10 |
| ARC-044-L05 | Demo: Larkspur's ten-minute executive presentation | 14 |
| ARC-044-L06 | Demo: a hostile technical design defense, handled | 14 |

**Lab** — `ARC-044-LAB1` *Present Larkspur:* a ten-minute executive presentation and a 30-minute technical design defense to role-played panels. Acceptance: executives can state the decision asked of them; the engineering panel's challenges are answered with evidence or recorded as follow-ups.

**Common mistakes:** technical detail for executives; claiming certainty you do not have.

**Assessment:** presentation and defense scored on the COM dimension.

**Workplace evidence:** a solution presentation that secured approval or funding.

**Career relevance:** the final step of every solution — and of this curriculum.

---

## Solution Architect capstone — Enterprise Digital Commerce Platform (`ARC-CAP`)

Full brief, acceptance criteria, and graduation gate: [`projects/ladder.md`](../../projects/ladder.md#08--enterprise-digital-commerce-platform-arc-cap).
