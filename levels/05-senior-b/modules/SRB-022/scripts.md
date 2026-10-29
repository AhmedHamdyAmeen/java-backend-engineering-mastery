# SRB-022 · AI tools across teams — Lecture scripts

**Video:** 86 min · **Running case:** *The FulfillCo integration* — the engineer leads the four-team program planned in SRB-P1 through delivery; role-players act as team leads, product, finance, and security.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRB-022-L01 · AI assistants as a team capability (10 min)
**Goal:** treat AI coding assistants as a capability to be introduced and managed across teams, not a personal tool choice.

**Key points**
- Individual use is already happening; the lead decides whether it is visible, safe, and consistent.
- Benefits vary by task: boilerplate, tests, and explanations help more than novel design.
- Costs: review load grows with more generated code, skill gaps for juniors, and risk of confident but wrong output.
- Treat adoption like any program: goal, pilot, policy, training, measurement.

**Show** A one-page framing: goal (reduce time on routine work without lowering quality), non-goals (replace review), risks, owner, review date.

**Check:** Why manage assistants at program level? *(Without shared rules, risk, cost, and quality vary by person and nobody can measure the effect.)*

---

## SRB-022-L02 · Pilots and rollout (12 min)
**Goal:** plan a staged rollout with pilots, training, and support.

**Key points**
- Pilot with volunteer teams first, including a skeptic and a team with a different codebase type.
- Use a control group or a baseline period so results can be compared.
- Provide training on prompting, verification, and what never to paste; name a support channel and an owner.
- Gate widening on criteria: policy in place, security review passed, metrics reviewed.
- Collect structured feedback, not only anecdotes.

**Show** Rollout timeline: weeks 1-2 baseline and policy, weeks 3-8 pilot with two teams and a control, week 9 review gate, weeks 10-14 wider rollout, ongoing review.

**Check:** Why need a control group or baseline? *(Without it, you cannot tell the tool's effect from other changes.)*

---

## SRB-022-L03 · Usage policy (12 min)
**Goal:** write a short policy people can follow.

**Key points**
- Confidentiality: what code and data may be sent to the tool; never customer data or credentials.
- Secrets: never paste keys or tokens; secret scanning stays on.
- Licensing and provenance: understand the tool's terms on output and any code-matching controls; involve legal.
- Review: generated code gets the same review and tests as any other; the author is accountable.
- Approved tools list and an exception route; verify tool terms and settings before recording.

**Show** A one-page policy outline: scope, approved tools, allowed data, forbidden data, review rule, incident reporting, owner, review date.

**Check:** Who is accountable for AI-generated code in a pull request? *(The author who submits it.)*

---

## SRB-022-L04 · Reviewing an AI tool's security (10 min)
**Goal:** run a security review of an AI assistant before approving it.

**Key points**
- Data handling: what leaves the company, where it is processed, whether it is used for training.
- Retention: how long prompts and outputs are kept and whether they can be deleted.
- Access: single sign-on, roles, audit logs, and admin controls such as policy enforcement and repository exclusions.
- Integration risks: permissions of IDE plugins and agents, access to repositories, and prompt injection through content the tool reads.
- Record answers with evidence (contract, documentation); verify claims before recording.

**Show** Questionnaire table: area | question | evidence | answer | risk rating. Example: *Retention | are prompts stored, for how long, deletable? | vendor terms | ... | medium.*

**Check:** Name two admin controls to look for. *(For example single sign-on with audit logs, and the ability to exclude repositories or enforce settings.)*

---

## SRB-022-L05 · Measuring impact without fooling yourself (12 min)
**Goal:** measure real effect with honest metrics.

**Key points**
- Vanity metrics (lines generated, suggestions accepted) say activity, not value.
- Use delivery metrics (lead time, deployment frequency), quality metrics (change failure rate, defect rate, rework), and developer experience (survey, time on toil).
- Measure review load: more code can mean more review time.
- Beware novelty effect, selection bias (enthusiasts self-select), and short windows.
- Report uncertainty and negative findings.

**Show** A measurement plan table: question | metric | baseline | pilot | control | decision rule.

**Check:** Why is "percent of code generated" a weak success measure? *(It measures usage, not whether delivery or quality improved.)*

---

## SRB-022-L06 · Demo: designing a two-team pilot with a control group (15 min)
**Goal:** design the FulfillCo pilot with two pilot teams and two control teams; prepares SRB-022-LAB1.

**Steps**
1. Write the pilot question and the decision it will inform.
2. Choose the teams and note how they differ (domain, size, maturity); balance pilot and control where possible.
3. Capture a baseline for lead time, change failure rate, defect rate, review time, and a short survey.
4. **Planned mistake:** let teams self-select the pilot only from enthusiasts. Fix: include at least one skeptical team and record selection in the report.
5. Define training, policy, and support; set the duration and a review gate.
6. Write the decision rule, for example what combined change in quality and speed would justify wider rollout.

**Check:** What does a control group let you do? *(Compare the pilot's change against what happened anyway.)*

---

## SRB-022-L07 · Demo: reading a pilot's results that look better than they are (15 min)
**Goal:** critique pilot data that appears positive but hides problems; prepares SRB-022-LAB1.

**Steps**
1. Read the headline: pilot teams shipped 25% more pull requests.
2. Check the baseline and control: the control team also rose, as a release deadline passed.
3. Check quality: defect rate rose slightly, and review time per pull request grew.
4. **Planned mistake:** report the headline to executives. Fix: present throughput, quality, review load, and survey together, with caveats.
5. Identify biases: self-selected volunteers, short window, novelty effect.
6. Propose the next step: extend the pilot, fix review capacity, retest.

**Check:** What did the control team's rise reveal? *(Part of the improvement was not due to the tool.)*
