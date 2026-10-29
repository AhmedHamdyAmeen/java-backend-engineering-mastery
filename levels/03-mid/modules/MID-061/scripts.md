# MID-061 · Microservices introduction — Lecture scripts

**Video:** 50 min · **Analogy used throughout:** one big restaurant kitchen versus several food stalls: stalls work independently but need coordination, delivery, and more staff.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-061-L01 · What microservices promise (8 min)
**Goal:** state the real benefits.

**Key points**
- A microservice is a small, independently deployable service that owns its data and one business capability.
- Independent deployment: ship `payments` without redeploying `catalog`.
- Independent scaling: scale only the hot part, if load data shows which.
- Team ownership: a team owns a service end to end.
- Technology choice per service, within limits.
- These benefits mostly matter with many teams or very different load profiles.

**Show:** a table of promise versus the condition under which it really appears.

**Check:** Name two benefits of microservices. *(For example independent deployment and independent scaling or ownership.)*

---

## MID-061-L02 · What they cost (12 min)
**Goal:** list the costs before choosing.

**Key points**
- Network: calls can be slow, fail, or time out (MID-023); every call needs timeouts and retries.
- Consistency: no cross-service ACID transaction; use sagas and eventual consistency (MID-030, MID-031).
- Operations: many deployments, logs, metrics, traces, and configs to run and monitor.
- Testing and debugging span services; local development gets heavier.
- Data: no joins across services; reporting needs extra work.
- Team cost: needs platform skills and mature automation.

**Show:** a before/after: one method call `inventory.reserve(...)` becomes an HTTP call plus timeout, retry, idempotency, and a failure path.

**Check:** Which cost replaces a database transaction across services? *(Sagas and eventual consistency.)*

---

## MID-061-L03 · The distributed monolith (8 min)
**Goal:** spot the worst of both worlds.

**Key points**
- A distributed monolith has separate deployments but cannot change or deploy independently.
- Signs: lockstep releases, shared database, long synchronous call chains, a shared "common" library with domain types.
- It keeps the monolith's coupling and adds network costs.
- Usual causes: boundaries by technical layer or per entity, and shared data.
- Test: can you deploy one service alone, at any time, without breaking another?

**Show:** a diagram of four services all reading one `shop` database, with a release train arrow.

**Check:** What is the quick test for a distributed monolith? *(Cannot deploy one service independently.)*

---

## MID-061-L04 · Criteria for extracting a service (10 min)
**Goal:** apply concrete criteria, not fashion.

**Key points**
- Extract when there is a real driver: independent scaling backed by load data, a different release cadence, a team boundary, a different availability or compliance need.
- Check readiness: clear bounded context, owned data, a stable API, few callers.
- Check capability: monitoring, CI/CD, and on-call exist.
- "Not extracting" is a valid decision; modular monolith first (MID-059).
- Record the decision as an ADR with the criteria and the date to revisit.

**Show:** a scoring table: driver, data ownership, coupling, team, operational readiness, each yes/no/unknown.

**Check:** Is "keep it in the monolith" an acceptable outcome? *(Yes, when justified.)*

---

## MID-061-L05 · Demo: walking through the decision for each Shop module (12 min)
**Goal:** run the criteria table on Shop. Prepares `MID-061-LAB1`.

**Steps**
1. List Shop modules: `catalog`, `orders`, `inventory`, `payments`, `notifications`.
2. Gather evidence: request rates, deploy frequency, team ownership, data coupling.
3. Score each module on the criteria table.
4. **Planned mistake:** extract `catalog` "because it gets the most reads" without load numbers. Point out that a cache or a read replica may solve it; mark the criterion "unknown, measure first".
5. Conclude: for example `payments` (different compliance and provider failures) and `inventory` (different scaling and consistency needs) are candidates; `catalog` stays.
6. Write the result as an ADR draft with context, decision, consequences, and a review date.

---
