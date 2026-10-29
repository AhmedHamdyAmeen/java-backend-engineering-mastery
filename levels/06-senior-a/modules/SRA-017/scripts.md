# SRA-017 · Architectural reviews — Lecture scripts

**Video:** 80 min · **Running case:** *Commerce 2030* — the group formed by Shop and FulfillCo has 25 engineering teams and plans a third-party seller marketplace, a five-country expansion, and doubled order volume each year for three years; the strategy must now be adopted by 25 teams, funded, and executed, with role-players acting as managers, product, finance, security, and executives.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRA-017-L01 · The reviewer's job (10 min)
**Goal:** define a review as help to the author, not a test of the reviewer.

**Key points**
- The purpose: reduce risk and cost before the design ships, while change is cheap.
- The author owns the design and the decision; the reviewer owns the quality of the feedback.
- Review quickly and fairly; slow reviews push teams to skip them.
- Reviewing to show expertise damages trust and learning.

**Show:** a review charter: scope, turnaround (for example two working days), roles, outputs (blocking issues, suggestions, questions), how disagreements escalate.

**Check:** Who owns the design decision? *(The authoring team.)*

---

## SRA-017-L02 · Reviewing for risk (12 min)
**Goal:** find the risks that would hurt most if missed.

**Key points**
- Ask what can lose data, lose money, leak data, or stop the business.
- Look at failure modes: dependencies, retries, partial failure, ordering, duplicates.
- Check the rollout: can it be tested, rolled back, and observed?
- Check the quality requirements the design claims against the design itself.

**Show:** a risk checklist: data loss and consistency, security and privacy, dependency failure, scaling limits, migration and rollback, operational readiness.

**Check:** Name one failure mode to check in any design with a queue. *(Message loss or duplicates on failure and retry.)*

---

## SRA-017-L03 · Reviewing for complexity and operability (12 min)
**Goal:** judge whether the team can build and run what they propose.

**Key points**
- Complexity is a cost: each new component, language, or pattern needs an owner and on-call.
- Ask whether a simpler design meets the requirement.
- Operability: who is paged, what dashboard shows health, how do you debug, how do you recover?
- Match the design to the team's capability, or note the gap.

**Show:** a table: proposed component, what problem it solves, a simpler alternative, who operates it, how failure is detected.

**Check:** What is the operability test for a new service? *(Who is paged, how failure is seen, and how it is recovered.)*

---

## SRA-017-L04 · Blocking issues vs preferences (8 min)
**Goal:** tell the author clearly which comments must be addressed and which may be ignored.

**Key points**
- Blocking: risk to data, security, a quality requirement, or the team's ability to operate it, with evidence.
- Preference: style, taste, or an alternative of similar value; label it as such.
- Every blocking issue states the risk and a path forward, not just "I don't like this".
- Few blocking issues, clearly marked, make a review respected.

**Show:** comment labels: [BLOCKING], [SUGGESTION], [QUESTION], each with reason and a path to resolution.

**Check:** What must a blocking comment include? *(The risk and a way forward.)*

---

## SRA-017-L05 · Questions that teach (8 min)
**Goal:** use questions so authors find problems themselves.

**Key points**
- A good question points at the gap without giving the answer: "what happens if this write succeeds and the event publish fails?"
- Questions teach and build ownership; verdicts build dependence.
- Ask open questions about failure, scale, and change.
- If the author cannot find it after a question or two, state the concern directly.

**Show:** five stock questions: what if it fails halfway, what if it runs twice, what if load is ten times, how will we know it is broken, how do we undo this?

**Check:** Why ask rather than tell? *(Authors learn and own the fix; you build their judgment.)*

---

## SRA-017-L06 · Demo: reviewing a team's marketplace search design (15 min)
**Goal:** run a full review of a search design for the marketplace; prepares SRA-017-LAB1.

**Steps**
1. Read the design: sellers' listings flow to a search index; indexing runs from a nightly batch.
2. Check risks: staleness for new listings, index rebuild time, relevance ownership, load at peak.
3. Check operability: who is paged, how stale data is detected, how a rebuild is done.
4. **Planned mistake:** list twenty comments of mixed weight. Fix: reduce to two blocking items (no way to see staleness, rebuild takes longer than the window) and label the rest as suggestions.
5. Send the review within two days with paths forward and offer a short call.

---

## SRA-017-L07 · Demo: a review that finds a data-loss risk through questions alone (15 min)
**Goal:** run a worked review in which questions lead the team to find the data-loss risk; prepares SRA-017-LAB1.

**Steps**
1. The design: an order service writes to its database and then publishes an event; consumers update inventory.
2. Ask: "what happens if the write succeeds and the process crashes before the publish?"
3. Ask: "how would inventory know?" and "how would we find the lost event?"
4. **Planned mistake:** announce "you need the outbox pattern" at the start. Fix: wait for the team's own conclusion and then confirm and discuss options.
5. Record the finding as blocking, with the team's chosen fix and a re-review point.

**Show:** a timeline of the failure: write committed, crash, no event, inventory never reserves.
