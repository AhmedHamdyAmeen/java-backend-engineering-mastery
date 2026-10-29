# SRB-011 · Cross-team design — Lecture scripts

**Video:** 86 min · **Running case:** *The FulfillCo integration* — the engineer leads the four-team program planned in SRB-P1 through delivery; role-players act as team leads, product, finance, and security.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRB-011-L01 · Designs that cross team boundaries (10 min)
**Goal:** explain why a design spanning several teams fails for different reasons than a single-team design.

**Key points**
- Inside one team, a design is decided by people who share context; across teams, each team has its own priorities, roadmap, and vocabulary.
- Most failures are at the seams: unclear owner, mismatched assumptions about an interface, or a date nobody committed to.
- The lead's job is alignment before decisions harden, not drawing the best diagram alone.
- A design is "done" when every affected team can say what they build, what they depend on, and by when.

**Show** A one-line seam list for the FulfillCo program: stock updates (warehouse to shop), shipment status (warehouse to shop), returns (shop to warehouse), identity (both). Next to each, the question "who owns this and who consumes it?"

**Check:** Where do cross-team designs usually fail? *(At the interfaces between teams: ownership, assumptions, and dates.)*

---

## SRB-011-L02 · Ownership and dependency mapping (12 min)
**Goal:** produce a map of who owns what and who waits on whom.

**Key points**
- Three lists: capabilities (what the program delivers), owners (one accountable team each), and interfaces (APIs, events, data) with a consumer and a provider.
- Draw dependencies as arrows from consumer to provider; look for chains and for one team with many inbound arrows.
- Serial chains are schedule risk: if three teams wait on one, that team is the critical path.
- Every interface gets an owner and a date before the map is called complete.

**Show** A table: interface | provider | consumers | contract status | date. Example row: *stock-changed event | warehouse team | shop orders, search | draft | agree by end of week 2.* Plus a sketch of the arrows with the busiest provider circled.

**Check:** What does a node with many inbound arrows tell you? *(It is a bottleneck and a schedule risk to be unblocked early.)*

---

## SRB-011-L03 · Inclusive design processes (10 min)
**Goal:** run a design process where every affected team shapes the decision.

**Key points**
- Identify affected teams from the dependency map, not from who is easiest to invite.
- Share a short problem statement and options before the meeting, so the meeting is for deciding, not presenting.
- Give each team a defined role: proposer, reviewer, or informed; record decisions and open questions in one place.
- Set a decision date; silence after the date counts as agreement and is recorded as such.
- Avoid "designing alone and presenting": by then, objections feel like delay.

**Show** A design-session agenda: 5 min problem, 15 min options with trade-offs, 20 min per-team constraints, 10 min decision and owners, with a pre-read link.

**Check:** Why circulate a pre-read? *(So the session spends time on decisions and constraints instead of explanations.)*

---

## SRB-011-L04 · Contract-first parallel delivery (12 min)
**Goal:** let teams build at the same time by agreeing interfaces first.

**Key points**
- Contract-first: write the API schema or event schema, agree it, then both sides build against it.
- Stubs and mocks generated from the contract let the consumer start before the provider is ready.
- Contract tests catch drift: provider and consumer both verify against the agreed schema.
- Feature flags let unfinished work merge and deploy without being visible; integration turns on in stages.
- Changes to a contract go through a visible, versioned process.

**Show** Timeline of two teams: week 1 agree the schema; weeks 2-4 provider builds, consumer builds against a stub; week 5 swap stub for the real service behind a flag. Mention schema tooling by role (OpenAPI, an event schema registry); verify tool versions before recording.

**Check:** What lets a consumer start before the provider has finished? *(A contract-derived stub or mock.)*

---

## SRB-011-L05 · Resolving cross-team conflicts (12 min)
**Goal:** settle a design disagreement between teams using explicit criteria.

**Key points**
- Most conflicts are a mix of facts, priorities, and trust; separate them.
- Agree the criteria first (for example correctness, delivery date, operational cost, reversibility), then score options against them.
- Prefer reversible decisions made quickly; escalate only after criteria and evidence are on the table.
- When escalating, bring options and a recommendation, not a complaint.
- Record the decision and the dissent so it is not reopened by accident.

**Show** Decision table: criteria with weights as columns, two options as rows, a short justification per cell, plus a line "what would change this decision".

**Check:** Why agree criteria before comparing options? *(So the choice is judged by the standard, not by who argues hardest.)*

---

## SRB-011-L06 · Demo: a four-team design session for stock synchronization (15 min)
**Goal:** facilitate a design session where four teams agree how stock is synchronized between FulfillCo and Shop; prepares SRB-011-LAB1.

**Steps**
1. Share the pre-read: problem, two options (event stream vs periodic reconciliation API), and the draft dependency map.
2. Open the session by confirming the decision to be made today and the decision date.
3. Collect each team's constraints (rate limits, data ownership, release dates) on one shared page.
4. **Planned mistake:** present a finished design as a proposal for sign-off; teams push back late. Fix: pause, return to options, and let teams amend the criteria.
5. Agree the interface, owner, and date for each seam; note one open question with an owner.
6. Send decisions and the timeline within the hour.

**Check:** How do you know the session succeeded? *(Each interface has an owner and a date, and teams confirm the written record.)*

---

## SRB-011-L07 · Demo: unblocking a team stuck on another team's API (15 min)
**Goal:** unblock a consumer team waiting on a provider's unfinished API without forcing the provider's schedule; prepares SRB-011-LAB1.

**Steps**
1. Diagnose the block: what exactly is missing, since when, and what is the consumer's slip so far.
2. Ask the provider for the minimum viable contract, not the full implementation.
3. Publish the contract and a stub; the consumer builds against it behind a feature flag.
4. **Planned mistake:** escalate to managers first, which sours the relationship. Fix: talk to the provider lead with the options, then inform managers.
5. Add a contract test and a date for replacing the stub; record the new date on the dependency map.
6. Review after a week: is the dependency chain shorter?

**Check:** What is the first thing to ask a provider who cannot deliver yet? *(The smallest contract that lets the consumer proceed.)*
