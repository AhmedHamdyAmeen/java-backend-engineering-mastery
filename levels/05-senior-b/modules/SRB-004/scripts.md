# SRB-004 · Multi-region systems — Lecture scripts

**Video:** 94 min · **Running case:** The FulfillCo integration (Shop Platform acquires FulfillCo, a 10-year-old Java modular monolith on one PostgreSQL database; four teams integrate in real time and extract capabilities without stopping either business).
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRB-004-L01 · Why go multi-region (10 min)
**Goal:** decide whether multi-region is justified by a requirement.

**Key points**
- Valid reasons: survive a regional outage, lower latency for distant users, data residency law.
- Invalid reasons: it sounds resilient, a competitor does it.
- Costs: duplicate infrastructure, data replication, operational complexity, harder testing.
- Define RPO (data loss tolerated) and RTO (downtime tolerated) before choosing.

**Show:** a requirements card: regions lost, RPO, RTO, latency target, residency rules, budget; used to filter designs.

**Check:** Name two valid reasons for multi-region. *(Regional outage tolerance and data residency (or latency).)*

---

## SRB-004-L02 · Active-passive (12 min)
**Goal:** describe a standby region and its failover limits.

**Key points**
- Primary serves traffic; standby receives replicated data and is activated on failure.
- Variants: cold, warm, hot standby, trading cost against RTO.
- Async replication means RPO above zero; test promotion regularly.
- Failover that is never rehearsed does not work.

**Show:** a timeline: failure detected, decision, database promotion, DNS or routing switch, cache warm-up, verification; with minutes per step for RTO.

**Check:** What limits RPO in active-passive? *(Replication lag of data to the standby.)*

---

## SRB-004-L03 · Active-active and conflict handling (14 min)
**Goal:** explain what active-active really requires.

**Key points**
- Every region serves writes, so concurrent updates to the same data can conflict.
- Strategies: partition data by home region, last-write-wins, merge types (CRDTs), or avoid conflicts by design.
- Latency and consistency trade-offs are permanent, not a one-time project.
- Often only some data needs it.

**Show:** an example: order is homed in a region; any region can read; writes route to the home region; stock uses regional pools instead of one global counter.

**Check:** What is the main extra problem in active-active? *(Conflicting concurrent writes in different regions.)*

---

## SRB-004-L04 · Global traffic routing (10 min)
**Goal:** route users to healthy regions.

**Key points**
- DNS routing: simple, cached by clients, so failover is slower than the TTL suggests.
- Global load balancers or anycast give faster, health-based steering.
- Health checks must test real dependencies, not only that the process is up.
- Avoid flapping with thresholds and manual override.

**Show:** a decision table: DNS failover, global load balancer, client-side retry across endpoints, with failover time, cost, and caveats.

**Check:** Why can DNS failover be slow? *(Resolvers and clients cache records beyond the TTL.)*

---

## SRB-004-L05 · Data residency (10 min)
**Goal:** keep data in the legal region by design.

**Key points**
- Know which data classes are restricted: personal data, payments, health.
- Region-scoped stores and region-aware routing; no accidental replication across borders.
- Beware logs, backups, analytics, and support tools that copy data out.
- Prove it with data flow diagrams and automated checks.

**Show:** an EU data flow diagram with allowed flows in green and blocked ones, including backups and observability data, in red.

**Check:** Which hidden copies often break residency? *(Logs, backups, analytics exports.)*

---

## SRB-004-L06 · Selective multi-region (8 min)
**Goal:** apply multi-region only where the requirement demands it.

**Key points**
- Tier components: must survive region loss, should, and need not.
- Stateless services are cheap to replicate; state is the hard part.
- Control-plane dependencies (identity, secrets, CI) need an explicit plan.
- Write the decision per component in the topology doc.

**Show:** a component tier table for Shop and FulfillCo: checkout path tier 1, reporting tier 3, admin tools tier 2.

**Check:** Which parts are hardest to make multi-region? *(Stateful data stores.)*

---

## SRB-004-L07 · Demo: regional failover of the order path, step by step (15 min)
**Goal:** walk a failover of the order path using a runbook.

**Steps**
1. Show the order path: edge, API, order service, database, outbox, event broker.
2. Declare the incident and make the failover decision with the criteria in the runbook.
3. Promote the standby database and shift routing, watching replication lag at the moment.
4. **Planned mistake:** shift traffic before confirming promotion finished; fix by adding a verification gate to the runbook.
5. Measure achieved RPO and RTO and compare with targets.

Prepares SRB-004-LAB1.

---

## SRB-004-L08 · Demo: the hidden single-region dependency that breaks failover (15 min)
**Goal:** find the dependency that stays in the failed region.

**Steps**
1. Map dependencies of the order path beyond the obvious database.
2. Fail the primary region in a test and see the standby fail to start.
3. Discover the secrets manager and identity provider live only in the primary region.
4. **Planned mistake:** assume managed services are global; fix by reading each service's regional scope and adding replicas.
5. Add a dependency checklist and a game-day test to the topology review.

Prepares SRB-004-LAB1.

---
