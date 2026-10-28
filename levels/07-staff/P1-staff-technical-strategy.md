# STF-P1 — Staff-Level Technical Strategy

**Phase goal:** the engineer understands what a Staff engineer is for, finds the problems that matter across a whole engineering organization, and sets strategy, governance, platform direction, reliability and security programs, and technology choices that make many teams more effective at once.

**Running case:** *Platform 2.0.* The Commerce group from Levels 5–6 (Shop + FulfillCo) now has about 20 product teams. Delivery has slowed, every team runs its own pipelines and tooling, the same incidents repeat across teams, and onboarding a new engineer takes weeks. The engineer joins as a Staff engineer with no team of their own and a mandate to make the whole organization faster and safer. Every lab feeds the Staff capstone (`STF-CAP`).

**Format:** case studies, worked strategy sessions, and organizational role-play, with two worked sessions per module. Assessment weighs organizational leverage, not code. Each module lists the workplace evidence that demonstrates the role.

**Phase total:** ~17.5 h video · ~42 h practice

---

### STF-001 · Staff engineering role
`n: 235` · **Video:** 100 min · **Practice:** 3 h

**Prerequisites:** SRA-014, SRA-020

**Learning outcomes** — the engineer can:
1. Explain how Staff scope differs from Senior scope: problems chosen, time horizon, and leverage over many teams.
2. Describe common Staff archetypes (tech lead, architect, solver, right hand) and identify which one an organization needs.
3. Distinguish the Staff role from engineering management and agree boundaries with managers.
4. Choose work by leverage: what changes outcomes for many teams per unit of effort.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| STF-001-L01 | What organizations hire Staff engineers to do | 12 |
| STF-001-L02 | Scope, time horizon, and leverage | 12 |
| STF-001-L03 | Staff archetypes | 12 |
| STF-001-L04 | Staff engineers and managers: a partnership | 12 |
| STF-001-L05 | Choosing work by leverage | 12 |
| STF-001-L06 | Staying technical without a team | 10 |
| STF-001-L07 | Demo: the first 90 days in Platform 2.0 | 15 |
| STF-001-L08 | Demo: saying no to a high-visibility, low-leverage request | 15 |

**Lab** — `STF-001-LAB1` *First 90 days:* interview role-played managers, tech leads, and product partners; produce a 90-day plan with the archetype the organization needs and three candidate problems ranked by leverage. Acceptance: each candidate problem names the teams affected and how impact would be measured.

**Common mistakes:** acting as a super-senior on one team; collecting projects instead of choosing them; competing with managers for ownership.

**Assessment:** 90-day plan defense with a role-played VP of Engineering.

**Workplace evidence:** a piece of work you chose because of its leverage across teams, and the result.

**Career relevance:** frames every other Staff module; the Staff career path (STF-020).

---

### STF-002 · Technical strategy
`n: 236` · **Video:** 100 min · **Practice:** 4.5 h

**Prerequisites:** SRA-010, STF-001

**Learning outcomes** — the engineer can:
1. Connect business priorities (growth, margin, risk, speed) to engineering investment explicitly.
2. Write an organization-wide technical strategy from evidence: data on delivery, incidents, cost, and engineer experience.
3. Make trade-offs visible: what the organization will stop doing to fund the strategy.
4. Get a strategy endorsed by engineering and business leadership and keep it current.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| STF-002-L01 | Strategy at organization scale | 12 |
| STF-002-L02 | From business priorities to engineering bets | 14 |
| STF-002-L03 | Gathering evidence across 20 teams | 12 |
| STF-002-L04 | Writing the diagnosis | 12 |
| STF-002-L05 | What we will stop doing | 10 |
| STF-002-L06 | Endorsement and refresh cycles | 10 |
| STF-002-L07 | Demo: diagnosing Platform 2.0 from delivery and incident data | 15 |
| STF-002-L08 | Demo: turning three business goals into two engineering bets | 15 |

**Lab** — `STF-002-LAB1` *Platform 2.0 strategy:* an evidence-based technical strategy for the organization (diagnosis, guiding policies, actions, explicit trade-offs) presented to role-played CTO and CPO. Acceptance: every action traces to evidence and a business priority; at least one thing is explicitly stopped.

**Common mistakes:** strategy written from opinion; no trade-offs; a strategy owned by one person that nobody else can explain.

**Assessment:** strategy defense.

**Workplace evidence:** an organization-wide strategy you authored or shaped that leadership adopted.

**Career relevance:** executive communication (STF-017) and solution roadmaps (ARC-036).

---

### STF-003 · Architecture governance at scale
`n: 237` · **Video:** 98 min · **Practice:** 3.5 h

**Prerequisites:** SRB-012, SRA-012

**Learning outcomes** — the engineer can:
1. Write architecture principles that resolve real disagreements.
2. Publish reference architectures that teams start from rather than reinvent.
3. Define decision rights: which decisions belong to teams, domains, and the organization.
4. Design governance that scales with 20 teams without becoming a bottleneck, and measure its cost.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| STF-003-L01 | Governance as an enabling system | 12 |
| STF-003-L02 | Principles that decide things | 12 |
| STF-003-L03 | Reference architectures | 12 |
| STF-003-L04 | Decision rights | 12 |
| STF-003-L05 | Measuring the cost of governance | 10 |
| STF-003-L06 | Evolving governance as the organization grows | 10 |
| STF-003-L07 | Demo: writing a decision-rights matrix with engineering managers | 15 |
| STF-003-L08 | Demo: a reference architecture for event-driven services | 15 |

**Lab** — `STF-003-LAB1` *Governance model:* principles, two reference architectures, and a decision-rights matrix for Platform 2.0, with a target for review turnaround. Acceptance: a role-played team lead can tell, for five sample decisions, who decides and how fast.

**Common mistakes:** a central board that reviews everything; principles too vague to apply; rules with no owner.

**Assessment:** governance model review.

**Workplace evidence:** a governance mechanism you designed that sped up or improved decisions.

**Career relevance:** architecture review boards and principles (ARC-035, ARC-007).

---

### STF-004 · Platform strategy
`n: 238` · **Video:** 100 min · **Practice:** 4.5 h

**Prerequisites:** SRB-010, STF-002

**Learning outcomes** — the engineer can:
1. Decide what the internal platform should and should not provide, using developer journeys and toil data.
2. Design paved roads that are the easiest path, with escape hatches for teams with real needs.
3. Plan a platform as a product: users, roadmap, support model, and success measures.
4. Size and staff a platform team and justify the investment.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| STF-004-L01 | Why internal platforms succeed or fail | 12 |
| STF-004-L02 | Developer journeys and toil mapping | 12 |
| STF-004-L03 | Paved roads and escape hatches | 12 |
| STF-004-L04 | The platform as a product | 12 |
| STF-004-L05 | Build, assemble, or buy platform capabilities | 12 |
| STF-004-L06 | Funding and staffing a platform team | 10 |
| STF-004-L07 | Demo: mapping the "new service to production" journey across five teams | 15 |
| STF-004-L08 | Demo: choosing the platform's first three capabilities | 15 |

**Lab** — `STF-004-LAB1` *Platform 2.0 platform strategy:* developer-journey map, platform scope (in and out), capability roadmap, and team/budget proposal. Acceptance: each capability is backed by toil or delay data from at least three teams.

**Common mistakes:** building what the platform team finds interesting; mandatory platforms nobody wants; no product management for the platform.

**Assessment:** platform strategy defense.

**Workplace evidence:** a platform capability you shaped and its adoption numbers.

**Career relevance:** the core of `STF-CAP`; compute choices for architects (ARC-014).

---

### STF-005 · Organization-wide reliability
`n: 239` · **Video:** 96 min · **Practice:** 4 h

**Prerequisites:** SRC-012, SRA-006

**Learning outcomes** — the engineer can:
1. Find systemic reliability risks from incident patterns across teams.
2. Run a reliability program: SLO coverage, postmortem quality, action-item follow-through, on-call health.
3. Assess operational maturity of teams and target help where it matters most.
4. Report reliability to leadership as business risk with trends.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| STF-005-L01 | Reliability as an organizational property | 12 |
| STF-005-L02 | Mining incidents for systemic causes | 12 |
| STF-005-L03 | Designing a reliability program | 12 |
| STF-005-L04 | Operational maturity models | 10 |
| STF-005-L05 | On-call health | 10 |
| STF-005-L06 | Reporting reliability to leadership | 10 |
| STF-005-L07 | Demo: finding the cause behind 30 incidents in 12 teams | 15 |
| STF-005-L08 | Demo: a quarterly reliability review with the CTO | 15 |

**Lab** — `STF-005-LAB1` *Reliability program:* analyze a year of Platform 2.0 incident reports, identify three systemic causes, and design a reliability program with targets. Acceptance: program targets are measurable and tied to the systemic causes.

**Common mistakes:** fixing incidents one by one; postmortem actions that are never done; equating reliability with uptime alone.

**Assessment:** program review.

**Workplace evidence:** a reliability program or systemic fix that reduced repeat incidents across teams.

**Career relevance:** crisis leadership (STF-018) and resilience architecture (ARC-031).

---

### STF-006 · Cross-domain systems
`n: 240` · **Video:** 90 min · **Practice:** 4 h

**Prerequisites:** SRA-003, SRA-004

**Learning outcomes** — the engineer can:
1. Identify cross-domain capabilities (identity, billing, commerce core, data, integration) and the coupling they create.
2. Decide which cross-domain systems should be shared platforms and which should stay in domains.
3. Design ownership and funding models for shared systems.
4. Lead the evolution of a shared system without stalling its consumers.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| STF-006-L01 | Systems everyone depends on | 12 |
| STF-006-L02 | Identity, billing, and data as cross-domain capabilities | 14 |
| STF-006-L03 | Shared platform or domain-owned? | 12 |
| STF-006-L04 | Ownership and funding of shared systems | 10 |
| STF-006-L05 | Evolving a shared system safely | 12 |
| STF-006-L06 | Demo: untangling three competing customer-identity systems | 15 |
| STF-006-L07 | Demo: a funding model for the shared integration platform | 15 |

**Lab** — `STF-006-LAB1` *Cross-domain map:* map Platform 2.0's cross-domain systems, recommend ownership for each, and plan the consolidation of one duplicated capability. Acceptance: consolidation plan keeps every consumer working at each step.

**Common mistakes:** "shared" systems with no owner; consolidating by decree; ignoring the consumers' roadmaps.

**Assessment:** recommendation defense.

**Workplace evidence:** a cross-domain system whose ownership or design you changed.

**Career relevance:** enterprise systems integration (ARC-032) and identity architecture (ARC-017).

---

### STF-007 · Technology portfolio
`n: 241` · **Video:** 88 min · **Practice:** 3.5 h

**Prerequisites:** SRB-013, SRA-002

**Learning outcomes** — the engineer can:
1. Build a technology radar for the organization (adopt, trial, assess, hold) with clear criteria.
2. Decide when to standardize, consolidate, or allow diversity.
3. Run a technology retirement with migration support and deadlines.
4. Balance innovation with operational cost and skills.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| STF-007-L01 | Technology choices as a portfolio | 12 |
| STF-007-L02 | A technology radar that people use | 12 |
| STF-007-L03 | Standardize, consolidate, or diversify | 12 |
| STF-007-L04 | Introducing new technology safely | 10 |
| STF-007-L05 | Retiring technology | 12 |
| STF-007-L06 | Demo: building the first Platform 2.0 technology radar | 15 |
| STF-007-L07 | Demo: retiring a second message broker across eight teams | 15 |

**Lab** — `STF-007-LAB1` *Portfolio review:* inventory Platform 2.0's languages, frameworks, datastores, and CI tools; publish a radar; plan one retirement. Acceptance: radar entries have criteria and owners; retirement plan has a migration path and support offer.

**Common mistakes:** radars that reflect personal taste; retirements announced without help; never trialing anything new.

**Assessment:** radar and retirement plan review.

**Workplace evidence:** a technology standardization or retirement you led.

**Career relevance:** technology assessment (ARC-008) and legacy modernization (ARC-010).

---

### STF-008 · Security architecture strategy
`n: 242` · **Video:** 98 min · **Practice:** 3.5 h

**Prerequisites:** SRB-016, SRA-009

**Learning outcomes** — the engineer can:
1. Assess the organization's threat landscape and map it to architectural controls.
2. Define organization-wide trust boundaries and identity strategy for people, services, and partners.
3. Build secure defaults into the platform so teams are secure without extra effort.
4. Partner with the security team on a multi-year roadmap.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| STF-008-L01 | Security strategy vs security reviews | 10 |
| STF-008-L02 | Threat landscape for a commerce organization | 12 |
| STF-008-L03 | Organization-wide trust boundaries | 12 |
| STF-008-L04 | Secure defaults in the platform | 14 |
| STF-008-L05 | Supply-chain security at scale | 10 |
| STF-008-L06 | A joint roadmap with security | 10 |
| STF-008-L07 | Demo: turning five recurring audit findings into platform defaults | 15 |
| STF-008-L08 | Demo: a trust-boundary map for the whole organization | 15 |

**Lab** — `STF-008-LAB1` *Secure by default:* security architecture strategy for Platform 2.0 with five secure defaults built into the golden path and a joint roadmap with a role-played CISO. Acceptance: each default removes a class of findings rather than one finding.

**Common mistakes:** strategy as a list of tools; security work pushed onto every team individually.

**Assessment:** strategy review with the CISO role-player.

**Workplace evidence:** a secure default you introduced at organization level and the findings it eliminated.

**Career relevance:** security architecture (ARC-028).

---

### STF-009 · Engineering productivity
`n: 243` · **Video:** 98 min · **Practice:** 4 h

**Prerequisites:** SRB-014, STF-004

**Learning outcomes** — the engineer can:
1. Measure developer productivity with balanced indicators (delivery metrics, developer experience surveys, cognitive load) without ranking people.
2. Find the biggest feedback-loop delays (build, test, review, deploy, onboarding).
3. Improve build pipelines and developer tooling where the gains compound across teams.
4. Justify productivity investments in time saved and delivery outcomes.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| STF-009-L01 | What productivity means for engineers | 12 |
| STF-009-L02 | Measuring without surveillance | 12 |
| STF-009-L03 | Feedback loops: where time goes | 12 |
| STF-009-L04 | Build and test pipelines at scale | 12 |
| STF-009-L05 | Onboarding as a product | 10 |
| STF-009-L06 | Making the business case | 10 |
| STF-009-L07 | Demo: cutting a 40-minute CI pipeline to 8 minutes | 15 |
| STF-009-L08 | Demo: running a developer-experience survey and acting on it | 15 |

**Lab** — `STF-009-LAB1` *Productivity baseline:* measure Platform 2.0's feedback loops and developer experience, pick the top two improvements, and estimate engineer-hours saved per month. Acceptance: baseline recorded so the improvement can be measured in the capstone.

**Common mistakes:** lines of code or story points as productivity; optimizing one team's pipeline when the bottleneck is shared.

**Assessment:** baseline and business-case review.

**Workplace evidence:** a productivity improvement you led with before/after data.

**Career relevance:** success metrics in `STF-CAP`; measuring impact (STF-019).

---

### STF-021 · AI governance and engineering productivity
`n: new (added in v2.0)` · **Video:** 88 min · **Practice:** 4 h

**Prerequisites:** SRB-022, STF-009

**Learning outcomes** — the engineer can:
1. Define organization-wide AI governance: approved tools, usage policy, data rules, and decision rights.
2. Set evaluation and quality standards for AI features and AI-generated code that teams can meet without a central bottleneck.
3. Build guardrails into the platform (gateway, scanning, review rules) instead of relying on policy documents.
4. Measure the effect of AI on engineering productivity and quality honestly across ~20 teams.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| STF-021-L01 | Why AI needs governance, not prohibition | 10 |
| STF-021-L02 | Approved tools, data rules, and decision rights | 12 |
| STF-021-L03 | Evaluation and quality standards | 12 |
| STF-021-L04 | Guardrails as paved roads | 12 |
| STF-021-L05 | Measuring AI's effect on engineering | 12 |
| STF-021-L06 | Demo: turning an AI policy into platform guardrails | 15 |
| STF-021-L07 | Demo: an org-wide AI productivity report with honest caveats | 15 |

**Lab** — `STF-021-LAB1` *AI governance for Platform 2.0:* governance model, approved-tool list, data rules, evaluation standard for AI features, platform guardrails, and a measurement plan across the ~20 product teams. Acceptance: every rule has an enforcement point or an explicit owner; measurement plan has baselines and quality counter-metrics.

**Common mistakes:** banning tools and pushing usage underground; governance boards that review every prompt; productivity claims without baselines.

**Assessment:** governance proposal review.

**Workplace evidence:** AI governance or guardrails you established across several teams.

**Career relevance:** leading AI adoption (STF-022) and AI vendor evaluation (ARC-047).

---

### STF-010 · Technical due diligence
`n: 244` · **Video:** 96 min · **Practice:** 3.5 h

**Prerequisites:** SRA-008, STF-007

**Learning outcomes** — the engineer can:
1. Assess an unfamiliar organization's architecture, code health, operations, security, and team capability quickly.
2. Separate deal-breaking risks from fixable debt and estimate remediation cost.
3. Produce a due-diligence report for acquisitions, vendor selection, or internal modernization.
4. Recommend a modernization plan sized to the findings.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| STF-010-L01 | When due diligence is needed | 10 |
| STF-010-L02 | Assessing architecture and code health | 12 |
| STF-010-L03 | Assessing operations and security | 12 |
| STF-010-L04 | Assessing team capability and key-person risk | 12 |
| STF-010-L05 | Risk severity and remediation cost | 10 |
| STF-010-L06 | Writing the report | 10 |
| STF-010-L07 | Demo: a two-week due diligence of an acquisition target | 15 |
| STF-010-L08 | Demo: presenting findings to a deal team | 15 |

**Lab** — `STF-010-LAB1` *Acquisition review:* the group wants to acquire a payments start-up; assess its provided architecture docs, repository sample, incident history, and team interviews; write the report with a go/no-go recommendation. Acceptance: top risks costed; recommendation stated with conditions.

**Common mistakes:** judging style instead of risk; missing people risks; findings without cost estimates.

**Assessment:** report and presentation to role-played deal team.

**Workplace evidence:** an assessment you produced that informed an acquisition, vendor, or modernization decision.

**Career relevance:** vendor evaluation (ARC-040) and legacy modernization (ARC-010).
