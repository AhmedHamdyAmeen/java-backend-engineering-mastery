# SRA-014 · Leading ambiguous initiatives — Lecture scripts

**Video:** 80 min · **Running case:** *Commerce 2030* — the group formed by Shop and FulfillCo has 25 engineering teams and plans a third-party seller marketplace, a five-country expansion, and doubled order volume each year for three years; the strategy must now be adopted by 25 teams, funded, and executed, with role-players acting as managers, product, finance, security, and executives.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRA-014-L01 · Ambiguity is the job (10 min)
**Goal:** show that senior work starts from vague signals, not from specifications.

**Key points**
- At this level the problem arrives as a feeling: "checkout feels fragile", "the platform is slow to change".
- Waiting for someone to define it means it never gets defined.
- Your first deliverable is clarity, not code.
- Ambiguity is managed by steps: define, align, sequence, hand off.

**Show:** four raw signals collected in one week: three incident reports, a product complaint about launch speed, a manager's remark about on-call load. Nobody has linked them.

**Check:** What is the first deliverable on an ambiguous initiative? *(A clear problem statement everyone understands.)*

---

## SRA-014-L02 · Defining the problem (12 min)
**Goal:** turn vague signals into a problem statement backed by evidence.

**Key points**
- Gather evidence: interviews, incident data, lead-time and failure measures.
- Look for patterns across signals, not the loudest story.
- A problem statement names who is hurt, how much, and how we know; it contains no solution.
- Say what is out of scope and what success would look like.

**Show:** problem statement template: who, what happens, evidence (numbers), impact, why now, out of scope, how we will know it is better.

**Check:** What must a problem statement avoid? *(Smuggling in a solution.)*

---

## SRA-014-L03 · Alignment before solutions (10 min)
**Goal:** get stakeholders to agree the problem exists and matters before discussing fixes.

**Key points**
- Meet stakeholders one at a time first; surprise in a group meeting hurts.
- Ask each what they would call the problem; reconcile differences in wording and scope.
- Get the agreement in writing; revisit it if the facts change.
- Solution talk before alignment turns into a contest between favorites.

**Show:** alignment checklist: product, engineering managers, SRE, support, finance; each confirms the statement, impact estimate, and scope.

**Check:** Why align on the problem before solutions? *(Otherwise people argue favorite solutions to different problems.)*

---

## SRA-014-L04 · Sequencing for early value (10 min)
**Goal:** order the work so value shows early and learning starts quickly.

**Key points**
- Prefer the first milestone that removes real pain for a real team within weeks.
- Do the riskiest, most uncertain part early to learn cheaply.
- Each milestone should be useful on its own if the initiative stopped there.
- Publish milestones and measures so progress is visible without status meetings.

**Show:** two milestones for fragile checkout: M1 (six weeks) add timeouts, retries, and a dashboard on the top two failure points; M2 (quarter) isolate payment calls with a circuit breaker and measure the checkout failure rate.

**Check:** Why do the riskiest part early? *(You learn whether the plan works while changing it is still cheap.)*

---

## SRA-014-L05 · Handing off (8 min)
**Goal:** transfer the initiative to a team and step back at the right time.

**Key points**
- Hand off when the problem is clear, the first milestones are underway, and a team has the capacity and mandate.
- Hand over the why, the evidence, the decisions made, and the decision rights.
- Stay available for a defined period, then truly step away.
- Owning an initiative forever leaves you without capacity for the next ambiguity.

**Show:** a handoff note: problem statement, alignment record, milestones, open risks, who decides what, your office hours until a date.

**Check:** When do you hand off? *(When the problem is defined and a team has the mandate and capacity to carry it.)*

---

## SRA-014-L06 · Demo: turning "the platform is slow to change" into a defined initiative (15 min)
**Goal:** convert a vague complaint into a problem statement and measures; prepares SRA-014-LAB1.

**Steps**
1. Collect signals: lead-time data, three interviews, a quarter of change failures, and release calendars.
2. Look for patterns: most delay is waiting for another team's review, not building.
3. Write the problem statement with numbers: median change waits six days for approval across two teams.
4. **Planned mistake:** name the solution ("we need a new platform") in the statement. Fix: restate as the problem, with evidence, and list solutions separately later.
5. Add scope, success measures, and who must agree.

---

## SRA-014-L07 · Demo: the first 30 days of an ambiguous initiative (15 min)
**Goal:** run a worked leadership plan for the first month; prepares SRA-014-LAB1.

**Steps**
1. Week 1: gather evidence and interview ten people across product, support, SRE, and three teams.
2. Week 2: write the problem statement; meet stakeholders one on one.
3. Week 3: alignment session; record agreement and disagreements.
4. **Planned mistake:** present a full solution architecture in week 3. Fix: present options only after the problem statement is signed; the week-3 session ends with agreement on the problem and success measures.
5. Week 4: define the first two milestones, pick a team, and write the draft handoff note.

**Show:** a 30-day plan table: week, activity, output, who must be involved.
