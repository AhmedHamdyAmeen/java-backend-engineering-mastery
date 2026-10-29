# STF-021 · AI governance and engineering productivity — Lecture scripts

**Video:** 88 min · **Running case:** *Platform 2.0* — the Commerce group (Shop + FulfillCo) now has about 20 product teams; delivery has slowed, every team runs its own pipelines, the same incidents repeat, and onboarding takes weeks; you are a Staff engineer with no team of your own and a mandate to make the whole organization faster and safer.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## STF-021-L01 · Why AI needs governance, not prohibition (10 min)
**Goal:** explain why banning AI tools backfires and what governance does instead.

**Key points**
- Engineers adopt AI tools anyway; bans push use into personal accounts where data leaks go unseen.
- Governance sets safe, easy options: approved tools, clear data rules, and shared guardrails.
- Risks: data exposure, licensing, low-quality generated code, unreliable AI features.
- Aim: capture benefits while keeping risk visible and bounded.

**Show:** a two-column sketch: "Ban" (hidden use, unknown risk) versus "Govern" (approved tools, visible use, measured effect) for Platform 2.0.

**Check:** Why does a ban often increase risk? *(Use moves out of sight, so data handling is unmanaged.)*

---

## STF-021-L02 · Approved tools, data rules, and decision rights (12 min)
**Goal:** define the core rules and who decides.

**Key points**
- Approved tool list: reviewed for security, data handling, cost, and support; verify vendor terms and versions before recording.
- Data classes: what may never be shared, what may be shared with approved tools, what is free.
- Decision rights: teams choose within the list; security and legal approve additions; one owner keeps the list current.
- Keep the policy short enough to remember.

**Show:** a table of data classes (customer personal data, payment data, source code, public docs) against allowed tool tiers.

**Check:** Who should decide how a team uses an approved tool? *(The team, within the data rules.)*

---

## STF-021-L03 · Evaluation and quality standards (12 min)
**Goal:** set standards for AI features and AI-generated code that teams can meet themselves.

**Key points**
- AI features need evaluation sets, quality thresholds, and monitoring for drift and cost.
- AI-generated code goes through the same review, tests, and scanning as any code, with the author accountable.
- Provide shared templates and tooling for evaluations so teams do not build their own.
- Define what must be reviewed by humans before release.

**Show:** a one-page standard: required evaluation, threshold, monitoring, human review points, rollback.

**Check:** Who is accountable for AI-generated code in a pull request? *(The engineer who submits it.)*

---

## STF-021-L04 · Guardrails as paved roads (12 min)
**Goal:** put rules into the platform so compliance is the default.

**Key points**
- AI gateway: one entry point with logging, redaction of sensitive data, rate limits, and cost tracking.
- Pipeline scanning for secrets, licenses, and vulnerabilities in all code, whatever its source.
- Review rules and templates that apply to AI-assisted changes.
- Make exceptions explicit with an owner.

**Show:** an architecture sketch: developer tools and services calling models through the gateway, with policy checks and logs, and pipeline checks before merge.

**Check:** Why prefer a gateway to a policy document? *(A gateway enforces and records; a document relies on memory.)*

---

## STF-021-L05 · Measuring AI's effect on engineering (12 min)
**Goal:** measure effect honestly across about 20 teams.

**Key points**
- Take baselines before rollout: lead time, review time, defect rate, change failure rate, survey data.
- Compare adopting and non-adopting teams with caution; note confounders such as team size and work type.
- Track quality counter-metrics: defects, incidents, review load, security findings.
- Report ranges and caveats; avoid claims of a single percentage gain.

**Show:** a measurement plan table: metric, baseline, source, comparison group, caveat.

**Check:** Why track quality counter-metrics? *(Faster output can hide more defects or review burden.)*

---

## STF-021-L06 · Demo: turning an AI policy into platform guardrails (15 min)
**Goal:** convert a written policy into enforced platform controls; prepares STF-021-LAB1.

**Steps**
1. Take the draft policy and list each rule: data rules, approved tools, review requirements.
2. For each rule, decide the enforcement point: gateway, pipeline, template, or named owner.
3. Build the gateway design: logging, redaction, cost limits.
4. **Planned mistake:** a rule with no enforcement or owner ("do not paste secrets"). Fix: add a pipeline secret scan and gateway redaction, or assign a named owner.
5. Test with two teams and adjust.

---

## STF-021-L07 · Demo: an org-wide AI productivity report with honest caveats (15 min)
**Goal:** produce a report leadership can trust; prepares STF-021-LAB1.

**Steps**
1. Gather baselines and current data for 20 teams: delivery metrics, quality, survey.
2. Compare adopting and non-adopting teams and note differences in work type and team size.
3. Report gains and quality counter-metrics side by side.
4. **Planned mistake:** headlining "30% faster" from one team's anecdote. Fix: present ranges, sample sizes, and what is not yet known.
5. Recommend next steps: expand, adjust guardrails, or run a longer trial.
