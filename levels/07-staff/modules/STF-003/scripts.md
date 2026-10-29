# STF-003 · Architecture governance at scale — Lecture scripts

**Video:** 98 min · **Running case:** *Platform 2.0* — the Commerce group (Shop + FulfillCo) now has about 20 product teams; delivery has slowed, every team runs its own pipelines, the same incidents repeat, and onboarding takes weeks; you are a Staff engineer with no team of your own and a mandate to make the whole organization faster and safer.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## STF-003-L01 · Governance as an enabling system (12 min)
**Goal:** frame governance as a way to make good decisions fast, not to approve everything.

**Key points**
- Governance answers three questions: who decides, by what principles, and how quickly.
- At 20 teams, central approval of every design becomes the bottleneck.
- Good governance moves decisions to the lowest level that has the context.
- Its tools are principles, reference architectures, decision rights, and light review.

**Show:** a contrast diagram: a central board funnel with a queue versus a layered model where teams decide within guardrails and escalate only cross-team choices.

**Check:** Why does a review board for everything fail at scale? *(Queues grow, teams wait or bypass, and the board lacks context.)*

---

## STF-003-L02 · Principles that decide things (12 min)
**Goal:** write principles that settle real disagreements.

**Key points**
- A good principle has a trade-off built in: "prefer X over Y even when Y is faster".
- Test: could a reasonable team choose the opposite? If not, it is a platitude.
- Attach a short example and the reason for each principle.
- Keep the list to under ten; revisit when disagreements recur.

**Show:** two principle versions: vague ("build scalable systems") versus decisive ("prefer asynchronous events between domains over synchronous calls, except for user-facing reads").

**Check:** Why include the opposite option in a principle? *(It shows a real trade-off and makes the principle usable in a dispute.)*

---

## STF-003-L03 · Reference architectures (12 min)
**Goal:** give teams a proven starting point so they do not reinvent common designs.

**Key points**
- A reference architecture shows structure, components, decisions made, and decisions left open.
- Ship it with working code or templates, not only a diagram.
- Teams may deviate with a recorded reason; deviation is information.
- Assign an owner and update it as practice changes.

**Show:** an outline for a standard event-driven service: components, messaging contract, observability, deploy template, list of "you must" and "you may".

**Check:** What makes a reference architecture used rather than ignored? *(It is runnable, easy to start from, and has an owner who keeps it current.)*

---

## STF-003-L04 · Decision rights (12 min)
**Goal:** define who decides what so teams do not wait for permission.

**Key points**
- Sort decisions into team, domain, and organization levels.
- Organization-level decisions are few: shared contracts, security baselines, platform choices.
- For each, name the decider, who must be consulted, and the response time.
- Write it down and publish it; unwritten rights become politics.

**Show:** a matrix with rows (database choice for one service, public API style, identity provider, logging format) and columns (team, domain, organization, consult, target time).

**Check:** Who should decide the internal design of one team's service? *(The team; only cross-team effects go higher.)*

---

## STF-003-L05 · Measuring the cost of governance (10 min)
**Goal:** treat governance as something with a price you track.

**Key points**
- Measure review turnaround, number of items waiting, and bypass rate.
- Ask teams: how long did this decision cost you?
- Set targets, for example 90% of reviews answered in three working days.
- If a rule costs more than the risk it prevents, change or remove it.

**Show:** a small dashboard: median review time, queue size, percent of decisions made by teams alone, number of rules without an owner.

**Check:** What does a high bypass rate signal? *(The process costs too much or helps too little for teams to follow it.)*

---

## STF-003-L06 · Evolving governance as the organization grows (10 min)
**Goal:** adjust governance to the size and maturity of the organization.

**Key points**
- Light at 5 teams, structured at 20, federated at 50.
- Retire rules when automation (templates, checks in CI) can enforce them.
- Review governance yearly with team leads.
- Prefer automated guardrails over meetings.

**Show:** a timeline from "everyone talks" to "decision rights plus automated checks", with a rule moving from manual review to a pipeline check.

**Check:** Name one way to replace a manual review. *(An automated check in CI or a pre-approved template.)*

---

## STF-003-L07 · Demo: writing a decision-rights matrix with engineering managers (15 min)
**Goal:** build a decision-rights matrix collaboratively; prepares STF-003-LAB1.

**Steps**
1. List twenty recurring decisions from recent design reviews and incidents.
2. Sort them with three managers into team, domain, organization.
3. For each organization-level item, name decider, consulted parties, and a response time.
4. **Planned mistake:** putting every contentious item at the organization level. Fix: ask what the cross-team effect is; if none, return it to the team.
5. Publish the draft, test it on five sample decisions with a team lead, and fix unclear rows.

---

## STF-003-L08 · Demo: a reference architecture for event-driven services (15 min)
**Goal:** produce a reference architecture teams can start from; prepares STF-003-LAB1.

**Steps**
1. Collect how five teams already publish and consume events; note common parts.
2. Define the shared decisions: event envelope, schema versioning, retry and dead-letter rules, observability fields.
3. Mark open choices left to teams, such as the broker client library.
4. **Planned mistake:** publish only a diagram. Fix: add a template repository that builds, deploys, and emits events end to end.
5. Name an owner, a feedback channel, and a review date.
