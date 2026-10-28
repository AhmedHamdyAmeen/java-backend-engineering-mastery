# SRB-P2 — Engineering Leadership and Delivery

**Phase goal:** the engineer leads a technical initiative that spans several teams: aligning designs and dependencies, running lightweight governance, evaluating technology objectively, steering by metrics and cost, securing service-to-service communication, executing large migrations, and keeping stakeholders and peers aligned.

**Running case:** *The FulfillCo integration* continues. The engineer leads the four-team program planned in SRB-P1 through delivery. Role-players act as team leads, product, finance, and security.

**Format:** case studies, worked sessions, and multi-team role-play.

**Phase total:** ~14.2 h video · ~34 h practice

---

### SRB-011 · Cross-team design
`n: 205` · **Video:** 86 min · **Practice:** 4 h

**Prerequisites:** SRC-006, SRB-008

**Learning outcomes** — the engineer can:
1. Map ownership, interfaces, and dependencies across teams for an initiative.
2. Run a design process that includes every affected team before decisions harden.
3. Align contracts and timelines so teams can work in parallel (contract-first, stubs, feature flags).
4. Resolve design conflicts between teams with explicit criteria.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRB-011-L01 | Designs that cross team boundaries | 10 |
| SRB-011-L02 | Ownership and dependency mapping | 12 |
| SRB-011-L03 | Inclusive design processes | 10 |
| SRB-011-L04 | Contract-first parallel delivery | 12 |
| SRB-011-L05 | Resolving cross-team conflicts | 12 |
| SRB-011-L06 | Demo: a four-team design session for stock synchronization | 15 |
| SRB-011-L07 | Demo: unblocking a team stuck on another team's API | 15 |

**Lab** — `SRB-011-LAB1` *Program design:* dependency map, interface agreements, and integration timeline for the four FulfillCo teams; a recorded design session with role-played leads. Acceptance: every interface has an owner and a date; one conflict resolved on record.

**Common mistakes:** designing alone and "presenting" to teams; serial dependencies that block three teams on one.

**Assessment:** session facilitation scored by role-players.

**Workplace evidence:** a cross-team design you led to agreement.

**Career relevance:** cross-team programs (STF-013).

---

### SRB-012 · Architecture governance
`n: 206` · **Video:** 84 min · **Practice:** 3 h

**Prerequisites:** SRC-003, SRC-010

**Learning outcomes** — the engineer can:
1. Run an RFC process with clear scope, reviewers, and decision deadlines.
2. Facilitate design reviews that improve designs without becoming gatekeeping.
3. Define an exception process for deviations from standards, with expiry and follow-up.
4. Calibrate governance weight to decision reversibility and blast radius.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRB-012-L01 | Governance that helps | 10 |
| SRB-012-L02 | RFC processes | 12 |
| SRB-012-L03 | Running design reviews | 12 |
| SRB-012-L04 | Exceptions and waivers | 10 |
| SRB-012-L05 | Right-sizing governance | 10 |
| SRB-012-L06 | Demo: a design review that improves a proposal without blocking it | 15 |
| SRB-012-L07 | Demo: writing an RFC that gets a decision in one review | 15 |

**Lab** — `SRB-012-LAB1` *Program governance:* RFC template, review cadence, and exception process for the FulfillCo program; run two reviews. Acceptance: both RFCs reach a decision within the deadline.

**Common mistakes:** reviews without decisions; one process for every change size.

**Assessment:** review facilitation.

**Workplace evidence:** an RFC or review process you introduced and its effect on decision time.

**Career relevance:** architecture governance at scale (STF-003) and review boards (ARC-035).

---

### SRB-013 · Technology evaluation
`n: 207` · **Video:** 90 min · **Practice:** 3.5 h

**Prerequisites:** MID-044, SRC-003

**Learning outcomes** — the engineer can:
1. Frame an evaluation around the problem and weighted criteria before looking at products.
2. Design a time-boxed proof of concept that tests the riskiest assumptions.
3. Compare options with an evaluation matrix, including total cost and exit cost.
4. Avoid common biases (novelty, sunk cost, vendor demos).

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRB-013-L01 | Start with the problem | 10 |
| SRB-013-L02 | Criteria and weights | 10 |
| SRB-013-L03 | Proofs of concept that answer questions | 12 |
| SRB-013-L04 | Evaluation matrices | 10 |
| SRB-013-L05 | Exit costs and lock-in | 10 |
| SRB-013-L06 | Bias in technology choices | 8 |
| SRB-013-L07 | Demo: evaluating two workflow engines in a two-day PoC | 15 |
| SRB-013-L08 | Demo: scoring options and checking the matrix for bias | 15 |

**Lab** — `SRB-013-LAB1` *Workflow engine choice:* evaluate a workflow engine vs hand-built sagas for FulfillCo's returns process with a PoC and matrix. Acceptance: recommendation includes exit plan and cost over three years.

**Common mistakes:** PoCs that only test the happy path; criteria chosen after the favorite.

**Assessment:** evaluation report review.

**Workplace evidence:** a technology evaluation you ran and the decision it produced.

**Career relevance:** technology assessment (ARC-008) and vendor evaluation (ARC-040).

---

### SRB-014 · Engineering metrics
`n: 208` · **Video:** 82 min · **Practice:** 3 h

**Prerequisites:** MID-055, SRC-012

**Learning outcomes** — the engineer can:
1. Measure the four DORA metrics and explain what each reveals.
2. Combine delivery metrics with reliability indicators (SLO attainment, incident rate).
3. Use metrics for improvement, not team ranking, and avoid Goodhart effects.
4. Present a metric trend with a hypothesis and an experiment.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRB-014-L01 | Why measure delivery | 8 |
| SRB-014-L02 | DORA metrics | 14 |
| SRB-014-L03 | Reliability indicators | 10 |
| SRB-014-L04 | Metrics that backfire | 10 |
| SRB-014-L05 | From metric to improvement experiment | 10 |
| SRB-014-L06 | Demo: diagnosing a slow lead time from pipeline data | 15 |
| SRB-014-L07 | Demo: spotting a metric that is being gamed | 15 |

**Lab** — `SRB-014-LAB1` *Program dashboard:* DORA and reliability dashboard for the four teams and one improvement experiment based on it. Acceptance: experiment hypothesis, measure, and result recorded.

**Common mistakes:** comparing teams by metric; measuring without acting.

**Assessment:** metrics narrative review.

**Workplace evidence:** an improvement you drove using delivery or reliability metrics.

**Career relevance:** measuring impact (STF-019) and engineering productivity (STF-009).

---

### SRB-015 · Cost optimization
`n: 209` · **Video:** 84 min · **Practice:** 3.5 h

**Prerequisites:** MID-056, SRC-004

**Learning outcomes** — the engineer can:
1. Identify the main cloud cost drivers of a system (compute, storage, data transfer, managed services).
2. Attribute costs to services and teams with tagging and unit economics (cost per order).
3. Reduce cost with rightsizing, autoscaling, commitments, storage tiers, and architectural changes.
4. Weigh cost savings against reliability and engineering time.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRB-015-L01 | Cost as an architectural quality | 10 |
| SRB-015-L02 | Cloud cost drivers | 12 |
| SRB-015-L03 | Attribution and unit economics | 12 |
| SRB-015-L04 | Optimization levers | 12 |
| SRB-015-L05 | FinOps basics | 8 |
| SRB-015-L06 | Demo: cutting cost per order by 30% | 15 |
| SRB-015-L07 | Demo: tagging a cloud bill and finding the top three cost drivers | 15 |

**Lab** — `SRB-015-LAB1` *Cost per order:* attribute the combined platform's cloud bill to services, compute cost per order, and deliver a savings plan with risks. Acceptance: savings estimate traceable to bill line items.

**Common mistakes:** optimizing the smallest line items; savings that quietly reduce redundancy.

**Assessment:** cost analysis review.

**Workplace evidence:** a cost reduction you delivered with numbers.

**Career relevance:** architecture economics (SRA-008) and financial analysis (ARC-039).

---

### SRB-016 · Security architecture
`n: 210` · **Video:** 86 min · **Practice:** 3.5 h

**Prerequisites:** SRC-018, SRB-009

**Learning outcomes** — the engineer can:
1. Define identity boundaries for users, services, and partners across two merged organizations.
2. Apply zero-trust principles: authenticate and authorize every request, assume breach.
3. Design service-to-service authorization (workload identity, mTLS, scoped tokens, policy engines).
4. Plan least-privilege access to data across teams.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRB-016-L01 | Security architecture vs security features | 10 |
| SRB-016-L02 | Identity boundaries | 12 |
| SRB-016-L03 | Zero trust in practice | 12 |
| SRB-016-L04 | Service-to-service authorization | 12 |
| SRB-016-L05 | Policy as code | 10 |
| SRB-016-L06 | Demo: authorizing FulfillCo services to Shop events and APIs | 15 |
| SRB-016-L07 | Demo: replacing network-based trust with workload identity | 15 |

**Lab** — `SRB-016-LAB1` *Merged trust model:* identity and authorization architecture for Shop + FulfillCo services and partner access. Acceptance: no network-location-based trust remains; reviewed by a role-played security architect.

**Common mistakes:** "inside the VPC means trusted"; shared credentials between teams.

**Assessment:** architecture review.

**Workplace evidence:** a security architecture change you led across services.

**Career relevance:** security architecture strategy (STF-008) and identity architecture (ARC-027).

---

### SRB-017 · Large migrations
`n: 211` · **Video:** 94 min · **Practice:** 4.5 h

**Prerequisites:** SRC-011, SRB-008

**Learning outcomes** — the engineer can:
1. Sequence a migration into reversible phases with measurable checkpoints.
2. Use feature flags, shadow traffic, and canaries to compare old and new paths in production.
3. Run large data backfills safely (throttling, idempotency, verification).
4. Decommission legacy paths and prove they are unused.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRB-017-L01 | Anatomy of a large migration | 10 |
| SRB-017-L02 | Rollout strategies | 12 |
| SRB-017-L03 | Shadow traffic and comparison | 12 |
| SRB-017-L04 | Feature flags at program scale | 10 |
| SRB-017-L05 | Backfills | 12 |
| SRB-017-L06 | Decommissioning | 8 |
| SRB-017-L07 | Demo: shadow-reading shipment status from both systems | 15 |
| SRB-017-L08 | Demo: a backfill that has to be stopped and resumed | 15 |

**Lab** — `SRB-017-LAB1` *Execute phase one:* carry out the first extraction phase from SRB-008 with flags, shadow comparison, a backfill, and a rollback rehearsal. Acceptance: mismatch rate measured and below threshold before cut-over.

**Common mistakes:** cut-over without comparison data; flags that outlive the migration by years; legacy never turned off.

**Assessment:** migration execution report.

**Workplace evidence:** a migration you executed through cut-over and decommissioning.

**Career relevance:** migration strategy (ARC-037).

---

### SRB-018 · Mentoring senior peers
`n: 212` · **Video:** 82 min · **Practice:** 3 h

**Prerequisites:** SRC-020

**Learning outcomes** — the engineer can:
1. Facilitate design discussions among senior engineers so the best idea wins, not the loudest.
2. Resolve technical conflicts between peers with structured techniques.
3. Influence decisions without authority by building shared understanding.
4. Give feedback to peers that they act on.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRB-018-L01 | Mentoring people at your own level | 10 |
| SRB-018-L02 | Facilitating design discussions | 12 |
| SRB-018-L03 | Technical conflict resolution | 12 |
| SRB-018-L04 | Influence through understanding | 10 |
| SRB-018-L05 | Peer feedback | 8 |
| SRB-018-L06 | Demo: facilitating a deadlocked design debate | 15 |
| SRB-018-L07 | Demo: giving hard feedback to a senior peer | 15 |

**Lab** — `SRB-018-LAB1` *Deadlock:* two role-played senior engineers disagree on the stock-ledger design; facilitate to a decision both commit to. Acceptance: scored by role-players and an observer.

**Common mistakes:** deciding for others; avoiding the conflict.

**Assessment:** facilitation simulation.

**Workplace evidence:** a disagreement between senior engineers you helped resolve.

**Career relevance:** influence without authority (STF-011) and decision facilitation (STF-016).

---

### SRB-019 · Risk management
`n: 213` · **Video:** 82 min · **Practice:** 3 h

**Prerequisites:** SRC-009, SRB-011

**Learning outcomes** — the engineer can:
1. Identify technical, dependency, people, and schedule risks in a program.
2. Maintain a risk register with likelihood, impact, owner, and trigger.
3. Reduce uncertainty early with spikes, prototypes, and staged commitments.
4. Prepare contingency plans and decide when to invoke them.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRB-019-L01 | Risk in technical programs | 10 |
| SRB-019-L02 | Identifying risks | 10 |
| SRB-019-L03 | Risk registers that are used | 10 |
| SRB-019-L04 | Buying information early | 12 |
| SRB-019-L05 | Contingency planning | 10 |
| SRB-019-L06 | Demo: a monthly risk review that changes the plan | 15 |
| SRB-019-L07 | Demo: invoking a contingency plan when a dependency slips | 15 |

**Lab** — `SRB-019-LAB1` *Program risks:* risk register for the FulfillCo program and a contingency plan for the top three; the assessor triggers one risk mid-lab. Acceptance: response follows the plan or justifies deviation.

**Common mistakes:** registers written once; risks without owners or triggers.

**Assessment:** risk-response simulation.

**Workplace evidence:** a risk you identified early and the action it led to.

**Career relevance:** decision-making under uncertainty (SRA-013) and architecture risk registers (ARC-043).

---

### SRB-020 · Stakeholder communication
`n: 214` · **Video:** 82 min · **Practice:** 3 h

**Prerequisites:** SRC-017

**Learning outcomes** — the engineer can:
1. Translate technical work into business impact (revenue, risk, cost, customer experience).
2. Write status reports that state progress, risks, and asks honestly.
3. Write a technical proposal that a non-technical leader can approve.
4. Deliver bad news early with options.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRB-020-L01 | Knowing your audience | 10 |
| SRB-020-L02 | Business impact framing | 12 |
| SRB-020-L03 | Status reports | 10 |
| SRB-020-L04 | Technical proposals for decision-makers | 12 |
| SRB-020-L05 | Delivering bad news | 8 |
| SRB-020-L06 | Demo: rewriting an engineering update for the executive team | 15 |
| SRB-020-L07 | Demo: telling leadership the program is four weeks late | 15 |

**Lab** — `SRB-020-LAB1` *Program communication:* biweekly status reports for the FulfillCo program and a proposal to extend scope; present to role-played executives. Acceptance: executives can state the decision asked of them after reading.

**Common mistakes:** green status until the week before failure; jargon-heavy proposals.

**Assessment:** presentation and written report scored on the COM dimension.

**Workplace evidence:** a proposal you wrote that was approved by non-engineering leadership.

**Career relevance:** executive communication (SRA-019, STF-017).

---

## Senior B capstone — Architecture Modernization (`SRB-CAP`)

Full brief, acceptance criteria, and graduation gate: [`projects/ladder.md`](../../projects/ladder.md#05--architecture-modernization-srb-cap).
