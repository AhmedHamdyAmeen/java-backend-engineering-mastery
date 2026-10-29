# SRC-002 · Quality attributes — Lecture scripts

**Video:** 89 min · **Running case:** *Order Processing at 10×* — Shop Platform's order subsystem must handle a 10× growth forecast, a 99.95% availability commitment, and a 15-minute recovery objective.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRC-002-L01 · Quality attributes drive architecture (10 min)
**Goal:** explain why quality attributes, not features, pick the architecture.

**Key points**
- Two systems with the same features can have very different structures because of their quality targets.
- Each attribute pushes the design a direction: availability toward redundancy, latency toward fewer hops.
- Attributes compete for the same budget, time, and complexity.
- Name the few that matter most; you cannot maximize all.

**Show:** order subsystem with one feature set and two target sets: "internal tool, 99%" versus "customer checkout, 99.95%", sketched as two different deployments.

**Check:** Why can't every attribute be top priority? *(They trade off and share a limited budget.)*

---

## SRC-002-L02 · Availability and reliability, measured (12 min)
**Goal:** define availability and reliability with a measurement rule.

**Key points**
- Availability: share of time (or requests) the service works; reliability: how long it works without failing and how correctly.
- 99.95% monthly is about 22 minutes of allowed downtime; verify the arithmetic for your window.
- Define "up": which endpoint, which probe, which errors count, which maintenance is excluded.
- Serial dependencies multiply: two 99.9% components in series give roughly 99.8%.
- Distinguish MTTR (recovery) from MTBF (failure interval); recovery speed is often cheaper to improve.

**Show:** a table of availability targets and allowed monthly downtime, plus a measurement definition for checkout.

**Check:** What is missing from "we need 99.95%"? *(The measurement definition: what counts as up, where measured, over what window.)*

---

## SRC-002-L03 · Scalability and elasticity (10 min)
**Goal:** tell scalability from elasticity and say what limits each.

**Key points**
- Scalability: capacity grows with added resources at acceptable cost.
- Elasticity: capacity follows load up and down automatically.
- Limits: shared state, single writers, locks, the database; stateless tiers scale easily.
- State the scaling target with a dimension: orders per second, data size, tenants.

**Show:** a diagram of the order path with the stateless API tier scaling out and the single PostgreSQL primary marked as the limit.

**Check:** What usually limits horizontal scaling of an order system? *(Shared state such as the single write database.)*

---

## SRC-002-L04 · Maintainability and operability (10 min)
**Goal:** make "easy to change" and "easy to run" measurable.

**Key points**
- Maintainability: lead time to change, defect rate, onboarding time, size of blast radius of a change.
- Operability: time to detect, diagnose, and recover; quality of runbooks and dashboards.
- Both degrade silently; complexity is the usual cause.
- Treat on-call load as a design input.

**Show:** two scenarios: "a new engineer ships a small change in the order module within one week" and "an on-call engineer identifies the failing dependency within 10 minutes".

**Check:** Name one measure of operability. *(Time to detect, time to diagnose, or time to recover.)*

---

## SRC-002-L05 · Security as a quality attribute (8 min)
**Goal:** treat security as scenarios with measures, not a checklist.

**Key points**
- Threats become scenarios: source, stimulus, response, measure.
- Properties: confidentiality, integrity, availability, accountability.
- Security trades with usability, latency, and cost; decide explicitly.
- Tactics: authenticate, authorize, limit exposure, detect, recover.

**Show:** "An attacker replays a stolen token (stimulus); the gateway rejects it after expiry; the attempt is logged and alerts within 1 minute."

**Check:** What turns a security worry into a design input? *(A scenario with a measurable response.)*

---

## SRC-002-L06 · Utility trees and prioritization (12 min)
**Goal:** build a utility tree and rank its leaves.

**Key points**
- Root "utility"; second level the attributes; leaves concrete scenarios.
- Rank each leaf by business importance and technical difficulty (High/Medium/Low).
- High importance plus high difficulty leaves are where design effort goes.
- Run it with stakeholders; the tree is a negotiation tool.

**Show:** a tree with leaves such as "failover under 15 minutes (H,H)" and "release in under one hour (M,L)".

**Check:** Which leaves deserve the most design attention? *(High importance and high difficulty.)*

---

## SRC-002-L07 · Tactics catalog (12 min)
**Goal:** map each attribute to the tactics that achieve it.

**Key points**
- Availability: redundancy, health checks, failover, retries, graceful degradation.
- Latency/scalability: caching, partitioning, asynchronous work, load shedding.
- Maintainability: modularity, tests, small interfaces; operability: observability, runbooks.
- Security: least privilege, input validation, audit trail.
- Every tactic has a cost and side effects; record them.

**Show:** a table with attribute, tactic, cost, and side effect, e.g. caching, lower latency, stale reads.

**Check:** What must be recorded beside a tactic? *(Its cost and side effects.)*

---

## SRC-002-L08 · Demo: building the utility tree for the order subsystem (15 min)
**Goal:** build and prioritize the tree with role-played stakeholders; prepares SRC-002-LAB1.

**Steps**
1. Draft attributes from the SRC-001 requirements and add leaf scenarios.
2. Rate importance with the product owner and difficulty with the platform lead.
3. **Planned mistake:** product rates everything High. Fix: force-rank using a fixed budget of votes and ask what to sacrifice first.
4. Pick the top three attributes (for example availability, latency under peak, operability) and justify them.
5. Attach tactics per leaf with their costs.
6. Record disagreements as open conflicts with owners.
