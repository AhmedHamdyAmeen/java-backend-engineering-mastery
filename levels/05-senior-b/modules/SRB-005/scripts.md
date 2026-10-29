# SRB-005 · High-availability design — Lecture scripts

**Video:** 86 min · **Running case:** The FulfillCo integration (Shop Platform acquires FulfillCo, a 10-year-old Java modular monolith on one PostgreSQL database; four teams integrate in real time and extract capabilities without stopping either business).
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRB-005-L01 · Availability math (12 min)
**Goal:** compute availability of systems from their parts.

**Key points**
- Serial dependencies multiply: two 99.9% services in series give about 99.8%.
- Parallel redundancy improves: 1 - (1-a)^n assuming independent failures.
- Independence is rarely true; shared causes (deploys, config, region) break the math.
- Convert to downtime: 99.95% is about 22 minutes per month; verify figure before recording.

**Show:** a worked calculation: checkout depends on identity (99.95%), orders DB (99.99%), payments (99.9%), FulfillCo stock API (99.9%); product of those; then add a cache fallback.

**Check:** What is the availability of two 99.9% services in series? *(About 99.8%.)*

---

## SRB-005-L02 · Redundancy and hidden SPOFs (10 min)
**Goal:** find single points of failure beyond servers.

**Key points**
- Redundancy at each layer: instances, zones, databases, networks, DNS.
- Hidden SPOFs: a shared config store, a certificate expiry, one CI pipeline, one engineer.
- Redundancy must be tested; unused failover paths rot.
- Check shared fate: two replicas on one host are one failure.

**Show:** a layered checklist with questions per layer and a column for evidence (test date).

**Check:** Name a hidden SPOF that is not a server. *(An expiring certificate, shared config, or a single identity provider.)*

---

## SRB-005-L03 · Load shedding and admission control (12 min)
**Goal:** stay useful under overload by rejecting work on purpose.

**Key points**
- Overload without limits makes everything slow, then fails everything.
- Admission control: limit concurrent work per service and reject early.
- Shedding priority: protect checkout and paying customers; drop recommendations and bots first.
- Return fast errors with retry hints; avoid retry storms.

**Show:** a priority table (critical: payment confirm; high: checkout; medium: browse; low: recommendations, crawlers) and a limiter placed at the edge with queue limits.

**Check:** What should be shed first? *(Low-priority traffic such as crawlers or recommendations.)*

---

## SRB-005-L04 · Cell-based architecture (12 min)
**Goal:** limit blast radius by splitting the system into independent cells.

**Key points**
- A cell is a complete copy of the stack serving a subset of customers.
- A failure or bad deploy affects one cell, not everyone.
- A routing layer maps customers to cells; it must be simple and highly available.
- Cost: more infrastructure and operational tooling; rollouts go cell by cell.

**Show:** diagram: router maps customer id hash to cell A, B, C; each cell has its own services and database; a bad deploy canaried in cell A.

**Check:** What does a cell limit? *(The blast radius of a failure.)*

---

## SRB-005-L05 · Shuffle sharding (10 min)
**Goal:** reduce the chance that one bad client harms many.

**Key points**
- Each client gets a small random subset of workers; the overlap between two clients is small.
- A poison request takes down its shard, not everyone.
- Works with retries: other workers in the subset keep serving.
- Needs enough workers for subsets to differ.

**Show:** an example: 8 workers, each customer assigned 2 of them; chance two customers share both is 1 in 28; one noisy tenant degrades only a pair.

**Check:** Why does shuffle sharding help? *(Few other clients share the same workers.)*

---

## SRB-005-L06 · Demo: shedding low-priority traffic during a flash sale (15 min)
**Goal:** protect checkout during a spike.

**Steps**
1. Generate a flash-sale load test with browse, checkout, and crawler traffic.
2. Observe checkout latency collapsing without limits.
3. Add priority-based admission control with separate queues and concurrency limits.
4. **Planned mistake:** shed by arrival order, dropping paying customers first; fix by classifying with an authenticated cart header and limiting anonymous traffic first.
5. Re-run and compare checkout success rate.

Prepares SRB-005-LAB1.

---

## SRB-005-L07 · Demo: computing checkout's real availability from its dependencies (15 min)
**Goal:** calculate a realistic availability number for checkout.

**Steps**
1. Draw the dependency graph, hard versus soft dependencies.
2. Collect measured availability of each hard dependency.
3. Multiply the serial hard dependencies and note the cap.
4. **Planned mistake:** multiply nines for every dependency including optional ones; fix by marking recommendations as soft with a fallback.
5. Show how a cache fallback for the FulfillCo stock check raises the total, and by how much.

Prepares SRB-005-LAB1.

---
