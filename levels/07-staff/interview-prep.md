# Level 7 — Staff Software Engineer: Interview Preparation

The questions most often asked when hiring Staff engineers, how to answer them, and where in this course you learned and practiced each one.

**How to use this guide**
1. Answer each question **out loud** before reading the guidance. Staff interviews test how you think about organizations, not only systems.
2. Every answer needs **organizational evidence**: what changed for many teams because of you, and how you know.
3. Use the capstone to rehearse the reasoning; use your real work for the stories. At this level, interviewers probe until they find your actual role.

> **About "How often":** frequencies reflect commonly reported interview patterns for Staff-level roles, not measured statistics. Staff loops vary widely between organizations; verify against current job posts and update this guide when the market moves.

---

## 1. What the market asks for — and where you proved it

| Skill employers list | Learned in | Proven by |
| --- | --- | --- |
| Organization-wide technical strategy | STF-002, SRA-010 | `SRA-010-LAB1`, `STF-CAP` adoption roadmap |
| Platform and developer-experience strategy | STF-004, STF-009, SRB-010 | `SRB-010-LAB1` golden path, `STF-CAP` platform design |
| Influence without authority | STF-011, STF-016, SRB-018 | `SRB-018-LAB1`, `STF-CAP` governance process |
| Technical writing (RFCs, proposals) | STF-012, SRB-012 | `SRB-012-LAB1`, `STF-CAP` |
| Cross-team programs | STF-013, SRB-011 | `SRB-011-LAB1` |
| Reliability programs | STF-005, SRA-006 | `SRA-006-LAB1` |
| Technical due diligence | STF-010 | `STF-CAP` platform assessment |
| Measuring impact | STF-019, SRB-014 | `SRB-014-LAB1`, `STF-CAP` success metrics |
| Organizational change and adoption | STF-014, SRA-012 | `SRA-012-LAB1`, `STF-CAP` |
| Major-incident leadership | STF-018, SRC-019 | `SRC-019-LAB1` |

**Your portfolio at the end of Level 7:** the internal developer platform design and rollout plan (`STF-CAP`), plus written evidence of organizational impact from your real work. The capstone shows you can reason at Staff scope; only work evidence shows you have operated there.

## 2. How Staff interviews usually run

| Round | What happens | What they check | Prepare with |
| --- | --- | --- | --- |
| Hiring-manager / career deep-dive | Your last two or three roles in depth | Scope, leverage, archetype fit | Q1, Q13, Q14 |
| Org-scale system design | Design for many teams or a whole platform | Leverage, adoption, trade-offs | Q3, Q12 |
| Technical leadership / influence | How you drove change across teams | Influence without authority | Q4–Q6, Q10 |
| Past-impact presentation | Present a program you led, then Q&A | Real role, measurable outcomes | Q6, Q9, Q14 |
| Written exercise (some loops) | Write or critique an RFC | Clarity, framing, alternatives | Q5 |
| Executive / partner round | A director or VP interviews you | Business framing, judgment | Q2, Q8 |

---

## 3. The Staff role

### Q1 · What does a Staff engineer do that a senior engineer doesn't? Which kind of Staff engineer are you?
**How often:** Very common · **Round:** Hiring manager

**How to answer:**
- Senior engineers own outcomes for a system or team; Staff engineers create **leverage** across many teams — by solving problems no single team owns, setting direction, and multiplying others.
- Name the common archetypes (tech lead for a large area, architect, solver for hard problems, right hand to an engineering leader) and say which describes you, with evidence.
- Mention the boundary with management: you lead through influence and technical judgment, not reporting lines.

**Common trap:** describing yourself as "a very senior coder who also reviews a lot".

**Learned in:** STF-001, STF-020
**Practiced in:** `STF-001-LAB1`, `STF-020-LAB1`, `STF-CAP`
**Show it:** a one-page summary of your last year's impact framed by archetype.

---

### Q2 · How do you find and prioritize the problems worth your time across an organization?
**How often:** Very common · **Round:** Hiring manager, leadership

**How to answer:**
- **Discover:** listen across teams, read incident and delivery data, look for repeated toil and recurring cross-team friction.
- **Assess:** impact on the business, number of teams affected, whether anyone owns it, cost of waiting.
- **Choose:** few problems at a time; prefer those where your position adds unique leverage.
- **Say no:** explicitly hand off or drop work that a team can own.

**Common trap:** working on whatever is technically interesting.

**Learned in:** STF-002, STF-005, SRA-014
**Practiced in:** `STF-002-LAB1`, `STF-005-LAB1`, `SRA-014-LAB1`, `STF-CAP`
**Show it:** how you chose your last major initiative, with the alternatives you rejected.

---

## 4. Platforms and technical strategy

### Q3 · How would you design an internal developer platform for 15 product teams?
**How often:** Very common · **Round:** Org-scale design

**How to answer:**
1. **Users first:** interview teams; measure lead time, toil, onboarding time, incident causes.
2. **Platform as a product:** a small number of golden paths (service template, CI/CD, observability, security scanning, environments) with self-service and escape hatches.
3. **Architecture:** thin layers over existing tools; APIs and templates rather than tickets.
4. **Adoption:** start with willing teams, measure, make the paved road the easiest road; no mandates without tooling.
5. **Success metrics:** onboarding time, deployment frequency, change failure rate, developer satisfaction, cost.
6. **Governance and funding:** roadmap driven by user demand; deprecation policy.

**Common trap:** a platform designed from technology choices instead of user problems.

**Learned in:** STF-004, STF-009, SRB-010
**Practiced in:** `STF-004-LAB1`, `STF-009-LAB1`, `SRB-010-LAB1`, `STF-CAP`
**Show it:** the STF capstone's platform design and adoption roadmap.

---

### Q4 · How do you connect business priorities to engineering investment?
**How often:** Common · **Round:** Executive, leadership

**How to answer:**
- Start from business goals and constraints; translate them into technical capabilities and risks.
- Present investment options with expected outcomes and cost (including "do nothing").
- Agree an allocation (e.g., product vs platform vs reliability) and the metrics that will show whether it works.
- Revisit quarterly; kill investments that do not deliver.

**Common trap:** a technology roadmap with no link to business outcomes.

**Learned in:** STF-002, SRA-010, SRA-008
**Practiced in:** `STF-002-LAB1`, `SRA-010-LAB1`, `SRA-008-LAB1`
**Show it:** an investment case you made that leadership funded.

---

## 5. Influence and execution

### Q5 · How do you write an RFC that actually gets adopted?
**How often:** Very common · **Round:** Leadership, written exercise

**How to answer:**
- **Frame the problem** with evidence before the solution; state goals and non-goals.
- Present **real alternatives** honestly, including doing nothing.
- **Socialize early:** talk to the most affected and most skeptical people before publishing.
- Ask for a specific decision with a deadline; record dissent and how it was addressed.
- Follow through: adoption plan, owners, and measurement.

**Common trap:** a polished document that surprises its readers.

**Learned in:** STF-012, SRB-012
**Practiced in:** `STF-012-LAB1`, `SRB-012-LAB1`, `STF-CAP`
**Show it:** an RFC you wrote, the feedback that changed it, and its adoption.

---

### Q6 · Tell me about a time you drove a change across teams that didn't report to you.
**How often:** Very common · **Round:** Behavioral

**How to answer (STAR, Staff emphasis):**
- **Situation/Task:** the organization-wide problem and why no one owned it.
- **Action:** how you built trust and a shared understanding, found allies, handled resistance, adjusted the plan to teams' constraints, and made adoption easy.
- **Result:** measurable change across teams, and what remained after you stepped back.
- What this level must show: influence without authority and durable outcomes.

**Common trap:** a story where your manager's authority did the work.

**Learned in:** STF-011, STF-014, STF-016
**Practiced in:** `STF-011-LAB1`, `STF-014-LAB1`, `SRB-018-LAB1`, `STF-CAP`
**Show it:** adoption numbers or a before/after metric from your own program.

---

### Q7 · How would you run a program that spans several teams and quarters?
**How often:** Common · **Round:** Leadership

**How to answer:**
- Clear goal and success measures; ownership per workstream; dependency map.
- Milestones that deliver value early; risk register with triggers.
- Regular, honest status for stakeholders; escalate decisions, not problems.
- Close the program deliberately: handover, decommissioning, retrospective.

**Common trap:** confusing activity reporting with progress.

**Learned in:** STF-013, SRB-011, SRB-019
**Practiced in:** `STF-013-LAB1`, `SRB-011-LAB1`, `SRB-019-LAB1`
**Show it:** the FulfillCo program plan, and a real multi-team program you led.

---

### Q8 · How do you measure your own impact as a Staff engineer?
**How often:** Common · **Round:** Hiring manager

**How to answer:**
- Measure outcomes for the organization, not your output: adoption of what you built or proposed, reliability or delivery improvements (DORA, SLO attainment), cost, developer experience surveys.
- Add qualitative evidence: decisions you shaped, people who grew.
- Set a baseline before the work and compare after.

**Common trap:** counting documents written or meetings attended.

**Learned in:** STF-019, SRB-014
**Practiced in:** `STF-019-LAB1`, `SRB-014-LAB1`, `STF-CAP`
**Show it:** the capstone's success metrics and your own before/after data.

---

## 6. Reliability, risk, and hard problems

### Q9 · How would you improve reliability across an organization, not just one service?
**How often:** Common · **Round:** Org-scale design, leadership

**How to answer:**
- Diagnose systemically: incident themes, shared dependencies, teams without on-call maturity.
- Program elements: SLOs for key journeys, error-budget policies, incident process, postmortem follow-through, chaos experiments, platform defaults that make reliability easy.
- Sequence by risk; measure SLO attainment and incident impact over time.

**Common trap:** a reliability team that owns everyone's reliability.

**Learned in:** STF-005, SRA-006, SRC-012
**Practiced in:** `STF-005-LAB1`, `SRA-006-LAB1`, `SRC-012-LAB1`
**Show it:** a reliability improvement across several teams with numbers.

---

### Q10 · Walk me through how you led a major incident and what changed afterwards.
**How often:** Common · **Round:** Behavioral

**How to answer (STAR):**
- **Situation:** impact and scope.
- **Action:** incident command (roles, priorities, communications), mitigation choices under uncertainty.
- **Result:** recovery, and the **systemic** follow-up — the org-level change (process, platform, architecture) that prevents a class of incidents.

**Common trap:** stopping at the fix for that one incident.

**Learned in:** STF-018, SRC-019
**Practiced in:** `STF-018-LAB1`, `SRC-019-LAB1`
**Show it:** a postmortem whose action items changed something beyond one team.

---

### Q11 · You are asked to assess the architecture and team of a company we may acquire. How do you do it?
**How often:** Occasional · **Round:** Executive, org-scale design

**How to answer:**
- Agree the questions the business needs answered (integration cost, risk, key people, scalability).
- Review architecture, code samples, operations data, security posture, dependencies, licences, and team capabilities.
- Identify red flags and integration options with cost ranges.
- Report findings as risks and options, not a grade.

**Common trap:** a code-quality review that ignores people, operations, and integration.

**Learned in:** STF-010, SRB-007, SRB-008
**Practiced in:** `STF-010-LAB1`, `SRB-008-LAB1`, `STF-CAP`
**Show it:** the FulfillCo integration analysis as a worked example.

---

### Q12 · Design how 20 teams should deploy and observe their services consistently.
**How often:** Common · **Round:** Org-scale design

**How to answer:**
- Clarify constraints: current tooling diversity, regulatory needs, team autonomy expectations.
- Propose standards for the *interfaces* (deployment contract, telemetry conventions, SLO definitions), with a paved-road implementation.
- Migration plan: volunteers first, measurable benefits, deprecation path for old setups.
- Governance: exceptions process, ownership of the platform, feedback loop.

**Common trap:** mandating one toolset without a migration story.

**Learned in:** STF-003, STF-007, SRA-012
**Practiced in:** `STF-003-LAB1`, `STF-007-LAB1`, `SRA-012-LAB1`, `STF-CAP`
**Show it:** the capstone's CI/CD and observability standards.

---

## 7. Career story

### Q13 · Why do you want a Staff role, and what would your first 90 days look like?
**How often:** Very common · **Round:** Hiring manager

**How to answer:**
- Motivation tied to leverage, not title.
- First 30 days: listen and map (people, systems, problems). Days 30–60: pick one or two problems and build alignment. Days 60–90: deliver an early, visible improvement and propose direction.

**Common trap:** arriving with a plan before listening.

**Learned in:** STF-001, STF-020
**Practiced in:** `STF-001-LAB1`, `STF-020-LAB1`, `STF-CAP`
**Show it:** how you started your current or last role.

---

### Q14 · Tell me about the biggest impact you've had.
**How often:** Very common · **Round:** Deep-dive, hiring manager

**How to answer:**
- Pick work whose scope matches Staff: several teams or the whole organization.
- Explain the problem, *your* role precisely, the decisions you made, how you brought people along, and the measured result.
- Expect follow-ups probing what others did; credit them accurately.

**Common trap:** inflating your role — interviewers will dig until they find the truth.

**Learned in:** STF-019, STF-011
**Practiced in:** `STF-019-LAB1`, `STF-011-LAB1`, `STF-CAP`
**Show it:** a written impact narrative with metrics and named collaborators.

---

## 8. Six-week preparation plan

| Week | Focus | Do this |
| --- | --- | --- |
| 1 | Evidence | Write impact narratives for your three largest cross-team contributions, with metrics |
| 2 | Role and strategy | Rehearse Q1, Q2, Q4, Q13; define your archetype |
| 3 | Org-scale design | Q3, Q9, Q12 as timed mock designs using the `STF-CAP` platform |
| 4 | Influence and writing | Write one RFC from scratch in two hours; rehearse Q5–Q7 |
| 5 | Hard situations | Q10, Q11; practice a past-impact presentation with hostile questions |
| 6 | Full mocks | Two complete Staff loops with Staff or Principal engineers |

**Ready when:** every story shows impact beyond your own team with numbers, you can design for many teams and talk about adoption as fluently as architecture, and a skeptical interviewer cannot shrink your role by probing.
