# ARC-031 · Resilience architecture — Lecture scripts

**Video:** 58 min · **Running case:** *Larkspur Retail* — a fictional 120-store retailer replacing its dated on-premises web shop with a web and mobile platform (inventory, payments, fulfillment, customer service, reporting) integrated with the existing ERP and CRM. You are the solution architect.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## ARC-031-L01 · Resilience beyond infrastructure (10 min)
**Goal:** show that resilience is about business processes, not only servers.

**Key points**
- Redundant servers do not help if the payment provider, ERP, or carrier API is down.
- Resilience means the business keeps doing its important things, possibly in a reduced way.
- Start from critical business processes (sell in store, take web orders, ship, refund) and ask what each depends on.
- Targets (recovery time, recovery point) come from the business impact, not from technology preference.

**Show:** a dependency map from "sell in a store" down to till software, store network, payment terminal, provider, platform, ERP.

**Check:** A process depends on a provider with 99.9 percent availability. Is the process 99.9 percent available? *(No. Dependencies multiply; the process is usually lower unless a degraded mode exists.)*

---

## ARC-031-L02 · Failure scenarios for enterprise solutions (12 min)
**Goal:** enumerate failure scenarios including third-party and on-premises dependencies.

**Key points**
- Scenario types: component failure, dependency outage, slow dependency, data corruption, bad deployment, region loss, human error, cyberattack.
- Include on-premises systems: the ERP has maintenance windows and capacity limits.
- Each scenario states trigger, impact on processes, detection, and expected response.
- Rate by likelihood and business impact to choose where to invest.

**Show:** a scenario catalog row: "Payment provider unavailable for 30 min" → impact: web and store card sales → detection: authorization error rate → response: secondary provider or offline mode.

**Check:** Why include the slow dependency, not only the dead one? *(Slowness exhausts threads and queues and often does more damage than a clean failure.)*

---

## ARC-031-L03 · Fault isolation and degradation (12 min)
**Goal:** design so a failing component degrades one feature rather than the business.

**Key points**
- Isolation tools: timeouts, circuit breakers, bulkheads (separate resource pools), queues that absorb bursts.
- Degraded modes: show cached prices, disable recommendations, accept orders and post to the ERP later.
- Decide per feature which are essential and which can switch off.
- Make the degraded state visible to staff and customers where it matters.

**Show:** a table: dependency, failure, degraded behavior, user message. ERP down: orders accepted, stock shown as "last known", postings queued.

**Check:** What is a degraded mode? *(A reduced but working behavior used while a dependency is unavailable.)*

---

## ARC-031-L04 · Business continuity planning (10 min)
**Goal:** write continuity plans for processes when systems are unavailable.

**Key points**
- A plan names the process, trigger, manual or offline procedure, owner, communication, and recovery steps.
- People need practice: stores must know the offline procedure before the outage.
- Plan the catch-up: reconcile offline sales, deduplicate, resolve conflicts.
- Resilience tests prove the plan: failover drills, dependency kill tests, game days, restore tests.

**Show:** a one-page continuity card for a store: "central platform unreachable" → sell offline with the terminal's stored mode within agreed limits (verify limits with the payment provider) → record sales → upload on reconnection.

**Check:** What proves a continuity plan works? *(A test or drill that exercises it and records the result.)*

---

## ARC-031-L05 · Demo: keeping 120 stores selling when the central platform is down (14 min)
**Goal:** worked session designing offline store trading; prepares ARC-031-LAB1.

**Steps**
1. List what a store needs to sell: product and price data, tax rules, payment, receipt, stock decrement.
2. Design the store edge: local cache of catalog and prices, local queue of sales, card terminals with provider offline mode within limits.
3. Define limits: maximum offline period and value, returns allowed or blocked, loyalty points deferred.
4. **Planned mistake:** assume the store link is always up because it is redundant. Fix: treat "platform unreachable" as a normal scenario with a tested degraded mode.
5. Design reconnection: replay the queue with idempotent sale IDs, reconcile stock and payments, and define resilience tests (cut the link in a pilot store).
