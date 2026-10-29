# SRA-010 · Technical strategy — Lecture scripts

**Video:** 94 min · **Running case:** *Commerce 2030* — the group formed by Shop and FulfillCo has 25 engineering teams and plans a third-party seller marketplace, a five-country expansion, and doubled order volume each year for three years, while its earliest services approach end of life; you are the senior technical leader for the commerce product area.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRA-010-L01 · What a technical strategy is (10 min)
**Goal:** define a technical strategy and tell it apart from goals and roadmaps.

**Key points**
- A strategy has three parts: a diagnosis of the situation, guiding policies that choose an approach, and coherent actions that carry it out.
- It says what we will not do; a strategy without trade-offs is a wish list.
- A roadmap lists work; a strategy explains why that work and in what order.
- It is written to guide many teams making their own decisions.

**Show:** a one-page skeleton: diagnosis (what is hard and why), guiding policies (three to five rules), actions (owned, dated), measures, and review date.

**Check:** What are the three parts of a strategy? *(Diagnosis, guiding policies, and coherent actions.)*

---

## SRA-010-L02 · Diagnosis (12 min)
**Goal:** write a diagnosis that names the few problems that matter most.

**Key points**
- Gather evidence: incident history, delivery data, cost, obsolescence calendar, team interviews, business plans.
- Name the critical challenges in plain language and rank them; not every problem is a strategic one.
- Separate causes from symptoms: slow releases may come from coupling, not from slow engineers.
- A good diagnosis lets readers predict the policies.

**Show:** a diagnosis outline for Commerce 2030: three challenges (end-of-life core services, coordination load at 25 teams, marketplace load and compliance), each with evidence.

**Check:** Why separate causes from symptoms in a diagnosis? *(Policies aimed at symptoms do not fix the underlying problem.)*

---

## SRA-010-L03 · Guiding policies (12 min)
**Goal:** write policies that choose an approach and rule out others.

**Key points**
- A guiding policy is a rule of thumb that shapes many decisions, such as "buy generic capabilities".
- Good policies are specific enough to say no and are tied to the diagnosis.
- Include the trade-off: what we give up for what we gain.
- Provide defaults and an exception process.

**Show:** three policies with trade-offs: "New cross-domain access goes through published APIs (slower short-term features, lower coupling)", "Generic capabilities are bought (less control, faster delivery)", "Each region added needs a business trigger."

**Check:** What makes a policy useful rather than vague? *(It can rule out options and states its trade-off.)*

---

## SRA-010-L04 · Coherent actions and investment allocation (12 min)
**Goal:** choose actions that reinforce each other and decide how much to invest in them.

**Key points**
- Actions must follow from the policies and support one another; a list of unrelated projects is not coherent.
- Allocation: how much capacity goes to platform, product delivery, and keeping the lights on, stated explicitly.
- Each action has an owner, a sequence, a cost, and a measure.
- Reallocate at review points based on evidence.

**Show:** an allocation table by year: product delivery, platform and modernization, reliability and compliance, as percentages of engineering capacity, with the reasoning.

**Check:** Why state an explicit allocation? *(Otherwise the urgent product work absorbs all capacity and platform investment never happens.)*

---

## SRA-010-L05 · Prioritizing modernization (10 min)
**Goal:** rank modernization work by business risk and opportunity.

**Key points**
- Score each candidate on risk reduced (end of life, security, outage), opportunity enabled (marketplace, countries), and cost.
- Order by value and dependency; some work unlocks others.
- Prefer incremental modernization with visible value at each step over a big rewrite.
- Say what will not be modernized and why: some old systems are fine.

**Show:** a prioritization grid: candidate, risk score, opportunity score, cost, dependency, decision (now, next, later, never).

**Check:** Should every old system be modernized? *(No; modernize by risk and opportunity, and leave stable low-risk systems.)*

---

## SRA-010-L06 · Measuring and revising strategy (8 min)
**Goal:** tie the strategy to measurable outcomes and review it regularly.

**Key points**
- Choose a few outcome measures: lead time, incident minutes, cost per order, upgrade debt, adoption of platforms.
- Set baselines and targets, with owners and a reporting rhythm.
- Review at least yearly, and when major assumptions change.
- Revising is normal; record what changed and why.

**Show:** a scorecard of five measures with baseline, target at 12 and 36 months, owner, and data source.

**Check:** When should a strategy be revised? *(On a regular review and when key assumptions or evidence change.)*

---

## SRA-010-L07 · Demo: writing the diagnosis for Commerce 2030 (15 min)
**Goal:** write a diagnosis section from evidence; prepares SRA-010-LAB1.

**Steps**
1. Collect evidence from earlier modules: landscape map, obsolescence calendar, incident causes, forecast, compliance needs.
2. Cluster the evidence into candidate challenges and rank them by effect on the business plan.
3. Write three challenges with cause, evidence, and consequence if unaddressed.
4. Test it: can a team lead predict the policies from the diagnosis?
5. **Planned mistake:** write a list of goals ("be scalable", "be modern"). Fix: restate each as a specific challenge with evidence and a cause.
6. Circulate to team leads and capture disagreement.

---

## SRA-010-L08 · Demo: defending a 30% platform allocation to product leadership (15 min)
**Goal:** role-play defending an investment split against pressure for more product work; prepares SRA-010-LAB1.

**Steps**
1. Prepare: the diagnosis, the evidence of coordination cost, and the plan for what the 30% buys.
2. Present the trade-off: feature capacity lost now versus lead time and risk gained later.
3. Handle objections: "ship the marketplace first", "prove the return", "do it later".
4. Offer commitments: milestones, measures, a review at six months, and a fallback allocation if targets are missed.
5. **Planned mistake:** argue from technical purity ("we must clean up the code"). Fix: argue from business outcomes and measured delivery and risk data.
6. Agree on the decision and record it with the review date.
