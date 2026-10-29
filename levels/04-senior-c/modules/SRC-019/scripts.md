# SRC-019 · Incident leadership — Lecture scripts

**Video:** 71 min · **Running case:** *Order Processing at 10×* — Shop Platform's order subsystem must handle a 10× growth forecast, a 99.95% availability commitment, and a 15-minute recovery objective.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRC-019-L01 · The incident commander role (12 min)
**Goal:** understand what the commander does and does not do.

**Key points**
- The incident commander (IC) coordinates: sets priorities, assigns roles, makes decisions, and keeps the picture clear.
- The IC does not debug; hands-on work goes to responders so the IC keeps the big picture.
- Typical roles: IC, operations lead (hands-on fix), communications lead, scribe, and subject experts; scale roles to severity.
- Declare early and name the commander out loud; hand over explicitly when tired.

**Show** Role card: IC | owns decisions and priorities; ops lead | drives mitigation; comms lead | updates stakeholders; scribe | keeps the timeline.

**Check:** Why should the IC not debug? *(Debugging narrows attention and nobody then holds the overall picture.)*

---

## SRC-019-L02 · Running the response (12 min)
**Goal:** keep responders focused and the response moving.

**Key points**
- Open with a short status: what we know, impact, current goal; repeat at intervals.
- Prefer mitigation (rollback, failover, load shedding, feature off) over root cause during the incident.
- Run parallel threads with clear owners; ask for hypotheses and a time box for each.
- Use one channel, a running timeline, and structured handoffs.
- Watch for fatigue and bring in relief.

**Show** A status template: impact | current hypothesis | actions in flight and owners | next checkpoint time.

**Check:** What comes first during an incident, mitigation or root cause? *(Mitigation; root cause analysis can follow.)*

---

## SRC-019-L03 · Stakeholder communication (10 min)
**Goal:** keep stakeholders informed at a steady cadence.

**Key points**
- Each update states impact, what is being done, and when the next update is, even if nothing has changed.
- Separate audiences: responders, executives, support, customers; adjust detail and avoid jargon.
- Do not guess root causes or promise times you cannot keep; say what is known and unknown.
- A comms lead frees the IC from writing updates.
- Close with a resolution message and a pointer to the follow-up.

**Show** Update template: *Status | Impact | What we are doing | Next update at HH:MM.* Example with times 30 minutes apart.

**Check:** What must every update include? *(Impact, actions, and when the next update comes.)*

---

## SRC-019-L04 · Decisions under uncertainty (10 min)
**Goal:** decide on risky mitigations with incomplete information.

**Key points**
- Compare options by reversibility, blast radius, and time to effect; prefer reversible steps first.
- State the decision, the assumption behind it, and a check that will show if it worked.
- Time-box analysis: a good decision now often beats a perfect one later.
- Involve a second opinion for risky steps; record the reasoning.
- Be willing to reverse a decision when evidence changes.

**Show** Decision table: option | reversible? | blast radius | time to effect | risk | check. Example options: fail over to the standby, roll back the release, shed 20% of traffic.

**Check:** Which option should be tried first when unsure? *(The most reversible one with limited blast radius.)*

---

## SRC-019-L05 · Facilitating postmortems (12 min)
**Goal:** run a blameless review that yields systemic actions.

**Key points**
- Blameless: assume people acted reasonably with the information they had; ask what made the action seem right.
- Build the timeline from evidence, then identify contributing factors (technical, process, organizational), not a single root cause.
- Actions: few, specific, owned, dated, and tracked to completion; prioritize ones that prevent classes of failure or speed detection.
- Share the document widely and review after a month for completion.

**Show** Postmortem outline: summary, impact, timeline, contributing factors, what went well, what was lucky, actions with owners and dates.

**Check:** What do blameless postmortems look for? *(Systemic contributing factors, not a person to blame.)*

---

## SRC-019-L06 · Demo: commanding a multi-team incident simulation (15 min)
**Goal:** command a simulated incident across several teams; prepares SRC-019-LAB1.

**Steps**
1. Declare the incident, name yourself IC, assign ops lead, comms lead, and scribe.
2. Post the first status and set a 30-minute update cadence.
3. Coordinate three teams (orders, payments, platform) with time-boxed hypotheses.
4. **Planned mistake:** the IC starts reading logs personally. Fix: delegate it to the ops lead and return to coordinating.
5. Decide on a risky mitigation (failover versus rollback) using the decision table; verify its effect.
6. Close the incident, send the resolution update, and schedule the postmortem.

**Check:** What should the IC do instead of reading logs? *(Delegate and keep coordinating.)*
