# SRC-001 · Requirements engineering — Lecture scripts

**Video:** 81 min · **Running case:** *Order Processing at 10×* — Shop Platform's order subsystem must handle a 10× growth forecast, a 99.95% availability commitment, and a 15-minute recovery objective.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRC-001-L01 · Why systems fail at the requirements stage (10 min)
**Goal:** show that most expensive failures start with a requirement nobody wrote down or tested.

**Key points**
- Stakeholders state goals ("handle 10×"), not requirements ("p99 checkout under 800 ms at 600 orders/s").
- A missing requirement is found late and costs a redesign; a wrong one costs a rebuild.
- Typical gaps: nonfunctional targets, failure behavior, data retention, who decides.
- Designing before asking locks in answers to questions never put to the business.

**Show:** a timeline of the order subsystem: goal "10× growth" in the board deck, then three architectures that each silently assume a different meaning of "10×".

**Check:** Why is "handle 10× growth" not yet a requirement? *(It has no measure, scope, or time frame; different people read it differently.)*

---

## SRC-001-L02 · Functional vs nonfunctional requirements (10 min)
**Goal:** separate what the system does from how well it must do it.

**Key points**
- Functional: behavior ("a customer can cancel an order before shipment").
- Nonfunctional (quality): availability, latency, durability, security, operability.
- Nonfunctional requirements drive architecture far more than functional ones.
- Each needs a measure and a condition, otherwise it is a wish.

**Show:** a two-column table for orders: "cancel before shipment" (functional) beside "order confirmation survives loss of one availability zone" (nonfunctional, measurable).

**Check:** Which kind of requirement usually shapes the architecture most? *(Nonfunctional.)*

---

## SRC-001-L03 · Constraints and assumptions (10 min)
**Goal:** record what is fixed and what is merely believed.

**Key points**
- Constraint: a limit we cannot choose (budget, PostgreSQL as the system of record, regulation).
- Assumption: something we believe but have not verified (peak is 3× average).
- Requirement: something the solution must satisfy, owned by a stakeholder.
- Every assumption gets an owner, a way to verify it, and a date.

**Show:** three-column register for the order subsystem with one row each, e.g. assumption "Black Friday peak is 6× daily peak", owner Finance, verify with last year's data.

**Check:** Which of the three can later turn out false and silently invalidate the design? *(Assumptions, if not recorded and verified.)*

---

## SRC-001-L04 · Stakeholder interviews that surface real needs (12 min)
**Goal:** run an interview that turns goals into testable needs.

**Key points**
- Ask about outcomes and consequences: "What happens if checkout is down 10 minutes at noon?"
- Use numbers and examples; ask "how would we know?" for every adjective.
- Interview product, finance, and operations separately; they want different things.
- Replay what you heard and write it down within a day.

**Show:** a question list: cost of one lost order, acceptable downtime per month, who is paged, what may degrade first.

**Check:** What question converts "fast" into something testable? *(Ask for the user action, the number, and the percentile: "how fast, for what action, for how many users?")*

---

## SRC-001-L05 · Quality-attribute scenarios (14 min)
**Goal:** write a nonfunctional requirement as a six-part scenario.

**Key points**
- Parts: source, stimulus, environment, artifact, response, response measure.
- The measure is the testable part: a number, a percentile, a time window.
- One scenario covers one attribute and one situation; write many.
- A scenario can be turned into a load test, a game day, or a monitoring alert.

**Show:** "During Black Friday peak (environment), 600 customers/s (source) submit orders (stimulus) to the order service (artifact); orders are accepted (response) with p99 under 800 ms and under 0.1% errors (measure)."

**Check:** Which part makes a scenario testable? *(The response measure.)*

---

## SRC-001-L06 · Conflicts and trade-off conversations (10 min)
**Goal:** surface conflicting requirements and get a decision from an owner.

**Key points**
- Typical conflicts: availability vs cost, latency vs consistency, speed of delivery vs resilience.
- Do not resolve a conflict silently in code; list it with both owners.
- Present options with consequences in each stakeholder's language (money, risk, time).
- Record the decision, owner, and review date.

**Show:** a conflict table: "99.95% availability" (operations) vs "no extra infrastructure budget" (finance): option A second region, option B multi-AZ plus faster recovery, with cost and risk per option.

**Check:** Who should resolve a requirements conflict? *(The accountable stakeholders, informed by the engineer's options; not the engineer alone.)*

---

## SRC-001-L07 · Demo: turning "orders must never be lost" into testable requirements (15 min)
**Goal:** work the vague sentence into scenarios, constraints, and a conflict list; prepares SRC-001-LAB1.

**Steps**
1. Start from the sentence and ask the interview questions: lost where, by whom, for how long?
2. Split it: "accepted orders are durable" (RPO) versus "orders are visible within 2 s" (latency) versus "no duplicate charge".
3. Write three scenarios with measures; define "lost" as accepted-but-not-recoverable.
4. Record assumptions (single-region failure is the worst case) and constraints (PostgreSQL stays).
5. **Planned mistake:** accept "zero loss" as written. Fix: show that it implies synchronous multi-site writes and price it; negotiate "no loss of acknowledged orders after a single-AZ failure".
6. List the conflict (zero loss vs latency budget) with owners.
