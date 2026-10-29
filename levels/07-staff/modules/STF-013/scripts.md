# STF-013 · Cross-team programs — Lecture scripts

**Video:** 96 min · **Running case:** *Platform 2.0* — the strategy, governance, and platform direction from STF-P1 must now be adopted by about 20 product teams who did not ask for them; role-players act as engineering managers, skeptical tech leads, product, finance, security, and executives.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## STF-013-L01 · Programs vs projects (10 min)
**Goal:** tell when work needs program management rather than a single team plan.

**Key points**
- A project has one team and one deliverable; a program coordinates many teams toward one outcome.
- Programs fail on coordination, not on code: unclear owners, hidden dependencies, no shared view.
- The outcome is a changed state (all 20 teams on the new pipelines), not a list of tasks.
- Program work is a real job; plan time for it.

**Show:** a one-page program charter: outcome, scope, teams, sponsor, end date, how success is measured.

**Check:** What does a program coordinate that a project does not? *(Work and dependencies across several independent teams.)*

---

## STF-013-L02 · Milestones that show progress (12 min)
**Goal:** define milestones that prove progress, not activity.

**Key points**
- A milestone is a verifiable state ("5 teams deploy through the new pipeline in production").
- Keep them small enough to finish in one or two cycles.
- Each has one owner and a done-check anyone can run.
- Order them to learn early: pilot first, scale after.

**Show:** milestone list for the rollout: M1 pilot team live, M2 five teams, M3 ten teams plus support model proven, M4 legacy pipeline switched off, each with owner and check.

**Check:** What makes a milestone useful? *(It is verifiable, owned, and shows real progress.)*

---

## STF-013-L03 · Dependencies and the critical path (12 min)
**Goal:** find what limits the program's finish date.

**Key points**
- List dependencies between teams and on shared services (identity, secrets, artifact store).
- The critical path is the chain that sets the end date; a delay there delays everything.
- Protect it: staff it first, clear its blockers daily.
- Revisit the map every cycle; it changes.

**Show:** a dependency diagram: secrets-service change (platform) before pipeline template v2 before teams migrate; highlight the critical chain.

**Check:** What happens if a non-critical task slips slightly? *(Usually nothing for the end date; critical-path slips move the whole program.)*

---

## STF-013-L04 · Accountability without authority (12 min)
**Goal:** get commitments kept when you are nobody's manager.

**Key points**
- Make commitments explicit, written, and visible: who, what, by when.
- Agree them with the team's manager as well as the engineer.
- Use a regular, short program review where status is data, not opinion.
- Raise misses early and privately first; recognize delivery publicly.

**Show:** a program board with owner, date, and red/amber/green defined by rules (for example, red = critical-path date at risk).

**Check:** Why involve the engineer's manager in the commitment? *(They control priorities; without them the commitment competes silently with other work.)*

---

## STF-013-L05 · Escalation done well (10 min)
**Goal:** escalate early, with options, and without blame.

**Key points**
- Escalate when the critical path is at risk and you cannot resolve it at your level.
- Bring facts, impact, two or three options, and your recommendation.
- Warn the other party first; no surprises.
- Escalation is a normal tool, not a failure.

**Show:** a one-page escalation note: situation, impact on the date, options (reassign, descope, delay), recommendation, decision needed by when.

**Check:** What should every escalation include besides the problem? *(Options, a recommendation, and the decision needed with a date.)*

---

## STF-013-L06 · Working with technical program managers (10 min)
**Goal:** split work well with a TPM.

**Key points**
- The TPM runs schedule, dependencies, and communication; you own technical direction and risk.
- Share the plan and the risk register; decide who calls which meeting.
- Give the TPM honest estimates and early warnings.
- Without a TPM, you cover these jobs and need to budget the time.

**Show:** a two-column split of responsibilities for the Platform 2.0 rollout.

**Check:** Who owns the technical risks of the program? *(The Staff engineer, with the TPM tracking them.)*

---

## STF-013-L07 · Demo: a program review for the migration of 20 teams' pipelines (15 min)
**Goal:** run a 30-minute program review that finds problems early; prepares STF-013-LAB1.

**Steps**
1. Prepare the dashboard: milestone status, burndown of teams migrated, top risks.
2. Start with the critical path and any red items; skip green ones.
3. For each red, name owner, cause, and next action with date.
4. **Planned mistake:** the review turns into a long status read-out by every team. Fix: status is read beforehand; the meeting is only for decisions and blockers.
5. Record decisions and actions, update the plan the same day.
6. Send a short summary to sponsors.

---

## STF-013-L08 · Demo: escalating a blocked dependency with options (15 min)
**Goal:** unblock a stalled secrets-service change owned by another department; prepares STF-013-LAB1.

**Steps**
1. Quantify the impact: the change blocks 12 teams and moves M3 by six weeks.
2. Talk to the owning team's lead first; understand their constraints.
3. Draft options: borrow two engineers, reduce scope to what the rollout needs, or move M3.
4. **Planned mistake:** writing the escalation as "team X is blocking us". Fix: describe the effect on the shared outcome and ask for a decision.
5. Present to the common manager or sponsor with a recommendation.
6. Record the decision and follow up on the agreed date.
