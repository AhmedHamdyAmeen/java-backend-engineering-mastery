# STF-018 · Incident and crisis leadership — Lecture scripts

**Video:** 94 min · **Running case:** *Platform 2.0* — the strategy, governance, and platform direction from STF-P1 must now be adopted by about 20 product teams who did not ask for them; role-players act as engineering managers, skeptical tech leads, product, finance, security, and executives.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## STF-018-L01 · When an incident becomes a crisis (10 min)
**Goal:** recognize when a normal incident needs crisis leadership.

**Key points**
- Signals: many teams affected, customer or revenue impact, external parties, regulators, or media attention.
- A crisis needs more roles: incident commander, communications lead, executive liaison.
- Declare it early; stand down easily.
- The Staff engineer's role is to lead and coordinate, not to fix every part.

**Show:** a severity ladder with criteria for "crisis" and the roles activated at each level.

**Check:** Why declare a crisis early? *(Coordination takes time to set up; late declaration wastes the first hour.)*

---

## STF-018-L02 · Leading many teams in an incident (12 min)
**Goal:** coordinate several teams without taking over their work.

**Key points**
- Set one channel, one commander, and a clear structure; assign owners per workstream.
- Hold short, regular syncs: status, hypotheses, actions, next update.
- Keep a timeline in one shared place.
- Protect the technical leads; handle executive questions through a liaison.

**Show:** a crisis room layout: commander, workstream leads (payments, platform, data), communications lead, scribe, executive liaison, with the update cadence.

**Check:** Why not fix the problem yourself? *(Leading means keeping the whole picture; hands-on work loses it.)*

---

## STF-018-L03 · Crisis communication (12 min)
**Goal:** communicate clearly with executives, customers, and regulators.

**Key points**
- Regular, honest updates with a known next-update time, even if nothing changed.
- Say what we know, what we do not, what we are doing, and when we will update.
- Different audiences need different detail; one source of truth for facts.
- Legal and regulatory obligations have deadlines; involve legal and compliance early (verify obligations for your jurisdiction).

**Show:** an update template: status, impact, what we know, what we are doing, next update time.

**Check:** What should an update say if nothing has changed? *(That nothing has changed, what is being worked on, and the next update time.)*

---

## STF-018-L04 · From postmortem to strategic action (12 min)
**Goal:** turn an incident into organization-wide improvement.

**Key points**
- Blameless review: find systemic causes, not culprits.
- Look across incidents for patterns (shared dependencies, missing tests, weak rollback).
- Strategic actions address causes across teams, have owners and funding, and are tracked.
- Local fixes alone allow the same failure elsewhere.

**Show:** a table: incident cause, local fix, systemic action, owner, funding, due date, how we will know it worked.

**Check:** Why are local fixes not enough? *(The same weakness exists in other teams and will fail again.)*

---

## STF-018-L05 · Improving the incident process (10 min)
**Goal:** improve how the organization handles incidents.

**Key points**
- Review the process after each crisis: detection, declaration, roles, communication, handover.
- Practice with game days, including executives and partners.
- Keep runbooks, contacts, and tools current.
- Track process measures: time to declare, time to first update, action completion.

**Show:** a process retrospective: what worked, what did not, three changes, owners, next game day date.

**Check:** How do you know the process improved? *(Better process measures and smoother practice runs.)*

---

## STF-018-L06 · Looking after responders (8 min)
**Goal:** protect the people who handle crises.

**Key points**
- Rotate leads and enforce rest in long incidents.
- Thank people and credit their work; do not blame.
- Watch for burnout after repeated crises.
- Include responder load in the improvement plan.

**Show:** a handover and rest schedule for a 12-hour incident with shifts and relief.

**Check:** Why enforce rest? *(Tired responders make mistakes, and burnout loses experienced people.)*

---

## STF-018-L07 · Demo: a simulated payment-provider outage on the busiest day of the year (15 min)
**Goal:** lead a multi-team simulated crisis; prepares STF-018-LAB1.

**Steps**
1. Declare the crisis, assign commander, communications lead, and workstreams.
2. Set the update cadence and the shared timeline.
3. Coordinate: fallback provider, queue and retry strategy, customer messaging.
4. **Planned mistake:** the commander starts debugging the provider integration. Fix: delegate, return to the whole picture.
5. Send executive and customer updates on schedule.
6. Stand down, hand over, and schedule the review.

---

## STF-018-L08 · Demo: presenting a crisis review to the executive team (15 min)
**Goal:** present causes, impact, and corrective actions that need funding; prepares STF-018-LAB1.

**Steps**
1. Summarize impact in business terms: revenue, customers, duration.
2. Present the timeline briefly and the systemic causes.
3. Propose strategic actions with owners, cost, and benefit.
4. **Planned mistake:** a list of local fixes. Fix: group actions by systemic cause and show cost of recurrence.
5. Ask for decisions and funding.
6. Agree how progress will be reported.
