# BEG-004 · Introduction to engineering — Lecture scripts

**Video:** 48 min · **Analogy used throughout:** building a house (architect, builders, inspectors, caretakers).
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-004-L01 · Developer vs software engineer (8 min)
**Goal:** explain why engineering is more than writing code.

**Key points**
- A developer writes code. An engineer also designs, tests, runs, and maintains it.
- Code is read many more times than it is written, so clarity matters.
- Real software is built by teams over years, not by one person in a weekend.
- Good engineers ask "what problem are we solving?" before "what should I type?".

**Show:** a pie chart: writing code is only one slice of the week.

**Check:** Name two engineering tasks besides writing code. *(Design, testing, fixing production issues, reviewing.)*

---

## BEG-004-L02 · Roles in an engineering team (12 min)
**Goal:** tell the main roles apart.

**Key points**
- Frontend: builds what the user sees.
- Backend: builds the hidden service, data, and rules.
- Full-stack: does both.
- QA: checks the software works and finds bugs.
- DevOps: automates building and releasing software.
- SRE: keeps the system reliable in production.
- Architect: decides how the big pieces fit together.
- They hand work to each other: a design becomes code, then tests, then a release, then operation.

**Show:** a row of roles with arrows for the hand-offs.

**Check:** Who keeps the system running at 3 a.m.? *(SRE / operations, often with the backend team.)*

---

## BEG-004-L03 · How a feature travels from idea to production (10 min)
**Goal:** follow one feature through the team.

**Key points**
- Idea → requirements → design → code → review → test → release → monitor.
- Code is reviewed by a teammate before it is merged.
- Automated tests run on every change.
- After release, the team watches for errors and user feedback.
- Small, frequent releases are safer than big ones.

**Show:** a conveyor belt with each step as a station.

**Check:** Why does a teammate review the code? *(To catch mistakes early and share knowledge.)*

---

## BEG-004-L04 · Your career map: the eight levels of this course (10 min)
**Goal:** know where this course is going.

**Key points**
- Beginner, Junior, Mid, Senior (grades C, B, A), Staff, Solution Architect.
- Each level adds scope: first a task, then a feature, then a service, then a system, then many teams.
- Technical skill is necessary but not enough: communication and judgment grow in importance.
- Senior jobs also need real production experience that no course replaces.

**Show:** a staircase with eight steps and one-line descriptions.

**Check:** What does a Junior level add over Beginner? *(Building real backend services with a framework.)*

---

## BEG-004-L05 · Demo: a day in a backend engineer's workflow, walked through (8 min)
**Goal:** see the engineering routine in practice.

**Steps**
1. Start with a ticket: "Return the customer's email in the order response."
2. Read the ticket and ask one clarifying question.
3. Create a branch, make the change, run the tests.
4. Open a pull request and respond to one review comment.
5. **Planned mistake:** forget to run the tests before the pull request; the automatic check fails. Fix it and push again.
6. Merge, release, and watch the dashboard for errors.
