# STF-022 · Leading an AI adoption program — Lecture scripts

**Video:** 86 min · **Running case:** *Platform 2.0* — the strategy, governance, and platform direction from STF-P1 must now be adopted by about 20 product teams who did not ask for them; role-players act as engineering managers, skeptical tech leads, product, finance, security, and executives.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## STF-022-L01 · AI adoption is organizational change (10 min)
**Goal:** apply organizational-change thinking to AI tools and AI features.

**Key points**
- Buying licenses is not adoption; changed work habits with better results are.
- Engineers differ widely in enthusiasm, trust, and skill; plan for each group.
- AI adds specific risks: leaked data, subtly wrong code, cost growth, over-reliance.
- Define the outcome (faster, safer delivery) before the tool metrics.

**Show:** a program one-pager: outcome, groups of engineers, risks, enablement, measures, review rhythm.

**Check:** Why are license counts a poor success measure? *(They show access, not better outcomes.)*

---

## STF-022-L02 · Champions, enablement, and communities (12 min)
**Goal:** build the support structure that spreads good practice.

**Key points**
- Champions: respected engineers in each team who try, share, and give feedback; give them time.
- Enablement: short hands-on sessions on real code, approved tools, and clear rules for data.
- Community: a channel, office hours, a shared library of good prompts and examples.
- A support route: who answers questions and handles problems.

**Show:** a program structure diagram: platform AI team, 20 champions, monthly community session, support channel, escalation to security.

**Check:** Why give champions protected time? *(Unfunded volunteer work fades under delivery pressure.)*

---

## STF-022-L03 · Resistance and trust (12 min)
**Goal:** respond honestly to fears about jobs, quality, and deskilling.

**Key points**
- Concerns are often valid: quality, security, learning, job impact.
- Do not promise what you cannot know; share what is known and what is not.
- Show evidence from pilots, including failures; keep review practices.
- Give people choice and voice: opt-in pilots, feedback, and a say in rules.

**Show:** a concerns table: concern, what we know, what we do about it, owner.

**Check:** Why is "they just resist change" a poor response? *(It dismisses valid concerns and loses trust.)*

---

## STF-022-L04 · Managing adoption risk (12 min)
**Goal:** plan for incidents before they happen.

**Key points**
- Risks: secrets or customer data in prompts, defect increase, cost overrun, licensing issues, over-reliance.
- Guardrails: approved tools, data classification rules, secret scanning, code review remains mandatory.
- Write the incident plan: who stops what, how fast, who is told.
- Define pause triggers (for example defect rate above a threshold) in advance.

**Show:** a risk register with trigger, owner, and response, plus a runbook "secret pasted into an AI tool: rotate, assess, notify, review".

**Check:** What should be decided before rollout? *(Pause triggers and the incident response plan.)*

---

## STF-022-L05 · Reporting and adjusting (10 min)
**Goal:** report outcomes and trade-offs to leadership and change the program from evidence.

**Key points**
- Report outcomes (cycle time, defects, incidents, cost, developer sentiment), not usage percentages.
- State trade-offs and unknowns openly.
- Compare with the baseline and a control where possible; do not overstate causation.
- Say what you will change next quarter.

**Show:** an executive report template: one-paragraph summary, outcome table with baseline, risks and incidents, cost, decision requests.

**Check:** What replaces "percent of engineers using the tool"? *(Outcome measures against a baseline.)*

---

## STF-022-L06 · Demo: a town hall on AI tools with skeptical engineers (15 min)
**Goal:** run an honest town hall; prepares STF-022-LAB1.

**Steps**
1. Prepare: collect questions in advance, anonymous allowed; group them.
2. Open with the goal, what is decided, and what is still open.
3. Answer hard questions directly (quality, jobs, data) and say "we do not know" where true.
4. **Planned mistake:** answering concerns with enthusiasm and vendor claims. Fix: acknowledge the concern and show evidence from our pilot.
5. Offer opt-in pilots and a feedback channel.
6. Publish the questions, answers, and follow-ups within a week.

---

## STF-022-L07 · Demo: pausing a rollout after a quality drop (15 min)
**Goal:** pause calmly using pre-agreed triggers; prepares STF-022-LAB1.

**Steps**
1. Spot the signal: defect escape rate in pilot teams up 30% over two sprints (illustrative figure).
2. Check against the pause trigger in the risk plan.
3. Pause expansion, keep existing pilots under stricter review, tell sponsors the same day.
4. **Planned mistake:** hiding the drop until the next monthly report. Fix: follow the plan and report immediately.
5. Investigate: review practice, prompt guidance, types of change.
6. Decide resume conditions and write them down before restarting.
