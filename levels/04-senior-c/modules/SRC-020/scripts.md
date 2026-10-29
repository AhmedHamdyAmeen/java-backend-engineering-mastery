# SRC-020 · Mentorship — Lecture scripts

**Video:** 63 min · **Running case:** *Order Processing at 10×* — Shop Platform's order subsystem must handle a 10× growth forecast, a 99.95% availability commitment, and a 15-minute recovery objective.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRC-020-L01 · Mentoring as a senior responsibility (8 min)
**Goal:** see mentoring as part of the senior role, not a favor.

**Key points**
- Senior impact includes raising the engineers around you; your output multiplies.
- Mentoring costs time; plan it as work, with a schedule and goals.
- The aim is independence: the mentee should need you less over time.
- Mentoring differs from teaching a skill (explaining) and sponsoring (advocating for opportunities); good mentors do all three as needed.

**Show** A mentoring agreement: goals, meeting cadence, what the mentee brings, what the mentor offers, how progress is reviewed.

**Check:** What is the aim of mentoring? *(Growing the mentee's independence.)*

---

## SRC-020-L02 · Delegation that grows people (12 min)
**Goal:** hand over work sized to stretch without breaking.

**Key points**
- Pick work slightly beyond the mentee's current comfort, with clear outcomes (what done looks like), not instructions for every step.
- Define the boundaries: decisions they own, when to ask, deadlines, and review points.
- Provide support: context, access, check-ins; resist taking over when it gets hard.
- Plan for failure: make it safe to fail by limiting blast radius.
- Recognize the outcome and what they learned.

**Show** Delegation brief: outcome, why it matters, constraints, decisions they own, check-in dates, how success is judged, what support is available.

**Check:** What should a delegation brief define rather than every step? *(The outcome and boundaries.)*

---

## SRC-020-L03 · Coaching through reviews (10 min)
**Goal:** use code and design review to build skills, not to rewrite.

**Key points**
- Ask questions that lead the author to see the issue ("what happens if this call times out?").
- Separate must-fix from suggestions and explain the principle behind the comment, not only the fix.
- Praise specifics that you want repeated.
- Let some imperfect choices stand if they are harmless; prioritize teachable points.
- Do not push your own style as correctness.

**Show** Three review comments rewritten: from "change this to a switch" to a question and a principle, labeled as suggestion versus required.

**Check:** Why ask questions in a review? *(They help the author discover the issue and build judgment.)*

---

## SRC-020-L04 · Design feedback (10 min)
**Goal:** give feedback on how someone thinks about design, not only on the code.

**Key points**
- Look for the reasoning: requirements understood, alternatives considered, trade-offs named, failure modes and operations covered.
- Ask "what would make you change this decision?" and "what did you rule out?".
- Give feedback on the habit, not only the artifact: "you jumped to a solution before stating the problem".
- Offer a method (decision records, failure-mode checklist) they can reuse.

**Show** A design feedback template: problem clarity, options, trade-offs, risks, operability, communication; one strength and one growth area each.

**Check:** What is design feedback about besides the document? *(The thinking habits that produced it.)*

---

## SRC-020-L05 · Growth plans (8 min)
**Goal:** track growth against level expectations.

**Key points**
- Use the level expectations as the reference: what is expected at the mentee's level and the next.
- Agree two or three focus areas per period, with evidence examples, not a long list.
- Check evidence together: work delivered, scope handled, independence shown.
- Adjust the plan when the context changes; celebrate progress.

**Show** Growth plan table: focus | expected behavior at next level | evidence so far | next stretch task | review date.

**Check:** Why limit focus areas? *(A short list can actually be practiced and evidenced.)*

---

## SRC-020-L06 · Demo: a coaching review of a junior's design doc (15 min)
**Goal:** coach a junior's design document without rewriting it; prepares SRC-020-LAB1.

**Steps**
1. Read the design doc for a small order-notification feature; note strengths first.
2. Identify the main growth areas: missing failure modes, no alternatives considered.
3. Run the conversation: ask questions, such as "what happens if the notification service is down?".
4. **Planned mistake:** rewrite the failure-handling section yourself. Fix: let the author draft it after a question and a pointer to a checklist.
5. Agree what to change and what is a suggestion; set a follow-up date.
6. Record growth observations against level expectations.

**Check:** What replaced rewriting the section? *(A question and a checklist so the author does the thinking.)*
