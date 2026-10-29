# STF-001 · Staff engineering role — Lecture scripts

**Video:** 100 min · **Running case:** *Platform 2.0* — the Commerce group (Shop + FulfillCo) now has about 20 product teams; delivery has slowed, every team runs its own pipelines, the same incidents repeat, and onboarding takes weeks; you join as a Staff engineer with no team of your own and a mandate to make the whole organization faster and safer.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## STF-001-L01 · What organizations hire Staff engineers to do (12 min)
**Goal:** explain why an organization of 20 teams creates a role that belongs to no single team.

**Key points**
- Some problems sit between teams: nobody owns them, so nobody fixes them.
- A Staff engineer is paid to find, frame, and solve those problems, then hand the result back to the teams.
- Output is judged by outcomes for many teams, not by the amount of code you wrote.
- The title varies by company; the work (scope beyond one team) is what matters.

**Show:** a list of five Platform 2.0 symptoms (slow delivery, duplicated pipelines, repeat incidents, slow onboarding, three identity systems) with the column "which team owns this today?" mostly empty.

**Check:** Why is a problem that no team owns a Staff-level problem? *(Only someone with cross-team scope can frame it, and no team has the mandate or time.)*

---

## STF-001-L02 · Scope, time horizon, and leverage (12 min)
**Goal:** compare Senior and Staff work on three dimensions.

**Key points**
- Scope: a Senior owns a system or team area; a Staff owns a problem across teams.
- Time horizon: Senior plans in quarters; Staff plans in years and sets direction others follow.
- Leverage: effect per unit of effort, counted across all the people your work reaches.
- Influence replaces authority: you have no reports, so decisions stick only if teams agree.

**Show:** a three-row table comparing Senior and Staff on scope, horizon, and leverage, with one Platform 2.0 example per cell.

**Check:** What does "leverage" measure? *(The outcome change across many teams for the effort you spend.)*

---

## STF-001-L03 · Staff archetypes (12 min)
**Goal:** recognize four common archetypes and pick the one an organization needs.

**Key points**
- Tech lead: guides one team or area with a broad view.
- Architect: owns direction and quality of a domain or the whole system.
- Solver: parachutes into the hardest or most urgent problems, then moves on.
- Right hand: extends a senior executive by taking on their technical load.
- Most people blend two; the organization's current pain decides which to lead with.

**Show:** a table of the four archetypes with "when it fits" and "risk", plus the Platform 2.0 verdict: architect plus solver, because direction is missing and incidents are urgent.

**Check:** Which archetype fits an executive who needs a trusted technical proxy? *(Right hand.)*

---

## STF-001-L04 · Staff engineers and managers: a partnership (12 min)
**Goal:** separate Staff and management responsibilities so they support each other.

**Key points**
- Managers own people: hiring, growth, performance, team health.
- Staff engineers own technical direction and quality across teams; they do not assign people.
- Agree explicitly who decides what, and say it out loud to the teams.
- Competing for ownership of a team's roadmap is the classic failure; share context early instead.

**Show:** a two-column responsibility sketch (manager, Staff) for one Platform 2.0 decision, "adopt a shared pipeline", showing who sponsors, who decides, who executes.

**Check:** Who owns a team member's performance review? *(The manager, not the Staff engineer; you may give input.)*

---

## STF-001-L05 · Choosing work by leverage (12 min)
**Goal:** rank candidate problems by how much they change outcomes for many teams.

**Key points**
- Score each problem: teams affected, size of the pain, cost of solving, who else could solve it.
- Prefer problems only you can unblock; delegate what others can do.
- Write down what you decline so the choice is visible.
- Revisit the ranking every quarter; leverage changes as the organization changes.

**Show:** a scoring table for four Platform 2.0 candidates (shared pipeline, incident review process, identity consolidation, a single team's refactor) with teams affected and an effort estimate.

**Check:** Why can a hard problem in one team rank low? *(It affects few teams, so leverage per effort is small.)*

---

## STF-001-L06 · Staying technical without a team (10 min)
**Goal:** keep technical credibility when you no longer ship features daily.

**Key points**
- Read code and incidents regularly; your judgment decays without contact with real systems.
- Build prototypes and tools to prove ideas, then give them away.
- Review designs and pair with teams, as teaching rather than gatekeeping.
- Write: documents are how a Staff engineer's thinking scales.

**Show:** a weekly time split, for example reading and pairing, writing, prototypes, meetings, with a note on what to protect when calendars fill.

**Check:** Why write documents instead of fixing everything yourself? *(A document reaches many teams and outlasts you; fixes reach one.)*

---

## STF-001-L07 · Demo: the first 90 days in Platform 2.0 (15 min)
**Goal:** run a worked session that turns an open mandate into a 90-day plan; prepares STF-001-LAB1.

**Steps**
1. List the stakeholders to interview: VP Engineering, six tech leads, two managers, product partners, security, SRE.
2. Run three interviews using one script: what slows you, what repeats, what would you fix with a magic wand.
3. Cluster answers into themes and count the teams naming each.
4. **Planned mistake:** jump to the theme you find most interesting (a build-system rewrite) and start prototyping. Fix: score every theme by leverage first; the rewrite affects 3 teams while incident repetition affects 12.
5. Choose the archetype (architect plus solver) and write the 90-day plan: listen (days 1-30), pick and prove (31-60), deliver and share (61-90).

---

## STF-001-L08 · Demo: saying no to a high-visibility, low-leverage request (15 min)
**Goal:** practice declining or reshaping a request from a senior leader without damaging trust; supports STF-001-LAB1.

**Steps**
1. Scenario: a director asks you to personally lead a flashy demo-day dashboard for one team.
2. Restate the underlying goal (visibility for the director's group) before answering.
3. Show the leverage table: the dashboard affects one team; your top candidate affects twelve.
4. **Planned mistake:** a flat "no, I'm busy". Fix: offer an alternative, such as a template the team can build alone, and a date when you can revisit.
5. Agree on a follow-up and record the decision so the trade-off is visible.
