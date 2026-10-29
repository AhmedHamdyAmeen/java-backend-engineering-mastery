# MID-050 · Incident handling — Lecture scripts

**Video:** 60 min · **Analogy used throughout:** a fire brigade: first put out the fire and protect people, later investigate the cause and improve the building code. Running project: Shop.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-050-L01 · Anatomy of an incident (8 min)
**Goal:** know the phases of an incident.

**Key points**
- Phases: detect, triage, mitigate, resolve, learn.
- Detection should come from alerts, not customers; track time to detect, to mitigate, and to resolve.
- An incident is anything that harms users beyond an agreed threshold, not only total outages.
- Calm, written process beats heroics.

**Show:** timeline: alert fires → acknowledged → severity set → mitigation → recovery → postmortem.

**Check:** Name the five phases. *(Detect, triage, mitigate, resolve, learn.)*

---

## MID-050-L02 · Triage and severity (10 min)
**Goal:** assess impact and set severity quickly.

**Key points**
- First questions: who is affected, how badly, since when, is it getting worse?
- Severity levels with plain definitions: Sev1 checkout down for everyone; Sev2 a major feature degraded; Sev3 minor, workaround exists.
- Escalate early; raising severity later is cheaper than discovering the delay.
- Check recent changes: deploys, config, flags, dependencies.

**Show:** severity table with example, response expectation, and who is paged.

**Check:** When should you escalate? *(Early, when impact is high or unclear.)*

---

## MID-050-L03 · Mitigate first (10 min)
**Goal:** restore service before finding the root cause.

**Key points**
- Mitigation options in order of speed and safety: rollback, disable a feature flag, scale or restart, fail over, shed load.
- Root cause analysis waits until users are no longer hurt.
- Keep evidence (logs, dashboards, heap dumps) before restarting if it is cheap to do so.
- Verify the mitigation worked using the SLI, not a feeling.

**Show:** decision list: "recent deploy? roll back. New feature? flag off. Load spike? scale or limit."

**Check:** Why not debug root cause first? *(Users stay harmed while you investigate.)*

---

## MID-050-L04 · Roles and communication (8 min)
**Goal:** run the incident as a small team.

**Key points**
- Incident commander coordinates and decides; operators investigate and act; a communicator updates stakeholders and users.
- One channel as the source of truth; keep a timeline with times and actions.
- Status updates on a schedule (for example every 30 minutes): impact, what we know, what we do, next update.
- Handoffs are explicit.

**Show:** a status update template with the four fields.

**Check:** What does the incident commander do? *(Coordinates and decides, rather than debugging.)*

---

## MID-050-L05 · Blameless postmortems (10 min)
**Goal:** write a postmortem that improves the system.

**Key points**
- Blameless: assume people acted reasonably with the information they had; ask what let the failure happen.
- Contents: summary, impact, timeline, root cause and contributing factors, what went well, what went badly, action items.
- Action items have owners and due dates and are tracked to completion.
- Never name a person as the cause.

**Show:** an action item: "Add alert on payment retries > 5%; owner: payments team; due 2 weeks; ticket linked."

**Check:** Why blameless? *(People report problems openly, and the fixes target the system.)*

---

## MID-050-L06 · Demo: a simulated incident, start to finish (14 min)
**Goal:** run an incident with the full format. Prepares `MID-050-LAB1`.

**Steps**
1. Alert fires during a load test: checkout error rate high. Acknowledge and open the incident channel.
2. Triage: impact (about 30% of checkouts failing), set Sev2, check the latest deploy.
3. **Planned mistake:** start reading code to find the bug; the timeline shows 15 minutes lost. Switch to mitigation: roll back the deploy.
4. Verify recovery on the checkout SLI; post a status update.
5. Write the timeline from the channel.
6. Write the postmortem draft with contributing factors and action items.
