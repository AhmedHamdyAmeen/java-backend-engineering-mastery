# Level 6 — Senior Backend Engineer, Grade A: Interview Preparation

The questions most often asked when hiring senior engineers who lead the technical direction of a product area (titles vary: Senior, Lead, Principal-track), how to answer them, and where in this course you learned and practiced each one.

**How to use this guide**
1. Answer each question **out loud**, in under five minutes, before reading the guidance. At this level you are judged on judgment and clarity, not recall.
2. Every answer needs **evidence**: a decision you made, what it cost, and what changed because of it. Use the capstone *and* your real work.
3. If an answer feels thin, return to the module in **Learned in** and the lab in **Practiced in**, then collect the matching **workplace evidence** listed in that module's spec.

> **About "How often":** frequencies reflect commonly reported interview patterns for senior and lead backend roles, not measured statistics. Verify them against current job posts in your target market and update this guide when the market moves.

---

## 1. What the market asks for — and where you proved it

| Skill employers list | Learned in | Proven by |
| --- | --- | --- |
| Technical strategy and vision | SRA-010, SRA-011 | `SRA-010-LAB1`, `SRA-011-LAB1`, `SRA-CAP` strategy package |
| Long-term architecture evolution | SRA-001, SRA-002 | `SRA-002-LAB1` fitness functions and obsolescence calendar |
| Domain-driven design at scale | SRA-003, SRA-004 | `SRA-003-LAB1` marketplace context map, `SRA-004-LAB1` data contracts |
| Cost and build-vs-buy judgment | SRA-007, SRA-008 | `SRA-008-LAB1` payouts TCO |
| Multi-region, resilience, compliance | SRA-005, SRA-006, SRA-009 | `SRA-005-LAB1`, `SRA-006-LAB1`, `SRA-009-LAB1` |
| Standards and architecture reviews | SRA-012, SRA-017 | `SRA-012-LAB1`, `SRA-017-LAB1` |
| Leading ambiguous, cross-functional work | SRA-014, SRA-015 | `SRA-014-LAB1`, `SRA-015-LAB1` |
| Organizational design awareness | SRA-018 | `SRA-018-LAB1` team-boundary proposal |
| Executive communication | SRA-019 | `SRA-019-LAB1` funding pitch |
| Growing engineers and succession | SRA-016, SRA-020 | `SRA-016-LAB1`, `SRA-020-LAB1` |
| AI strategy and build vs buy | SRA-021 | `SRA-021-LAB1`, AI strategy in `SRA-CAP` |
| Responsible AI and AI compliance | SRA-022 | `SRA-022-LAB1` |

**Your portfolio at the end of Level 6:** the *Commerce 2030* strategy package (`SRA-CAP`) — vision, context map, roadmap, cost model, standards — plus a written record of the **workplace evidence** each SRA module asks for. Interviewers at this level care far more about the second.

## 2. How interviews usually run at this level

| Round | What happens | What they check | Prepare with |
| --- | --- | --- | --- |
| Hiring-manager screen | Career story, scope of past roles | Level of scope and influence | Q13, Q14 |
| Architecture / strategy presentation | You present a past strategy or a take-home case, then defend it | Diagnosis, trade-offs, sequencing | Q1–Q3, `SRA-CAP` |
| System design at product-area scale | Evolve an existing platform, not design from scratch | Evolution, data ownership, migration risk | Q2–Q6 |
| Deep-dive on past impact | One project examined for 60 minutes | Your actual role, decisions, outcomes | Q10, Q12, Q14 |
| Leadership and behavioral | Influence, conflict, growing people | Influence without authority | Q8–Q13 |
| Executive / cross-functional | A director or product leader interviews you | Business framing, clarity | Q9, Q11 |

---

## 3. Strategy and architecture evolution

### Q1 · How would you create a technical strategy for an area you just joined?
**How often:** Very common · **Round:** Strategy presentation, hiring manager

**How to answer:** use *diagnosis → guiding policies → coherent actions*.
1. **Listen first (30–60 days):** interviews with teams, product, operations; incident and delivery data; architecture landscape.
2. **Diagnosis:** the two or three problems that matter most, stated with evidence ("checkout changes need four teams; lead time tripled in a year").
3. **Guiding policies:** the rules that shape choices ("new capabilities are built as platform services with self-service onboarding").
4. **Coherent actions and allocation:** what you will do, in what order, with what share of capacity — and what you will *not* do.
5. **Measures and review:** outcome metrics and a quarterly review to revise.

**Common trap:** presenting goals ("be scalable, modern, cloud-native") as a strategy. Without a diagnosis it is a wish list.

**Learned in:** SRA-010, SRA-011, SRA-001
**Practiced in:** `SRA-010-LAB1`, `SRA-011-LAB1`, `SRA-CAP`
**Show it:** the Commerce 2030 diagnosis, and a real strategy or proposal you wrote at work that changed investment.

---

### Q2 · Our platform must handle 3× growth and a new product line in three years. How would you evolve the architecture?
**How often:** Very common · **Round:** System design at scale

**How to answer:** evolution, not a greenfield drawing.
1. **Clarify:** growth drivers, the new product's domain, constraints (budget, teams, regulation, deadlines).
2. **Current state:** where it breaks first — capacity model, coupling hot spots, end-of-life components.
3. **Target and transition states:** year-by-year architecture with the reason for each step.
4. **Sequencing:** do the risky, enabling work first; keep each step reversible where possible.
5. **Guardrails:** fitness functions that keep the direction (latency budgets, coupling rules, cost per transaction).
6. **Risks and checkpoints:** what would make you change course.

**Common trap:** jumping to "rewrite as microservices"; ignoring teams and migration cost.

**Learned in:** SRA-001, SRA-002, SRA-007
**Practiced in:** `SRA-002-LAB1`, `SRA-007-LAB1`, `SRA-CAP`
**Show it:** the Commerce 2030 transition architectures and forecast.

---

### Q3 · What are architectural fitness functions? Give examples you would use.
**How often:** Common · **Round:** System design, strategy

**How to answer:**
- A fitness function is an automated, objective check that the architecture keeps a desired property as it evolves.
- Examples: p99 latency budget in a performance test; ArchUnit rules forbidding domain → infrastructure dependencies; no new synchronous call chains deeper than two; cost per order below a threshold; dependency age and CVE severity limits.
- Explain where they run (CI, scheduled, production telemetry) and who owns acting on failures.

**Common trap:** listing metrics nobody acts on.

**Learned in:** SRA-002
**Practiced in:** `SRA-002-LAB1`
**Show it:** a fitness function that blocked a regression in the capstone, or a quality gate you introduced at work.

---

## 4. Domains, data, and economics

### Q4 · How do you decide service and team boundaries in a large domain?
**How often:** Very common · **Round:** System design, deep-dive

**How to answer:**
- Start from the **domain**: event storming with domain experts, then classify subdomains (core, supporting, generic) — invest where you differentiate.
- Draw a **context map** and choose relationships deliberately (customer–supplier, published language, anti-corruption layer for legacy and vendors).
- Check against **change data** (what changes together) and **team cognitive load**.
- Align team ownership with contexts; avoid one context split across several teams.

**Common trap:** boundaries by database table or technical layer.

**Learned in:** SRA-003, SRA-018
**Practiced in:** `SRA-003-LAB1`, `SRA-018-LAB1`
**Show it:** the marketplace context map and the team-boundary proposal built on it.

---

### Q5 · Who should own data in a multi-team organization, and how do consumers depend on it safely?
**How often:** Common · **Round:** System design

**How to answer:**
- Each data set has **one owning domain team**; others consume through published interfaces, not shared tables.
- **Data contracts** define schema, semantics, quality, freshness SLAs, and change policy.
- Governance is **federated**: central rules for sensitive data and interoperability, decisions otherwise in domains.
- Mention analytical use (events or CDC into a platform) without breaking ownership.

**Common trap:** a central data team that owns everything and becomes the bottleneck.

**Learned in:** SRA-004
**Practiced in:** `SRA-004-LAB1`
**Show it:** the order-events data contract for finance.

---

### Q6 · Build or buy? Walk me through how you would decide for a non-core capability.
**How often:** Very common · **Round:** Strategy, executive

**How to answer:**
1. **Is it core?** If it differentiates the business, lean build; if generic, lean buy or open source.
2. **Total cost of ownership over 3–5 years:** licences or infrastructure, engineering build and run, support, upgrades.
3. **Opportunity cost:** what the team would not build instead.
4. **Risk and exit cost:** vendor viability, lock-in, data portability, compliance.
5. **Decide and record** with assumptions, and revisit triggers.

**Common trap:** comparing a licence fee with "free" in-house development.

**Learned in:** SRA-008, SRA-003
**Practiced in:** `SRA-008-LAB1`
**Show it:** the seller-payouts five-year TCO your finance role-player could reproduce.

---

### Q7 · We are expanding into several countries with data-residency rules. What changes in the architecture?
**How often:** Common · **Round:** System design

**How to answer:**
- Decide **per capability** what must be regional (personal data, payments) and what can stay global (catalog, analytics with anonymized data).
- Map **jurisdiction** requirements with legal/compliance: residency, transfer rules, retention, deletion.
- Choose topology per capability (regional cells, global control plane), then estimate **operational cost** per region (on-call, tooling, deployments).
- Sequence expansion so complexity grows only when a market requires it.
- Design privacy in: minimization, deletion across all stores, auditability.

**Common trap:** one global "active-active everything" decision.

**Learned in:** SRA-005, SRA-009
**Practiced in:** `SRA-005-LAB1`, `SRA-009-LAB1`
**Show it:** the five-country region plan and the marketplace compliance architecture.

---

## 5. Leadership and influence

### Q8 · How do you set engineering standards without slowing teams down or centralizing every decision?
**How often:** Common · **Round:** Leadership

**How to answer:**
- Standardize only where inconsistency is expensive: interfaces, security, observability.
- Write standards as **principles + defaults + documented exceptions with expiry**.
- Make the standard the easiest path (templates, libraries, paved roads), then measure adoption.
- Retire standards that stop earning their cost.

**Common trap:** standards enforced by review gates with no tooling.

**Learned in:** SRA-012, SRA-017
**Practiced in:** `SRA-012-LAB1`
**Show it:** a standard teams adopted voluntarily at work, and adoption numbers.

---

### Q9 · Tell me about a time you had to make a major technical decision with incomplete information.
**How often:** Very common · **Round:** Behavioral

**How to answer (STAR, senior emphasis):**
- **Situation/Task:** the decision, its stakes, and the deadline.
- **Action:** the assumptions you made explicit and ranked; the cheapest experiment you ran to reduce the biggest uncertainty; how you kept options open or chose to commit.
- **Result:** the outcome *and* what happened when an assumption proved wrong — how your decision record made revisiting it fast.
- What this level must show: structured judgment, not certainty.

**Common trap:** a story where everything went as planned.

**Learned in:** SRA-013
**Practiced in:** `SRA-013-LAB1`
**Show it:** a decision record with assumptions from your work.

---

### Q10 · Describe an initiative you led that started without a clear problem definition.
**How often:** Common · **Round:** Behavioral, deep-dive

**How to answer (STAR):**
- **Situation:** the vague signal ("releases feel risky").
- **Action:** how you turned it into a defined problem with evidence, aligned stakeholders on the problem before solutions, sequenced early value, and handed it to a team.
- **Result:** measurable outcome and who owns it now.

**Common trap:** describing the solution you already wanted.

**Learned in:** SRA-014
**Practiced in:** `SRA-014-LAB1`
**Show it:** the "fragile checkout" brief, plus your real initiative.

---

### Q11 · How would you explain a major technical risk to the executive team and get a decision?
**How often:** Very common · **Round:** Executive, cross-functional

**How to answer:**
- Lead with **business impact** (revenue, customers, regulators, cost), not mechanics.
- Structure: situation → recommendation → options with cost and risk → the decision you need, by when.
- Admit uncertainty with ranges; keep detail in a one-page backup.
- Demonstrate it briefly in the interview.

**Common trap:** a technical tour that never asks for anything.

**Learned in:** SRA-019, SRA-011
**Practiced in:** `SRA-019-LAB1`
**Show it:** the year-one funding pitch; a real decision you obtained from leadership.

---

### Q12 · Our teams keep blocking each other. How would you diagnose and fix it?
**How often:** Common · **Round:** Leadership, system design

**How to answer:**
- Measure coordination cost: cross-team dependencies per change, handoffs, wait times.
- Compare team boundaries with the architecture (Conway's Law); look for teams with too much cognitive load or contexts split across teams.
- Options: change architecture to match desired teams (inverse Conway), change team boundaries with managers, add platform capabilities to remove shared toil.
- Measure again after the change.

**Common trap:** proposing a reorg alone, or architecture changes that ignore team structure.

**Learned in:** SRA-018, SRA-001
**Practiced in:** `SRA-018-LAB1`, `SRA-001-LAB1`
**Show it:** the Commerce 2030 hot-spot map and the team proposal that reduced dependencies.

---

### Q13 · How have you grown other engineers, and how do you avoid becoming a single point of failure?
**How often:** Very common · **Round:** Leadership, hiring manager

**How to answer (STAR):**
- **Growth:** specific people, how you delegated ownership (not tasks), how their scope grew.
- **Systems, not heroics:** a community of practice, review practice, or learning path you started.
- **Key-person risk:** how you mapped where the organization depends on you, created successors and decision-rights documents, and stepped back.
- Result: something that kept working without you.

**Common trap:** "I'm always available to help" — that is the problem, not the answer.

**Learned in:** SRA-016, SRA-020
**Practiced in:** `SRA-016-LAB1`, `SRA-020-LAB1`
**Show it:** a mentee's promotion or expanded scope; an area you handed over.

---

### Q14 · Tell me about the technical decision you are most proud of and one you regret.
**How often:** Common · **Round:** Deep-dive, hiring manager

**How to answer:**
- **Proud:** context, options considered, why you chose, measurable result, how you brought others along.
- **Regret:** what you missed, how you detected it, what you changed — in the system and in how you decide.
- Show self-awareness and learning; avoid blaming others.

**Common trap:** a "regret" that is a disguised success.

**Learned in:** SRA-013, SRA-017
**Practiced in:** `SRA-CAP`
**Show it:** two ADRs from your career with their outcomes.

---

## 6. AI questions

### Q15 · Leadership wants "an AI strategy" for the product area. How do you approach it?
**How often:** Increasingly common · **Round:** Strategy, executive

**How to answer:**
1. **Start from problems, not models:** list use cases by business value and feasibility (data available, error tolerance, regulatory risk).
2. **Choose the approach per use case:** hosted model API, open-weight model you host, RAG over your data, or fine-tuning — and say why (RAG for changing knowledge, fine-tuning for style or narrow tasks, self-hosting for data control or cost at scale).
3. **Total cost of ownership:** tokens or GPUs, engineering, evaluation, operations, and the cost of errors; include exit options to limit lock-in.
4. **Foundations:** data quality and access, an AI platform, evaluation and governance.
5. **Sequence:** a few high-value, low-risk use cases first, with measurable outcomes and a decision point to scale or stop.

**Common trap:** a strategy that is a list of tools, or "add a chatbot everywhere".

**Learned in:** SRA-021, SRA-008, SRA-010
**Practiced in:** `SRA-021-LAB1`, `SRA-CAP`
**Show it:** the AI section of your Commerce 2030 strategy; at work, an AI investment decision you shaped.

---

### Q16 · How do you make an AI feature responsible and compliant?
**How often:** Increasingly common · **Round:** Strategy, risk

**How to answer:**
- **Classify the risk** of the use case (risk-based regulation such as the EU AI Act takes this approach) and involve legal and compliance early.
- **Privacy:** minimize personal data in prompts, know where model calls are processed (residency), check vendor data-use terms, and support deletion.
- **Transparency and oversight:** tell users they are interacting with AI, keep a human in the loop for consequential decisions, and provide a way to contest outcomes.
- **Quality and fairness:** evaluate for bias and errors on representative data.
- **Auditability:** log inputs, outputs, model versions, and decisions so you can explain what happened.

**Learned in:** SRA-022, SRA-009
**Practiced in:** `SRA-022-LAB1`

---

## 7. Six-week preparation plan

| Week | Focus | Do this |
| --- | --- | --- |
| 1 | Your evidence | List your workplace evidence for every SRA module; pick three flagship stories with measurable outcomes |
| 2 | Strategy | Rehearse Q1–Q3 using the `SRA-CAP` package; present it in 20 minutes to a peer |
| 3 | Design at scale | Q4–Q7; run two "evolve this platform" mock design sessions |
| 4 | Leadership stories | Write STAR answers for Q8–Q14; cut each to three minutes |
| 5 | Executive round | Deliver the funding pitch to someone outside engineering; refine from their questions |
| 6 | Full mocks | Two complete mock loops with a Senior A or Staff engineer |

**Ready when:** you can present a strategy and handle a changed premise without losing the thread, every leadership answer has a measurable outcome from real work, and a non-engineer can repeat back the decision you asked them for.
