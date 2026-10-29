# STF-014 · Organizational change — Lecture scripts

**Video:** 94 min · **Running case:** *Platform 2.0* — the strategy, governance, and platform direction from STF-P1 must now be adopted by about 20 product teams who did not ask for them; role-players act as engineering managers, skeptical tech leads, product, finance, security, and executives.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## STF-014-L01 · Why technical change is organizational change (12 min)
**Goal:** show that a technical rollout succeeds or fails through people, habits, and incentives.

**Key points**
- A better tool unused is a failed change; adoption is the outcome.
- People adopt when the new way is easier, safe, and rewarded.
- Announcing a change is not adopting it.
- Plan for habits, skills, support, and team priorities, not only for code.

**Show:** two timelines for the golden path: "announce and wait" (3 teams after six months) versus "pilot, support, expand" (with adoption counts per month).

**Check:** Why is announcing not enough? *(People change behaviour when they see value, have support, and face fewer obstacles, not when told.)*

---

## STF-014-L02 · Adoption curves and early adopters (12 min)
**Goal:** plan adoption in waves, starting with the willing.

**Key points**
- Teams adopt at different speeds: eager pilots, practical majority, cautious late adopters.
- Choose pilots that are willing, representative, and visible; give them strong support.
- Turn their results into proof points other teams can read.
- Plan for the middle majority: documentation, migration tools, peers' stories.

**Show:** an adoption curve with pilot, early, majority, and late waves, and a proof point attached to each wave (for example "build time down 40%"; verify before recording any such number).

**Check:** What should a pilot team provide beyond using the platform? *(Honest feedback and a proof point other teams trust.)*

---

## STF-014-L03 · Incentives (10 min)
**Goal:** make the new way the easy and rewarded one.

**Key points**
- Ask what each team is rewarded for: delivery dates, uptime, features.
- Remove cost: migration tools, pair engineers, a dedicated support channel.
- Add benefit: faster releases, less on-call, audit evidence for free.
- Mandates are a last resort and need a date and an exit path for the old system.

**Show:** an incentive table per stakeholder: what they are measured on, how the golden path helps or hurts, what we change.

**Check:** What should you do if a team is rewarded only for features? *(Lower their migration cost and show the feature-speed benefit; discuss priority with their manager.)*

---

## STF-014-L04 · Understanding resistance (12 min)
**Goal:** treat resistance as information about real causes.

**Key points**
- Common causes: lost autonomy, unclear benefit, migration cost, past bad experience, fear of blame.
- Ask and listen; each cause has a different response.
- Some resistance is right; the plan may need to change.
- Silence is not agreement; look for quiet non-adoption.

**Show:** a resistance register: team, stated reason, probable cause, response, owner, status.

**Check:** What does resistance tell you? *(Something about cost, risk, trust, or fit that the plan did not address.)*

---

## STF-014-L05 · Feedback loops during change (10 min)
**Goal:** adjust the change while it is under way.

**Key points**
- Measure adoption (teams migrated, services using the path), outcomes (lead time, incidents), and sentiment (short survey).
- Review on a fixed rhythm; decide what to change.
- Close the loop: tell teams what you changed because of their feedback.
- Watch leading signals such as support-channel questions.

**Show:** a monthly adoption review one-pager: adoption chart, top three friction points, changes made, changes planned.

**Check:** What do you do with feedback? *(Act on it, and tell people what changed.)*

---

## STF-014-L06 · When to stop pushing (8 min)
**Goal:** recognize when a change should pause, change shape, or end.

**Key points**
- Signals: adoption stalls despite support, harm to delivery, a better alternative emerges.
- Decide stop criteria at the start, with the sponsor.
- Stopping can be partial: keep the pieces that work.
- Say so openly; credibility grows when you correct course.

**Show:** a decision rule: "If fewer than 8 teams adopt by month 6 and friction items remain open, review scope with the sponsor."

**Check:** Why define stop criteria upfront? *(It turns emotional decisions into agreed ones.)*

---

## STF-014-L07 · Demo: picking the first three teams for the golden path (15 min)
**Goal:** choose pilot teams using explicit criteria; prepares STF-014-LAB1.

**Steps**
1. Define criteria: willingness, representative stack, visible work, manager support, tolerable risk.
2. Score the 20 teams from interviews and delivery data.
3. Choose three with different stacks so lessons generalize.
4. **Planned mistake:** picking the three friendliest teams, all on one simple stack. Fix: include one harder, representative team and agree extra support.
5. Agree pilot terms: duration, support, success criteria, what the team gets.
6. Publish the selection reasons so other teams see fairness.

---

## STF-014-L08 · Demo: an adoption review that changes the plan (15 min)
**Goal:** use adoption data to adjust the roadmap; prepares STF-014-LAB1.

**Steps**
1. Present adoption data: 6 of 20 teams migrated, but three teams stalled at the secrets step.
2. Review the resistance register and survey comments.
3. Diagnose: a missing migration tool, not unwillingness.
4. **Planned mistake:** concluding that the stalled teams are resistant and pushing a mandate. Fix: test the diagnosis with the teams.
5. Change the plan: build the tool first, move the mandate date, add office hours.
6. Report the change and the reason to sponsors and teams.
