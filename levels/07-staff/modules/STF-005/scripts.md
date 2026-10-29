# STF-005 · Organization-wide reliability — Lecture scripts

**Video:** 96 min · **Running case:** *Platform 2.0* — the Commerce group (Shop + FulfillCo) now has about 20 product teams; delivery has slowed, every team runs its own pipelines, the same incidents repeat, and onboarding takes weeks; you are a Staff engineer with no team of your own and a mandate to make the whole organization faster and safer.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## STF-005-L01 · Reliability as an organizational property (12 min)
**Goal:** show that reliability comes from how the organization works, not only from code.

**Key points**
- Repeated incidents across teams point to shared causes: missing practices, tools, incentives.
- Reliability needs clear ownership, SLOs, working on-call, and learning from failure.
- Uptime alone hides user-visible problems and slow degradation.
- Staff scope: fix the system that produces incidents, not each incident.

**Show:** a chart sketch of incidents per team with the same three causes recurring in many teams.

**Check:** Why do repeat incidents in many teams suggest an organizational cause? *(One team's habit would stay local; repeats across teams show shared gaps.)*

---

## STF-005-L02 · Mining incidents for systemic causes (12 min)
**Goal:** turn a pile of postmortems into a few systemic findings.

**Key points**
- Use a common tagging scheme: trigger, contributing factors, detection, recovery.
- Count by tag across teams, not only within one.
- Look for patterns: deploys without rollback, missing alerts, shared dependency failures.
- Share findings with the teams; they know the context and will correct you.

**Show:** a table of 30 incidents tagged by cause, with counts: "no safe rollback" 11, "alert missed" 9, "dependency overload" 6.

**Check:** What makes a cause systemic? *(It recurs across teams and reflects a shared gap rather than one mistake.)*

---

## STF-005-L03 · Designing a reliability program (12 min)
**Goal:** assemble a program with measurable goals.

**Key points**
- Core elements: SLO coverage, postmortem quality, action-item follow-through, on-call health.
- Each element has a target: for example 80% of services with SLOs, 90% of actions closed in 60 days.
- Provide help: templates, tooling, coaching, not only policy.
- Fund fixes for systemic causes as shared work.

**Show:** a program scorecard with four rows, the current value, the target, and an owner.

**Check:** Why add tooling and coaching to a policy? *(Policies without help create burden; help makes compliance easy.)*

---

## STF-005-L04 · Operational maturity models (10 min)
**Goal:** assess teams on a common scale to target help.

**Key points**
- A maturity model lists practices by level: basic monitoring, SLOs, tested rollback, game days.
- Use it to find where help is needed, not to rank or punish teams.
- Self-assessment plus a short review is cheaper than audits.
- Focus on teams that own critical customer paths.

**Show:** a grid of five practices by four levels with three example teams marked.

**Check:** What is a maturity model for? *(Directing help to the teams and practices that need it most.)*

---

## STF-005-L05 · On-call health (10 min)
**Goal:** treat on-call as a measurable part of reliability and engineer wellbeing.

**Key points**
- Measure pages per shift, out-of-hours pages, and share of noisy alerts.
- Ensure rotations are large enough, with handover and runbooks.
- Burnout leads to attrition and worse response.
- Reduce load by fixing the top noisy alerts first.

**Show:** a table of rotations with pages per week and share actionable; highlight rotations above target.

**Check:** What is the first step to improve a noisy rotation? *(Fix or remove the highest-volume non-actionable alerts.)*

---

## STF-005-L06 · Reporting reliability to leadership (10 min)
**Goal:** present reliability as business risk with trends.

**Key points**
- Translate to impact: revenue at risk, customer minutes lost, repeat incident count.
- Show trends over quarters, not single numbers.
- Pair each risk with a proposed investment and cost.
- Be honest about unknowns and data gaps.

**Show:** a one-page quarterly report: top risks, trend arrows, program scorecard, requested decisions.

**Check:** Why show trends? *(They show whether risk is improving or worsening, which one number cannot.)*

---

## STF-005-L07 · Demo: finding the cause behind 30 incidents in 12 teams (15 min)
**Goal:** run an incident-mining session; prepares STF-005-LAB1.

**Steps**
1. Collect the 30 postmortems and agree a tag set with two SRE leads.
2. Tag each incident independently, then reconcile differences.
3. Count by tag; chart the top causes and which teams are affected.
4. **Planned mistake:** declaring "human error" as a cause. Fix: ask what made the error easy and undetected; tag the missing guardrail.
5. Write three systemic findings with counts and a candidate shared fix for each.

---

## STF-005-L08 · Demo: a quarterly reliability review with the CTO (15 min)
**Goal:** present program status and ask for decisions; prepares STF-005-LAB1.

**Steps**
1. Build the one-page report: business risks, trend, program scorecard.
2. Choose the two decisions needed: fund a shared rollback tool, mandate SLOs for tier-one services.
3. Rehearse likely questions: cost, effect, who owns it.
4. **Planned mistake:** presenting twenty metrics. Fix: reduce to five that connect to business risk.
5. Run the review in role-play, record the decisions and follow-ups.
