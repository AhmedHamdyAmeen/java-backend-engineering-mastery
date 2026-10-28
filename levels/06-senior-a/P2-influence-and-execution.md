# SRA-P2 — Influence and Organizational Execution

**Phase goal:** the engineer turns a technical strategy into organizational reality without formal authority: communicating a vision, setting standards people choose to follow, deciding well under uncertainty, leading ambiguous initiatives, working across functions, growing engineering capability, reviewing architectures, fixing organizational bottlenecks, speaking to executives, and making themselves replaceable.

**Running case:** *Commerce 2030* continues. The strategy drafted in SRA-P1 must now be adopted by 25 teams, funded by leadership, and executed. Role-players act as engineering managers, product, finance, security, and executives.

**Format:** case studies, worked sessions, and leadership role-play, with two worked sessions per module.

**Phase total:** ~13.4 h video · ~31.5 h practice

---

### SRA-011 · Technical vision
`n: 225` · **Video:** 82 min · **Practice:** 4 h

**Prerequisites:** SRA-010

**Learning outcomes** — the engineer can:
1. Write a multi-year engineering vision that describes the future state concretely enough to guide decisions.
2. Distinguish vision (where), strategy (how), and roadmap (when).
3. Communicate the vision in several formats (document, talk, one-page summary) for different audiences.
4. Gather feedback and revise the vision without losing its direction.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRA-011-L01 | Why teams need a technical vision | 10 |
| SRA-011-L02 | Vision, strategy, and roadmap | 10 |
| SRA-011-L03 | Writing a vision people can use | 12 |
| SRA-011-L04 | Telling the vision as a story | 10 |
| SRA-011-L05 | Feedback without dilution | 10 |
| SRA-011-L06 | Demo: drafting the Commerce 2030 vision document | 15 |
| SRA-011-L07 | Demo: presenting the vision to an all-hands of engineers | 15 |

**Lab** — `SRA-011-LAB1` *Commerce 2030 vision:* vision document, one-page summary, and a 10-minute talk; collect and incorporate feedback from role-played team leads. Acceptance: team leads can explain how the vision affects their next quarter.

**Common mistakes:** visions too abstract to guide a decision; visions that are roadmaps in disguise.

**Assessment:** vision talk and document review.

**Workplace evidence:** a vision you wrote that teams referenced in their own planning.

**Career relevance:** Staff technical strategy (STF-002) and architecture communication (ARC-044).

---

### SRA-012 · Engineering standards
`n: 226` · **Video:** 80 min · **Practice:** 3 h

**Prerequisites:** SRB-012, SRA-001

**Learning outcomes** — the engineer can:
1. Decide which things to standardize (interfaces, security, observability) and which to leave to teams.
2. Write standards as principles plus defaults plus documented exceptions.
3. Drive adoption through paved roads and tooling rather than mandates.
4. Retire standards that no longer earn their cost.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRA-012-L01 | The cost and value of standards | 10 |
| SRA-012-L02 | What to standardize | 12 |
| SRA-012-L03 | Principles, defaults, exceptions | 10 |
| SRA-012-L04 | Adoption through paved roads | 10 |
| SRA-012-L05 | Retiring standards | 8 |
| SRA-012-L06 | Demo: writing an observability standard teams accept | 15 |
| SRA-012-L07 | Demo: handling a team that wants an exception | 15 |

**Lab** — `SRA-012-LAB1` *Commerce standards:* three standards for Commerce 2030 (API, events, observability) with adoption plan and exception process. Acceptance: adoption measurable; one exception processed.

**Common mistakes:** standardizing languages and frameworks first; standards with no tooling support.

**Assessment:** standards review.

**Workplace evidence:** a standard you authored that teams adopted voluntarily.

**Career relevance:** technology portfolio and governance (STF-003, STF-007).

---

### SRA-013 · Decision-making under uncertainty
`n: 227` · **Video:** 82 min · **Practice:** 3 h

**Prerequisites:** SRC-003, SRB-019

**Learning outcomes** — the engineer can:
1. Make assumptions explicit and rank them by impact and uncertainty.
2. Design cheap experiments that reduce the most important uncertainty.
3. Value keeping options open and decide when to commit.
4. Record decisions with their assumptions so they can be revisited when assumptions fail.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRA-013-L01 | Deciding without all the facts | 10 |
| SRA-013-L02 | Surfacing and ranking assumptions | 12 |
| SRA-013-L03 | Experiments that buy information | 12 |
| SRA-013-L04 | Option value and commitment timing | 10 |
| SRA-013-L05 | Decision records with assumptions | 8 |
| SRA-013-L06 | Demo: an assumption map for the marketplace launch | 15 |
| SRA-013-L07 | Demo: revisiting a decision when its key assumption fails | 15 |

**Lab** — `SRA-013-LAB1` *Marketplace bets:* assumption map, two experiments, and decision records for the marketplace architecture; the assessor invalidates one assumption mid-lab. Acceptance: response follows from the recorded assumptions.

**Common mistakes:** analysis paralysis; decisions recorded without why.

**Assessment:** decision simulation.

**Workplace evidence:** a decision you made with explicit assumptions and later revisited.

**Career relevance:** technical due diligence (STF-010) and solution options (ARC-033).

---

### SRA-014 · Leading ambiguous initiatives
`n: 228` · **Video:** 80 min · **Practice:** 3.5 h

**Prerequisites:** SRB-011, SRA-013

**Learning outcomes** — the engineer can:
1. Define a problem worth solving from vague signals ("checkout feels fragile").
2. Build alignment on the problem before the solution.
3. Sequence delivery to show value early and learn quickly.
4. Know when to hand an initiative to a team and step back.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRA-014-L01 | Ambiguity is the job | 10 |
| SRA-014-L02 | Defining the problem | 12 |
| SRA-014-L03 | Alignment before solutions | 10 |
| SRA-014-L04 | Sequencing for early value | 10 |
| SRA-014-L05 | Handing off | 8 |
| SRA-014-L06 | Demo: turning "the platform is slow to change" into a defined initiative | 15 |
| SRA-014-L07 | Demo: the first 30 days of an ambiguous initiative | 15 |

**Lab** — `SRA-014-LAB1` *Fragile checkout:* from interview notes and incident data, define the problem, align role-played stakeholders, and plan the first two milestones. Acceptance: stakeholders agree on the problem statement in writing.

**Common mistakes:** jumping to a favorite solution; trying to own the initiative forever.

**Assessment:** initiative brief and alignment session.

**Workplace evidence:** an initiative you started from an ambiguous problem and handed to a team.

**Career relevance:** cross-team programs and organizational change (STF-013, STF-014).

---

### SRA-015 · Cross-functional leadership
`n: 229` · **Video:** 82 min · **Practice:** 3 h

**Prerequisites:** SRB-020

**Learning outcomes** — the engineer can:
1. Understand the goals and constraints of product, security, finance, legal, and infrastructure partners.
2. Build joint plans where engineering trade-offs are visible to partners.
3. Negotiate scope, timelines, and risk with partners as peers.
4. Build durable working relationships across functions.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRA-015-L01 | Engineering is one function among several | 10 |
| SRA-015-L02 | What product, finance, and security need from you | 12 |
| SRA-015-L03 | Joint planning | 10 |
| SRA-015-L04 | Negotiating as peers | 12 |
| SRA-015-L05 | Building relationships across functions | 8 |
| SRA-015-L06 | Demo: a joint planning session with product and finance | 15 |
| SRA-015-L07 | Demo: negotiating a security requirement that threatens a launch date | 15 |

**Lab** — `SRA-015-LAB1` *Marketplace launch plan:* joint plan with role-played product, finance, security, and legal partners. Acceptance: each partner signs off on the trade-offs that affect them.

**Common mistakes:** treating partners as blockers; hiding engineering risk from product.

**Assessment:** negotiation simulation.

**Workplace evidence:** a cross-functional plan you co-led.

**Career relevance:** stakeholder management (ARC-041).

---

### SRA-016 · Engineering capability development
`n: 230` · **Video:** 80 min · **Practice:** 3 h

**Prerequisites:** SRB-018

**Learning outcomes** — the engineer can:
1. Assess capability gaps across teams (skills, practices, tooling).
2. Design mentorship systems and learning paths beyond one-to-one mentoring.
3. Start and sustain communities of practice.
4. Measure whether capability development is working.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRA-016-L01 | Capability is a system, not a talent | 10 |
| SRA-016-L02 | Assessing capability gaps | 10 |
| SRA-016-L03 | Mentorship systems | 10 |
| SRA-016-L04 | Communities of practice | 12 |
| SRA-016-L05 | Measuring capability growth | 8 |
| SRA-016-L06 | Demo: launching a reliability guild | 15 |
| SRA-016-L07 | Demo: a capability gap analysis across eight teams | 15 |

**Lab** — `SRA-016-LAB1` *Capability plan:* gap analysis for Commerce 2030's strategy (e.g., event-driven design, SRE practices) and a one-year development plan. Acceptance: plan ties gaps to strategy actions.

**Common mistakes:** training as the only lever; communities that fade after the launch event.

**Assessment:** plan review.

**Workplace evidence:** a community of practice or learning program you started that outlived your direct involvement.

**Career relevance:** mentoring at scale (STF-015).

---

### SRA-017 · Architectural reviews
`n: 231` · **Video:** 80 min · **Practice:** 3.5 h

**Prerequisites:** SRC-018, SRB-012

**Learning outcomes** — the engineer can:
1. Review designs from other teams for risk, complexity, and operability quickly and fairly.
2. Distinguish blocking issues from preferences and say which is which.
3. Ask questions that let teams find problems themselves.
4. Track review outcomes and improve the review practice.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRA-017-L01 | The reviewer's job | 10 |
| SRA-017-L02 | Reviewing for risk | 12 |
| SRA-017-L03 | Reviewing for complexity and operability | 12 |
| SRA-017-L04 | Blocking issues vs preferences | 8 |
| SRA-017-L05 | Questions that teach | 8 |
| SRA-017-L06 | Demo: reviewing a team's marketplace search design | 15 |
| SRA-017-L07 | Demo: a review that finds a data-loss risk through questions alone | 15 |

**Lab** — `SRA-017-LAB1` *Review round:* review three designs from other learners (or provided designs); feedback rated by the authors. Acceptance: each review separates blocking issues from preferences.

**Common mistakes:** reviewing to show expertise; vague concerns without a path forward.

**Assessment:** review-quality rubric scored by authors.

**Workplace evidence:** reviews you gave that changed designs before they shipped.

**Career relevance:** architecture review boards and assurance (ARC-035, ARC-042).

---

### SRA-018 · Organizational bottlenecks
`n: 232` · **Video:** 82 min · **Practice:** 3 h

**Prerequisites:** SRC-008, SRA-001

**Learning outcomes** — the engineer can:
1. Explain Conway's Law and the inverse Conway maneuver with examples.
2. Measure coordination costs (cross-team dependencies, handoffs, wait times).
3. Recommend team boundary changes that align with the target architecture, working with engineering managers.
4. Recognize team cognitive-load limits (team topologies).

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRA-018-L01 | Conway's Law | 10 |
| SRA-018-L02 | Measuring coordination cost | 12 |
| SRA-018-L03 | Team topologies and cognitive load | 12 |
| SRA-018-L04 | The inverse Conway maneuver | 10 |
| SRA-018-L05 | Working with managers on team design | 8 |
| SRA-018-L06 | Demo: finding the team that every change waits on | 15 |
| SRA-018-L07 | Demo: proposing a team split aligned with the context map | 15 |

**Lab** — `SRA-018-LAB1` *Team design proposal:* using dependency data, propose team boundary changes for Commerce 2030 aligned with the context map, and present to role-played engineering managers. Acceptance: proposal reduces measured cross-team dependencies.

**Common mistakes:** reorganizing without changing architecture (or the reverse); ignoring managers' constraints.

**Assessment:** proposal review.

**Workplace evidence:** a team-boundary or ownership change you influenced and its effect.

**Career relevance:** organizational change (STF-014).

---

### SRA-019 · Executive communication
`n: 233` · **Video:** 80 min · **Practice:** 3 h

**Prerequisites:** SRB-020, SRA-011

**Learning outcomes** — the engineer can:
1. Translate technical risk into business impact executives can weigh (revenue, customers, regulators, cost).
2. Structure a short executive brief: situation, recommendation, options, ask.
3. Answer hard questions concisely and admit uncertainty.
4. Secure a decision or funding within a fixed time slot.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRA-019-L01 | How executives decide | 10 |
| SRA-019-L02 | From technical risk to business impact | 12 |
| SRA-019-L03 | The executive brief | 10 |
| SRA-019-L04 | Handling hard questions | 10 |
| SRA-019-L05 | Getting to a decision | 8 |
| SRA-019-L06 | Demo: a 10-minute funding pitch for the modernization program | 15 |
| SRA-019-L07 | Demo: briefing the CEO after a major outage | 15 |

**Lab** — `SRA-019-LAB1` *Funding pitch:* 10-minute pitch to role-played executives for year one of Commerce 2030 with one page of backup. Acceptance: a clear decision is reached within the slot.

**Common mistakes:** technical detail first; asking for nothing specific; overstating certainty.

**Assessment:** pitch scored on the COM and LEA dimensions.

**Workplace evidence:** an executive decision or funding you secured.

**Career relevance:** executive communication (STF-017) and architecture communication (ARC-044).

---

### SRA-020 · Succession and delegation
`n: 234` · **Video:** 78 min · **Practice:** 2.5 h

**Prerequisites:** SRB-018

**Learning outcomes** — the engineer can:
1. Identify where the organization depends on them (or any single person) and the risk this creates.
2. Delegate ownership, not just tasks, with clear decision rights.
3. Grow successors for their own responsibilities.
4. Document knowledge so it survives their absence.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRA-020-L01 | Key-person risk | 10 |
| SRA-020-L02 | Delegating ownership | 12 |
| SRA-020-L03 | Decision rights | 8 |
| SRA-020-L04 | Growing successors | 10 |
| SRA-020-L05 | Knowledge that survives you | 8 |
| SRA-020-L06 | Demo: mapping your own key-person risks | 15 |
| SRA-020-L07 | Demo: a handover of decision rights for the event platform | 15 |

**Lab** — `SRA-020-LAB1` *Make yourself replaceable:* key-person risk map for Commerce 2030 (including the learner's own role) and a succession plan for three critical areas. Acceptance: each area has a named successor path and decision-rights document.

**Common mistakes:** delegating tasks while keeping all decisions; succession plans that exist only on paper.

**Assessment:** plan review.

**Workplace evidence:** an area you handed over that continued to thrive without you.

**Career relevance:** sustainable leadership (STF-020).

---

## Senior A capstone — Multi-Year Platform Evolution (`SRA-CAP`)

Full brief, acceptance criteria, and graduation gate: [`projects/ladder.md`](../../projects/ladder.md#06--multi-year-platform-evolution-sra-cap).
