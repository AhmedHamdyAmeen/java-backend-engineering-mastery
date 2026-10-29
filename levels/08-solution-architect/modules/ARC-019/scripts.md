# ARC-019 · High availability and DR — Lecture scripts

**Video:** 83 min · **Running case:** *Larkspur Retail* — a fictional 120-store retailer replacing its dated on-premises web shop with a web and mobile platform (inventory, payments, fulfillment, customer service, reporting) integrated with the existing ERP and CRM. You are the solution architect.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## ARC-019-L01 · Availability and recovery as business decisions (10 min)
**Goal:** turn business impact into RPO and RTO per capability.

**Key points**
- Availability is the share of time a capability works; recovery objectives describe the worst acceptable outage.
- RTO: how long until service is back; RPO: how much recent data may be lost.
- Each capability gets its own targets; checkout matters more than the marketing page.
- Cost grows steeply as targets tighten; the business sponsor chooses, the architect prices and explains.
- Base targets on impact: lost sales per hour, legal exposure, reputation.

**Show:** a table: capability, impact per hour, RPO, RTO, tier (checkout: tight; reporting: relaxed).

**Check:** Who decides how much downtime is acceptable? *(The business, informed by impact and cost the architect presents.)*

---

## ARC-019-L02 · Multi-AZ design (10 min)
**Goal:** design for zone failure inside a region.

**Key points**
- Run application instances in at least two or three zones behind a load balancer with health checks.
- Make services stateless so any instance can serve any request.
- Use managed data services with multi-AZ standby; state lives there.
- Size so that losing one zone still leaves enough capacity.
- Remove single points of failure: one NAT, one queue consumer, one VPN tunnel.

**Show:** a diagram: three zones, each with application instances and data nodes, load balancer spanning them; one zone shaded as failed.

**Check:** Why size for the loss of one zone? *(Otherwise the remaining zones are overloaded when one fails.)*

---

## ARC-019-L03 · DR patterns from backup-restore to active-active (14 min)
**Goal:** compare the four DR patterns by recovery speed and cost.

**Key points**
- Backup-restore: copies of data elsewhere; rebuild on disaster; lowest cost, longest recovery (hours or more).
- Pilot light: data replicated, minimal core running; scale up on disaster; faster, moderate cost.
- Warm standby: a scaled-down full copy running; scale up and switch; minutes, higher cost.
- Active-active: multiple regions serving traffic; shortest recovery, highest cost and complexity (data conflicts, consistency).
- Choose the cheapest pattern that meets the RTO and RPO.

**Show:** a four-row table: pattern, typical RTO, typical RPO, relative cost, complexity (qualitative; use Larkspur numbers in the demo).

**Check:** Which DR pattern is cheapest and slowest? *(Backup-restore.)*

---

## ARC-019-L04 · Dependencies you don't own (10 min)
**Goal:** design DR for systems outside your control.

**Key points**
- Your recovery depends on the ERP, payment provider, and identity service recovering too.
- Ask for their RTO and RPO in contracts and agreements; design to the weakest link.
- Decouple with queues and caches so you can keep working while they are down.
- Define degraded modes: accept orders and post later, switch payment methods, cache sign-in sessions.
- Document fallbacks and who triggers them.

**Show:** a dependency table: dependency, their stated RTO, our fallback, degraded behavior, owner.

**Check:** Why include the ERP in your DR plan if you do not own it? *(Your recovery cannot be faster than what it depends on without a fallback.)*

---

## ARC-019-L05 · Testing DR (10 min)
**Goal:** define DR testing and the evidence that proves recovery.

**Key points**
- An untested plan is an assumption; test restore, failover, and runbooks.
- Test types: tabletop walk-through, partial failover, full exercise, chaos-style fault injection in non-prod.
- Measure real RTO and RPO and compare with targets.
- Keep evidence: dates, results, gaps found, fixes made.
- Repeat on a schedule and after major changes.

**Show:** a test plan template: scenario, steps, success criteria, measured RTO/RPO, findings, owner, next date.

**Check:** What evidence shows a DR plan works? *(Measured results from tests against the targets.)*

---

## ARC-019-L06 · Demo: costing three DR patterns for Larkspur's checkout (15 min)
**Goal:** price three options for checkout and prepare the trade-off for the sponsor in `ARC-019-LAB1`.

**Steps**
1. Set targets with the sponsor: example checkout RTO one hour, RPO five minutes (assumptions, confirm with the business).
2. Option A, backup-restore: low monthly cost; recovery measured in many hours; misses the RTO.
3. Option B, warm standby in a second region: replicate data, run a small copy; meets the RTO; moderate cost.
4. Option C, active-active: meets any RTO; highest cost and consistency complexity.
5. **Planned mistake:** choosing active-active because "downtime is unacceptable". Fix: price it against lost-sales-per-hour and show the sponsor warm standby meets the stated targets at a fraction of the cost.
6. Present recommendation with cost ranges and the residual risk; escalate if the sponsor wants a tighter target than the budget allows.

---

## ARC-019-L07 · Demo: what happens to stores when the cloud region is down (14 min)
**Goal:** design the degraded mode so stores keep selling when the platform is unavailable.

**Steps**
1. Walk a store transaction: till, local POS, platform inventory and payment calls.
2. Identify what depends on the region: stock lookup, loyalty, online-order pickup, card authorization path.
3. Design degraded mode: till sells offline with cached prices, queues sales locally, card terminals use the provider's own offline or direct network path (confirm with the provider).
4. **Planned mistake:** assuming stores need the cloud for every sale. Fix: define offline limits (what can be sold, spending limits) and a sync-and-reconcile step on recovery.
5. Cover ERP and online orders: orders queue, pickup orders are shown as unavailable.
6. Document triggers, who decides, store communication, and reconcile steps.

---
