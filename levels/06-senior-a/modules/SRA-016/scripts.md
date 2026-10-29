# SRA-016 · Engineering capability development — Lecture scripts

**Video:** 80 min · **Running case:** *Commerce 2030* — the group formed by Shop and FulfillCo has 25 engineering teams and plans a third-party seller marketplace, a five-country expansion, and doubled order volume each year for three years; the strategy must now be adopted by 25 teams, funded, and executed, with role-players acting as managers, product, finance, security, and executives.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRA-016-L01 · Capability is a system, not a talent (10 min)
**Goal:** treat the organization's ability to do something as designed, not as luck or a few heroes.

**Key points**
- Capability = skills + practices + tooling + incentives + time to use them.
- Hiring a star helps until they leave; a system keeps working.
- A strategy that needs event-driven design needs that capability across many teams.
- Capability gaps are strategy risks and belong on the strategy's risk list.

**Show:** a diagram of four levers around "can run services reliably": skills, practices (on-call, reviews), tooling (dashboards), time (capacity for learning).

**Check:** Why is training alone rarely enough? *(Skills fade without practices, tools, and time to apply them.)*

---

## SRA-016-L02 · Assessing capability gaps (10 min)
**Goal:** find where teams fall short of what the strategy requires.

**Key points**
- Start from the strategy: which capabilities must exist in 12 and 36 months?
- Gather evidence: incident reviews, design reviews, self-assessments, and code and operations data.
- Rate teams on a small scale (for example none, learning, practicing, teaching).
- Show gaps by capability and by team, not as a ranking of people.

**Show:** a heat map: capabilities (event design, SRE practice, data contracts) against teams, each cell rated and backed by evidence.

**Check:** Where does the assessment start? *(From the capabilities the strategy requires.)*

---

## SRA-016-L03 · Mentorship systems (10 min)
**Goal:** build mentoring that scales beyond your own one-to-one time.

**Key points**
- One-to-one mentoring does not scale to 25 teams; design for many.
- Components: mentor matching, learning paths, shadowing, pairing on real work, office hours.
- Train mentors; a good engineer is not automatically a good mentor.
- Align mentoring to strategy gaps, and review who is and is not being reached.

**Show:** a learning path for event-driven design: reading, a design review as shadow, pair on one real flow, lead a small design with a mentor watching.

**Check:** Why design mentoring as a system? *(One person's time does not reach 25 teams.)*

---

## SRA-016-L04 · Communities of practice (12 min)
**Goal:** start communities that last beyond the launch event.

**Key points**
- A community is a group with a shared craft that meets regularly to learn and solve problems.
- Start with real pain and two or three committed leaders, not a mailing list.
- Keep a cadence, a small output (a guideline, a toolkit, a talk), and a rotating host.
- Fade comes from no purpose, no sponsor, and no visible results; plan to hand off leadership.

**Show:** a guild charter: purpose, members, cadence, outputs, sponsor, how leadership rotates, how success is measured.

**Check:** Why do many communities fade after launch? *(No lasting purpose, rotation of leaders, or visible output.)*

---

## SRA-016-L05 · Measuring capability growth (8 min)
**Goal:** know whether the development effort is working.

**Key points**
- Measure outcomes, not attendance: fewer incidents of a kind, faster recovery, better review quality.
- Use leading signals too: practice adoption, number of people able to lead a design.
- Repeat the assessment at fixed intervals and compare to the baseline.
- Stop activities that do not move the outcome measures.

**Show:** a small scorecard: baseline, target, current for on-call readiness, mean time to recover, share of teams with tested runbooks.

**Check:** Why not measure attendance? *(It shows activity, not whether capability improved.)*

---

## SRA-016-L06 · Demo: launching a reliability guild (15 min)
**Goal:** launch and sustain a reliability community of practice for Commerce 2030; prepares SRA-016-LAB1.

**Steps**
1. Start from pain: repeated incidents across teams from missing timeouts and weak alerts.
2. Recruit three leaders from different teams and agree on a six-month purpose.
3. Run the first session on a real incident and produce a checklist for service reviews.
4. **Planned mistake:** launch with a large kickoff and a mailing list. Fix: start small with working sessions that produce an output each month, and publish it.
5. Set measures (incident rate for the covered failure type, adoption of the checklist) and plan rotation of the leader role after six months.

---

## SRA-016-L07 · Demo: a capability gap analysis across eight teams (15 min)
**Goal:** run a worked analysis showing where eight teams lag on strategy-critical capabilities; prepares SRA-016-LAB1.

**Steps**
1. List the strategy-critical capabilities: event-driven design, SRE practice, data contracts.
2. Gather evidence per team: incident reviews, design review notes, and short interviews.
3. Rate and build the heat map; look for capabilities that are weak across many teams.
4. **Planned mistake:** conclude "send everyone to training". Fix: pick the lever for each gap (training, a guild, tooling, hiring, or pairing), and sequence them.
5. Review the results with the engineering managers before sharing wider.

**Show:** a plan table: gap, affected teams, lever, owner, measure, date.
