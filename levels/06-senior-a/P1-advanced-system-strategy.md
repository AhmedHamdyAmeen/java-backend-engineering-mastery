# SRA-P1 — Advanced System Strategy

**Phase goal:** the engineer reasons about architecture at the scale of a whole product area over years: how organizations and platforms shape systems, how to keep architecture evolvable, how to own data and domains across many teams, how to manage systemic risk, cost, and compliance, and how to turn all of it into a technical strategy.

**Running case:** *Commerce 2030.* The group formed by Shop and FulfillCo now has 25 engineering teams. Over three years it plans to launch a third-party seller marketplace, expand to five countries, and double order volume each year, while its earliest services approach end of life. The engineer is the senior technical leader for the commerce product area and must shape its three-year architecture evolution. Every lab contributes to the Senior A capstone (`SRA-CAP`).

**Format:** case studies, worked strategy sessions, and leadership role-play, with two worked sessions per module. Each module lists the workplace evidence that demonstrates the role.

**Phase total:** ~14.3 h video · ~37 h practice

---

### SRA-001 · Architecture at scale
`n: 215` · **Video:** 86 min · **Practice:** 4 h

**Prerequisites:** SRB-010, SRB-012

**Learning outcomes** — the engineer can:
1. Describe an organization's architecture as platforms, product domains, and shared capabilities, and explain how each evolves.
2. Draw platform boundaries that reduce coordination between product teams.
3. Apply evolutionary architecture principles (incremental change, guided by fitness functions, last responsible moment).
4. Identify where architecture and organization are misaligned.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRA-001-L01 | From system architecture to organizational architecture | 12 |
| SRA-001-L02 | Platforms, domains, and shared capabilities | 12 |
| SRA-001-L03 | Drawing platform boundaries | 10 |
| SRA-001-L04 | Evolutionary architecture | 12 |
| SRA-001-L05 | Reading misalignment between teams and systems | 10 |
| SRA-001-L06 | Demo: mapping the Commerce 2030 landscape | 15 |
| SRA-001-L07 | Demo: moving one capability from product teams into a platform | 15 |

**Lab** — `SRA-001-LAB1` *Landscape map:* map Commerce 2030's current systems, teams, platforms, and shared capabilities; mark the five worst coordination hot spots. Acceptance: reviewed by role-played team leads who agree the hot spots are real.

**Common mistakes:** maps of systems without teams; "platform" for anything shared.

**Assessment:** landscape map defense.

**Workplace evidence:** an architecture landscape you produced that leadership used for planning.

**Career relevance:** platform strategy (STF-004) and business architecture (ARC-002).

---

### SRA-002 · Long-term system evolution
`n: 216` · **Video:** 84 min · **Practice:** 3.5 h

**Prerequisites:** SRB-014, SRA-001

**Learning outcomes** — the engineer can:
1. Define architectural fitness functions (performance, coupling, security, cost) and automate them.
2. Build a technical roadmap that connects target state, transition states, and checkpoints.
3. Track technology obsolescence (versions, end-of-support dates, vendor viability) and plan upgrades before they become emergencies.
4. Revise a roadmap when its assumptions change.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRA-002-L01 | Architecture decays unless guided | 10 |
| SRA-002-L02 | Fitness functions | 12 |
| SRA-002-L03 | Automating fitness functions | 10 |
| SRA-002-L04 | Technical roadmaps: target and transition states | 12 |
| SRA-002-L05 | Managing obsolescence | 10 |
| SRA-002-L06 | Demo: a fitness function that blocks a coupling regression | 15 |
| SRA-002-L07 | Demo: replanning a roadmap after a vendor end-of-life notice | 15 |

**Lab** — `SRA-002-LAB1` *Fitness and lifecycle:* five automated fitness functions for the commerce area and a three-year obsolescence calendar with upgrade plans. Acceptance: fitness functions run in CI; calendar covers every runtime, framework, and datastore.

**Common mistakes:** roadmaps as feature lists; upgrades left until security forces them.

**Assessment:** roadmap and fitness-function review.

**Workplace evidence:** a fitness function or lifecycle plan adopted by multiple teams.

**Career relevance:** technology portfolio (STF-007) and solution roadmaps (ARC-036).

---

### SRA-003 · Complex domain modeling
`n: 217` · **Video:** 88 min · **Practice:** 4 h

**Prerequisites:** MID-060, SRB-002

**Learning outcomes** — the engineer can:
1. Apply strategic DDD: subdomains (core, supporting, generic) and where to invest.
2. Build a context map with relationship patterns (partnership, customer–supplier, conformist, published language, open host service).
3. Design anti-corruption layers for legacy and third-party systems.
4. Run collaborative modeling sessions (event storming) with domain experts across teams.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRA-003-L01 | Strategic DDD | 12 |
| SRA-003-L02 | Core, supporting, and generic subdomains | 10 |
| SRA-003-L03 | Context mapping patterns | 14 |
| SRA-003-L04 | Anti-corruption layers | 10 |
| SRA-003-L05 | Event storming at scale | 12 |
| SRA-003-L06 | Demo: event storming the seller marketplace | 15 |
| SRA-003-L07 | Demo: an anti-corruption layer around a carrier API | 15 |

**Lab** — `SRA-003-LAB1` *Marketplace domains:* event-storm the marketplace with role-played domain experts; produce subdomain classification and a context map for Commerce 2030. Acceptance: build/buy implications noted per subdomain.

**Common mistakes:** treating every subdomain as core; context maps that mirror the org chart without examining it.

**Assessment:** context map defense.

**Workplace evidence:** a context map or modeling session that changed team or service boundaries.

**Career relevance:** cross-domain systems (STF-006) and enterprise integration (ARC-009).

---

### SRA-004 · Data ownership strategy
`n: 218` · **Video:** 84 min · **Practice:** 3.5 h

**Prerequisites:** SRB-007, SRA-003

**Learning outcomes** — the engineer can:
1. Design federated data ownership with clear domain owners for operational and analytical data.
2. Define data contracts (schema, semantics, quality, SLAs) between producing and consuming teams.
3. Establish governance for sensitive data that does not centralize all decisions.
4. Evaluate data mesh ideas against the organization's maturity.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRA-004-L01 | Who owns the data | 10 |
| SRA-004-L02 | Federated ownership | 12 |
| SRA-004-L03 | Data contracts | 12 |
| SRA-004-L04 | Federated governance | 10 |
| SRA-004-L05 | Data mesh: ideas and limits | 10 |
| SRA-004-L06 | Demo: writing a data contract for order events used by finance | 15 |
| SRA-004-L07 | Demo: resolving a dispute over who owns "customer" | 15 |

**Lab** — `SRA-004-LAB1` *Ownership map:* data ownership map for Commerce 2030 with data contracts for the five most consumed data sets. Acceptance: every data set has one owner; contracts include quality SLAs.

**Common mistakes:** a central data team owning everything; contracts without semantics.

**Assessment:** contract and ownership review.

**Workplace evidence:** a data contract or ownership agreement you established between teams.

**Career relevance:** data architecture and governance (ARC-023, ARC-030).

---

### SRA-005 · Multi-region trade-offs
`n: 219` · **Video:** 84 min · **Practice:** 3.5 h

**Prerequisites:** SRB-003, SRB-004

**Learning outcomes** — the engineer can:
1. Decide per capability how much availability vs consistency the business needs across regions.
2. Map jurisdictional requirements (residency, data transfer rules, local regulators) onto architecture.
3. Estimate the operational complexity and cost of each multi-region option.
4. Sequence a five-country expansion so complexity grows only when needed.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRA-005-L01 | Multi-region as a business decision | 10 |
| SRA-005-L02 | Consistency needs per capability | 12 |
| SRA-005-L03 | Jurisdiction and data transfer | 12 |
| SRA-005-L04 | The operational cost of regions | 10 |
| SRA-005-L05 | Sequencing geographic expansion | 10 |
| SRA-005-L06 | Demo: a capability-by-capability region decision table | 15 |
| SRA-005-L07 | Demo: costing three expansion options | 15 |

**Lab** — `SRA-005-LAB1` *Five-country plan:* region strategy for Commerce 2030's expansion with per-capability decisions, residency mapping, and cost. Acceptance: reviewed with a role-played legal/compliance advisor.

**Common mistakes:** one global decision for all capabilities; underestimating on-call and tooling cost per region.

**Assessment:** strategy review.

**Workplace evidence:** a regional or residency strategy you contributed to.

**Career relevance:** cloud architecture and compliance (ARC-012, ARC-029).

---

### SRA-006 · Enterprise resilience
`n: 220` · **Video:** 84 min · **Practice:** 3.5 h

**Prerequisites:** SRC-013, SRB-005

**Learning outcomes** — the engineer can:
1. Plan for regional and provider-level failures and decide what must survive them.
2. Run a chaos engineering program with hypotheses, blast-radius control, and learning reviews.
3. Identify systemic risks (shared dependencies, correlated failures, single teams, knowledge silos).
4. Present a resilience posture to leadership with prioritized investments.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRA-006-L01 | Resilience at organization scale | 10 |
| SRA-006-L02 | Regional and provider failure | 12 |
| SRA-006-L03 | Chaos engineering as a program | 12 |
| SRA-006-L04 | Systemic and correlated risk | 12 |
| SRA-006-L05 | Resilience investment cases | 8 |
| SRA-006-L06 | Demo: a chaos experiment with a hypothesis and abort criteria | 15 |
| SRA-006-L07 | Demo: finding the shared dependency behind three "unrelated" incidents | 15 |

**Lab** — `SRA-006-LAB1` *Resilience posture:* resilience assessment for Commerce 2030 with a chaos program plan and a ranked investment list. Acceptance: top risk quantified in business impact.

**Common mistakes:** chaos without hypotheses; resilience plans for services but not for people and tools.

**Assessment:** posture presentation.

**Workplace evidence:** a resilience program or systemic risk you led action on.

**Career relevance:** organization-wide reliability (STF-005) and resilience architecture (ARC-031).

---

### SRA-007 · Large-scale performance
`n: 221` · **Video:** 84 min · **Practice:** 3.5 h

**Prerequisites:** SRC-016, SRB-015

**Learning outcomes** — the engineer can:
1. Forecast capacity across many services from business drivers.
2. Build workload models that represent real traffic mixes, including new products (marketplace sellers).
3. Optimize cost and performance together (cost per transaction at target latency).
4. Set performance budgets for teams and track them.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRA-007-L01 | Capacity at product-area scale | 10 |
| SRA-007-L02 | Forecasting from business drivers | 12 |
| SRA-007-L03 | Workload modeling | 12 |
| SRA-007-L04 | Cost-performance optimization | 12 |
| SRA-007-L05 | Performance budgets for teams | 8 |
| SRA-007-L06 | Demo: forecasting the marketplace launch's load | 15 |
| SRA-007-L07 | Demo: trading 10 ms of latency for 25% lower cost | 15 |

**Lab** — `SRA-007-LAB1` *Three-year forecast:* capacity forecast and workload model for Commerce 2030, with cost per order at target latency per year. Acceptance: assumptions explicit; sensitivity to growth rate shown.

**Common mistakes:** linear extrapolation; ignoring new traffic shapes from new products.

**Assessment:** forecast review.

**Workplace evidence:** a capacity forecast used in budgeting.

**Career relevance:** cost architecture (ARC-021).

---

### SRA-008 · Architecture economics
`n: 222` · **Video:** 84 min · **Practice:** 3.5 h

**Prerequisites:** SRB-013, SRB-015

**Learning outcomes** — the engineer can:
1. Analyze build vs buy vs open source with total cost of ownership over several years.
2. Include opportunity cost, staffing, and exit cost in decisions.
3. Value architectural options (the cost of keeping a decision open vs committing).
4. Present an economic case that finance can check.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRA-008-L01 | Architecture decisions are investment decisions | 10 |
| SRA-008-L02 | Build vs buy vs open source | 12 |
| SRA-008-L03 | Total cost of ownership | 12 |
| SRA-008-L04 | Opportunity cost | 10 |
| SRA-008-L05 | Real options thinking | 10 |
| SRA-008-L06 | Demo: buy vs build for marketplace seller payouts | 15 |
| SRA-008-L07 | Demo: a finance review of an architecture business case | 15 |

**Lab** — `SRA-008-LAB1` *Payouts decision:* build vs buy analysis for seller payouts with five-year TCO, opportunity cost, and exit plan. Acceptance: role-played finance partner can reproduce the numbers.

**Common mistakes:** comparing licence cost to zero; ignoring engineering opportunity cost.

**Assessment:** business case review.

**Workplace evidence:** a build/buy decision you analyzed and its outcome.

**Career relevance:** technology assessment and financial analysis (ARC-008, ARC-039).

---

### SRA-009 · Security and compliance
`n: 223` · **Video:** 84 min · **Practice:** 3.5 h

**Prerequisites:** SRC-014, SRB-016

**Learning outcomes** — the engineer can:
1. Apply privacy by design (data minimization, purpose limitation, retention, consent) in architecture.
2. Design auditability (immutable audit logs, traceability of changes and access).
3. Translate regulatory constraints (e.g., GDPR, PCI DSS, local data laws) into architecture requirements with compliance partners.
4. Reduce compliance scope architecturally (tokenization, segmentation).

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRA-009-L01 | Compliance as an architecture driver | 10 |
| SRA-009-L02 | Privacy by design | 12 |
| SRA-009-L03 | Auditability | 10 |
| SRA-009-L04 | From regulation to requirements | 12 |
| SRA-009-L05 | Reducing compliance scope | 10 |
| SRA-009-L06 | Demo: shrinking PCI scope with tokenization | 15 |
| SRA-009-L07 | Demo: designing data deletion across 30 services | 15 |

**Lab** — `SRA-009-LAB1` *Marketplace compliance:* privacy and payment-compliance architecture for the marketplace, including seller data, payouts, and right-to-erasure across services. Acceptance: reviewed with a role-played compliance officer.

**Common mistakes:** treating compliance as documentation; deletion that misses derived stores and backups.

**Assessment:** compliance architecture review.

**Workplace evidence:** an architecture change you led that reduced compliance risk or scope.

**Career relevance:** privacy and compliance architecture (ARC-029).

---

### SRA-010 · Technical strategy
`n: 224` · **Video:** 94 min · **Practice:** 4.5 h

**Prerequisites:** SRA-002, SRA-008

**Learning outcomes** — the engineer can:
1. Write a technical strategy with diagnosis, guiding policies, and coherent actions.
2. Balance platform investment against product delivery with explicit allocation.
3. Prioritize modernization by business risk and opportunity.
4. Tie the strategy to measurable outcomes and review it periodically.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRA-010-L01 | What a technical strategy is | 10 |
| SRA-010-L02 | Diagnosis | 12 |
| SRA-010-L03 | Guiding policies | 12 |
| SRA-010-L04 | Coherent actions and investment allocation | 12 |
| SRA-010-L05 | Prioritizing modernization | 10 |
| SRA-010-L06 | Measuring and revising strategy | 8 |
| SRA-010-L07 | Demo: writing the diagnosis for Commerce 2030 | 15 |
| SRA-010-L08 | Demo: defending a 30% platform allocation to product leadership | 15 |

**Lab** — `SRA-010-LAB1` *Commerce 2030 strategy draft:* diagnosis, guiding policies, actions, and investment split for three years. Acceptance: every action traceable to the diagnosis; outcomes measurable.

**Common mistakes:** strategy as a list of goals; no explicit trade-offs; actions that ignore the diagnosis.

**Assessment:** strategy defense.

**Workplace evidence:** a technical strategy you authored or co-authored that guided investment.

**Career relevance:** the core of the Senior A capstone and Staff technical strategy (STF-002).
