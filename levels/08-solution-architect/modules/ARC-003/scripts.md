# ARC-003 · Requirements discovery — Lecture scripts

**Video:** 93 min · **Running case:** *Larkspur Retail* — a fictional 120-store retailer replacing its dated on-premises web shop with a web and mobile platform (inventory, payments, fulfillment, customer service, reporting) integrated with the existing ERP and CRM. You are the solution architect.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## ARC-003-L01 · Discovery as the architect's first deliverable (8 min)
**Goal:** treat discovery as a planned deliverable, not a warm-up.

**Key points**
- Discovery output: requirements baseline, constraints, assumptions, stakeholder decisions, open questions.
- Skipped or rushed discovery shows up later as rework and scope fights.
- The architect asks different questions from a product owner: quality, integration, data, failure.
- Done means signed off by owners, not merely written.

**Show:** a Larkspur discovery plan outline: objectives, participants, sessions, outputs, sign-off date.

**Check:** What marks discovery as done? *(A baseline accepted by the owners, with open items owned and dated.)*

---

## ARC-003-L02 · Planning workshops and interviews (12 min)
**Goal:** choose the right format and prepare it.

**Key points**
- Interviews for sensitive or individual views; workshops for cross-team agreement and conflicts.
- Prepare: objective, agenda, participants, pre-reads, the artifacts to produce.
- Invite decision-makers for decision topics; send questions in advance.
- Record outputs the same day and confirm back.

**Show:** a one-page workshop plan for Larkspur: 3 hours, store operations, e-commerce, finance, IT, security; agenda blocks for goals, journeys, quality, constraints, conflicts.

**Check:** When is a workshop better than separate interviews? *(When people must agree or expose conflicts together.)*

---

## ARC-003-L03 · Facilitation techniques (12 min)
**Goal:** run a session that surfaces real requirements.

**Key points**
- Open with goals and ground rules; use a visible parking lot for off-topic items.
- Ask "what happens if this fails?" and "how would we know it works?" rather than "what do you want?".
- Balance voices: invite quiet people, time-box dominant ones.
- Use artifacts live (journey maps, scenario cards) so everyone sees what is captured.

**Show:** a facilitation script excerpt: opening statement, three probing questions, a technique for a stalled argument (write both positions, ask what evidence would decide).

**Check:** Why ask "what happens if this fails?" *(It reveals priorities and quality needs that a wish list hides.)*

---

## ARC-003-L04 · Functional requirements and journeys (10 min)
**Goal:** capture what the system must do as use cases or user journeys.

**Key points**
- A user journey follows one actor through steps toward a goal across channels.
- A use case: actor, goal, main flow, alternative and failure flows.
- Keep them at the level the business can validate; avoid design details.
- Give each a stable ID for traceability.

**Show:** journey FR-014 "Customer returns an online order to a store": steps, system touch points, failure flow (item not in order history), linked capabilities.

**Check:** Why include failure flows? *(Real behavior and risk live there, and they drive design.)*

---

## ARC-003-L05 · Nonfunctional requirements that can be tested (12 min)
**Goal:** turn "fast and secure" into measurable quality scenarios.

**Key points**
- Scenario parts: source, stimulus, environment, response, response measure.
- Cover performance, availability, security, privacy, operability, scalability, data retention.
- Use the business: peak days, revenue per minute of downtime, regulatory duties.
- If it cannot be tested or measured, it is not yet a requirement.

**Show:** "On a promotion day at peak (environment), 2,000 shoppers per minute (stimulus) browse the catalog; 95% of product pages return within 1.5 s (measure)". Rewrite "must be secure" as a named threat with a response.

**Check:** What makes "must be fast" insufficient? *(No measure, load, or condition.)*

---

## ARC-003-L06 · Constraints, assumptions, and conflicts (10 min)
**Goal:** separate fixed limits from beliefs and resolve clashes.

**Key points**
- Constraints: budget, regulation, existing systems, skills, timeline.
- Assumptions: believed but unverified; give each an owner and a check date.
- Conflicts: write both sides, the trade-off, options, and the decision owner.
- The architect brings options and consequences; the owner decides.

**Show:** a register with rows for constraint (ERP stays system of record for finance through year one), assumption (store networks handle handheld scanning), conflict (real-time stock versus ERP batch updates).

**Check:** Who decides a conflict between two business requirements? *(The accountable owner, informed by the architect's options.)*

---

## ARC-003-L07 · Demo: facilitating Larkspur's discovery workshop (15 min)
**Goal:** run a role-played workshop and capture a baseline. Prepares `ARC-003-LAB1`.

**Steps**
1. Open: goals, ground rules, parking lot, outputs expected.
2. Walk the three highest-value journeys with store operations and e-commerce; capture steps and failures.
3. Probe quality: peak load, downtime cost, payment rules with finance and security.
4. Record constraints and assumptions live on a shared screen.
5. **Planned mistake:** the head of e-commerce dominates and priorities follow their view. Fix: pause, rank requirements in a silent round with all participants, and show the result.
6. Close: read back decisions, owners, and open items; assign traceability IDs.

**Check:** How do you rebalance a dominated workshop? *(Use a silent individual ranking round and make results visible.)*

---

## ARC-003-L08 · Demo: resolving "real-time stock" vs "keep the ERP as master" (14 min)
**Goal:** make a conflict explicit, offer options, and get a decision.

**Steps**
1. State both requirements: stores want stock visible in seconds; finance wants the ERP to remain the master for inventory value.
2. Surface the underlying needs: avoid overselling; keep an audited ledger.
3. Draft options: A near-real-time inventory service fed by store events with nightly ERP reconciliation; B direct ERP calls (limited by ERP API capacity); C full inventory replacement.
4. Compare cost, risk, time, and fit to both needs; recommend A with explicit safety stock.
5. **Planned mistake:** the architect picks an option silently and moves on. Fix: record the trade-off and take it to the named decision owner (CIO with finance) for a decision.
6. Update the baseline with the decision and affected requirement IDs.

**Check:** Why separate the stated demand from the underlying need? *(Different options can satisfy the need that no single demand allows.)*
