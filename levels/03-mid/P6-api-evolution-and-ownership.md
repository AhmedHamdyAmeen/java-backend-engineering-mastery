# MID-P6 — API Evolution and Professional Ownership

**Phase goal:** the learner evolves running systems without breaking their consumers, documents decisions so others can follow them, plans and delivers work predictably, and acts as the owner of a service — including helping the engineers around them.

**Running project:** *Shop Platform* ships a breaking change safely, gains a full documentation set (C4, ADRs, runbooks), and is handed over as the Mid capstone.

**Phase total:** ~4.9 h video · ~11.5 h practice

> **Ordering change (v1.4):** MID-059 to MID-061 (architectural styles, DDD, microservices introduction) moved to the start of MID-P3, so this phase was renamed from "Software Architecture and Professional Ownership".

---

### MID-062 · API evolution
`n: 170` · **Video:** 58 min · **Practice:** 2.5 h

**Prerequisites:** JNR-020, MID-045

**Learning outcomes** — the learner can:
1. Classify changes to REST APIs and event schemas as compatible or breaking.
2. Evolve event schemas with a schema registry and compatibility rules (Avro or Protobuf).
3. Run a deprecation process: announce, measure usage, migrate consumers, remove.
4. Apply the tolerant-reader principle in consumers.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-062-L01 | What counts as a breaking change | 10 |
| MID-062-L02 | Evolving REST APIs | 10 |
| MID-062-L03 | Schema registries and compatibility modes | 12 |
| MID-062-L04 | Tolerant readers | 6 |
| MID-062-L05 | Deprecation done properly | 8 |
| MID-062-L06 | Demo: changing `OrderPlaced` without breaking consumers | 12 |

**Lab** — `MID-062-LAB1` *Money format change:* change how money is represented in the orders API and `OrderPlaced` across two releases without breaking any consumer. Acceptance: contract tests and schema registry pass at every step.

**Common mistakes:** removing fields in one release; versioning every change.

**Assessment:** change-classification quiz plus lab.

**Career relevance:** API and data contracts (SRC-006) and event architecture (ARC-026).

---

### MID-063 · Technical documentation
`n: 171` · **Video:** 68 min · **Practice:** 3 h

**Prerequisites:** MID-061

**Learning outcomes** — the learner can:
1. Write ADRs capturing context, options, decision, and consequences.
2. Write an RFC/design document for a change that needs review before building.
3. Draw C4 context, container, and component diagrams and sequence diagrams as code (Structurizr, PlantUML, or Mermaid).
4. Write an operational runbook for a known failure.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-063-L01 | Documentation that gets read | 8 |
| MID-063-L02 | Architecture decision records | 10 |
| MID-063-L03 | RFCs and design docs | 10 |
| MID-063-L04 | C4 diagrams | 12 |
| MID-063-L05 | Sequence diagrams | 8 |
| MID-063-L06 | Runbooks | 8 |
| MID-063-L07 | Demo: C4 diagrams of Shop Platform as code | 12 |

**Lab** — `MID-063-LAB1` *Shop docs:* C4 levels 1–3, sequence diagrams for the order saga, ADRs for the five biggest decisions, and runbooks for three alerts. Acceptance: a peer unfamiliar with Shop answers ten questions using the docs alone.

**Common mistakes:** diagrams with no legend; ADRs written after the fact without the alternatives.

**Assessment:** documentation review (COM dimension).

**Career relevance:** architecture documentation (SRC-010) and solution documentation (ARC-043).

---

### MID-064 · Estimation and delivery
`n: 172` · **Video:** 56 min · **Practice:** 2 h

**Prerequisites:** JNR-053

**Learning outcomes** — the learner can:
1. Clarify ambiguous requirements with questions and written acceptance criteria.
2. Decompose a feature into small, independently deliverable slices.
3. Estimate with ranges, identify the riskiest assumptions, and reduce them first (spikes).
4. Communicate progress and slippage early.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-064-L01 | Clarifying requirements | 10 |
| MID-064-L02 | Slicing work vertically | 10 |
| MID-064-L03 | Estimating with ranges | 10 |
| MID-064-L04 | Risk first: spikes and prototypes | 8 |
| MID-064-L05 | Reporting progress honestly | 6 |
| MID-064-L06 | Demo: breaking "returns and refunds" into slices | 12 |

**Lab** — `MID-064-LAB1` *Returns feature plan:* turn a one-paragraph request for returns and refunds into questions, acceptance criteria, slices, estimates, and a risk list. Acceptance: reviewed plan; first slice delivered.

**Common mistakes:** horizontal slices (all database work first); single-number estimates.

**Assessment:** planning exercise.

**Career relevance:** requirements engineering (SRC-001) and risk management (SRB-019).

---

### MID-065 · Engineering ownership
`n: 173` · **Video:** 56 min · **Practice:** 2 h

**Prerequisites:** MID-050

**Learning outcomes** — the learner can:
1. Describe what owning a service means: on-call, SLOs, dependencies, cost, and roadmap.
2. Prioritize between features, reliability work, and technical debt using evidence.
3. Run a production readiness checklist before launch.
4. Communicate service health and trade-offs to product and other teams.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-065-L01 | You build it, you run it | 8 |
| MID-065-L02 | On-call well | 10 |
| MID-065-L03 | Prioritizing reliability and debt | 10 |
| MID-065-L04 | Production readiness checklist | 8 |
| MID-065-L05 | Communicating as an owner | 8 |
| MID-065-L06 | Demo: a readiness review of the payments service | 12 |

**Lab** — `MID-065-LAB1` *Owner's pack:* a service ownership page for one Shop service (SLOs, dashboards, runbooks, dependencies, known risks, top three debts). Acceptance: passes the readiness checklist.

**Common mistakes:** ownership as "I wrote it"; debt listed but never prioritized.

**Assessment:** readiness review.

**Career relevance:** production readiness (SRC-011) — the bridge into Senior Grade C.

---

### MID-066 · Technical collaboration
`n: 174` · **Video:** 56 min · **Practice:** 2 h

**Prerequisites:** JNR-053

**Learning outcomes** — the learner can:
1. Review code for correctness, design, and operability, with comments that teach.
2. Give and receive feedback on designs constructively.
3. Mentor a junior engineer through pairing and well-scoped tasks.
4. Disagree and commit, escalating only when needed.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-066-L01 | Reviewing beyond style | 10 |
| MID-066-L02 | Feedback that lands | 8 |
| MID-066-L03 | Design reviews | 8 |
| MID-066-L04 | Mentoring juniors | 10 |
| MID-066-L05 | Disagreement and decisions | 8 |
| MID-066-L06 | Demo: reviewing a real pull request out loud | 12 |

**Lab** — `MID-066-LAB1` *Mentor and review:* review two Junior-level capstone PRs and pair with a Junior learner on one fix. Acceptance: reviews scored on usefulness; mentee feedback collected.

**Common mistakes:** rewriting the author's code in comments; approving without reading tests.

**Assessment:** review-quality rubric.

**Career relevance:** mentorship (SRC-020) and technical influence at every senior level.

---

## Mid-level capstone — Distributed Order Processing Platform (`MID-CAP`)

Full brief, acceptance criteria, and graduation gate: [`projects/ladder.md`](../../projects/ladder.md#03--distributed-commerce-platform-mid-cap).
