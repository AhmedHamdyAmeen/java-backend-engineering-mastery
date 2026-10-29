# SRA-011 · Technical vision — Lecture scripts

**Video:** 82 min · **Running case:** *Commerce 2030* — the group formed by Shop and FulfillCo has 25 engineering teams and plans a third-party seller marketplace, a five-country expansion, and doubled order volume each year for three years; the strategy drafted earlier must now be adopted, funded, and executed, with role-players acting as managers, product, finance, security, and executives.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRA-011-L01 · Why teams need a technical vision (10 min)
**Goal:** show that 25 teams with no shared picture of the future make locally sensible, globally conflicting choices.

**Key points**
- A vision describes the future state: where engineering is going and what will be true when it gets there.
- Without one, each team optimizes for its own quarter and the architecture drifts.
- A good vision settles recurring arguments before they start ("do we build or adopt?").
- You have no authority to order 25 teams; a vision people choose to follow is your main tool.

**Show:** two teams in Commerce 2030 independently picking different messaging approaches in the same month, and the cost of reconciling them a year later.

**Check:** Why does a leader without formal authority need a vision? *(Teams follow a picture they understand and agree with; orders are not available.)*

---

## SRA-011-L02 · Vision, strategy, and roadmap (10 min)
**Goal:** keep the three artifacts apart so each does its own job.

**Key points**
- Vision: where we are going (the destination). Strategy: how we choose to get there. Roadmap: when, in what order.
- The vision changes rarely; the strategy yearly; the roadmap often.
- A vision that lists projects and dates is a roadmap in disguise.
- A roadmap with no vision is a to-do list.

**Show:** a three-row table for Commerce 2030: "any seller can go live in a day" (vision), "own the seller domain, buy payments" (strategy), "Q1 onboarding service, Q3 settlement" (roadmap).

**Check:** Which of the three should change least often? *(The vision.)*

---

## SRA-011-L03 · Writing a vision people can use (12 min)
**Goal:** write a vision concrete enough to decide with.

**Key points**
- Describe the future in observable terms: what an engineer, a seller, an on-call person experiences in 2030.
- Include a decision test: "if we are choosing between A and B, the vision says..."
- Name what you are giving up; a vision that costs nothing guides nothing.
- Keep it short: a page or two, in everyday words.

**Show:** outline: context, destination in five concrete statements, principles for hard trade-offs, what we will not do, how we will know we are arriving.

**Check:** How can you test that a vision is not too abstract? *(Try to decide a real, current choice with it; if it cannot, it is too vague.)*

---

## SRA-011-L04 · Telling the vision as a story (10 min)
**Goal:** package the same vision for different audiences.

**Key points**
- Engineers need the why and the decisions it affects; executives need the business outcome; managers need what changes for their team this quarter.
- Three formats: full document, one-page summary, ten-minute talk.
- A story has a before (pain people recognize), a turning point, and an after.
- Repeat it; people need to hear it many times in many places.

**Show:** the same vision told three ways: a "day in the life of a seller launch" story for engineers, a three-bullet outcome slide for executives, a one-page summary for managers.

**Check:** Why use several formats? *(Different audiences care about different parts and have different time; one format reaches few.)*

---

## SRA-011-L05 · Feedback without dilution (10 min)
**Goal:** improve the vision from feedback without turning it into a compromise nobody owns.

**Key points**
- Ask for feedback early, from the people who must live with the vision.
- Sort feedback: facts that change the picture, preferences, and requests to add scope.
- Accept corrections to facts and clarity; hold the direction unless evidence changes it.
- Reply to every piece of feedback, even to say no and why.

**Show:** a feedback log with columns: source, comment, type (fact / clarity / preference / scope), decision, reason.

**Check:** Which feedback should change the direction of the vision? *(Evidence that an assumption behind it is wrong, not just preference.)*

---

## SRA-011-L06 · Demo: drafting the Commerce 2030 vision document (15 min)
**Goal:** write a first full vision document for Commerce 2030; prepares SRA-011-LAB1.

**Steps**
1. Collect inputs: the strategy draft, incident themes, and five short interviews with team leads about daily pain.
2. Write five concrete future-state statements (for example: a new seller goes live without a ticket to engineering).
3. Add trade-off principles and an explicit "we will not" list.
4. **Planned mistake:** list the first-year projects as the vision. Fix: move them to the roadmap and rewrite each as an outcome that guides decisions.
5. Run the decision test on three real pending choices; fix statements that cannot decide.
6. Circulate the draft to three team leads with a feedback log.

---

## SRA-011-L07 · Demo: presenting the vision to an all-hands of engineers (15 min)
**Goal:** run a worked leadership session delivering the vision to about 150 engineers; prepares SRA-011-LAB1.

**Steps**
1. Plan the ten minutes: pain recognized (2), destination story (3), what changes this quarter (3), how to give feedback (2).
2. Anticipate the three hard questions (jobs, rewrites, "is this another reorg?") and prepare honest answers.
3. Role-play the talk with a manager audience that interrupts with skepticism.
4. **Planned mistake:** spend eight minutes on architecture diagrams. Fix: cut to one diagram and add one concrete example from a team's current week.
5. Follow up within a week: publish the one-pager, answer open questions, and ask three teams to show how the vision changes their next quarter plan.

**Show:** a one-page summary layout: destination, why now, three decisions it changes, where to give feedback.
