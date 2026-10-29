# SRA-007 · Large-scale performance — Lecture scripts

**Video:** 84 min · **Running case:** *Commerce 2030* — the group formed by Shop and FulfillCo has 25 engineering teams and plans a third-party seller marketplace, a five-country expansion, and doubled order volume each year for three years, while its earliest services approach end of life; you are the senior technical leader for the commerce product area.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRA-007-L01 · Capacity at product-area scale (10 min)
**Goal:** extend capacity planning from one service to a product area with many dependent services.

**Key points**
- One business event (an order) fans out into calls across many services; capacity is a chain.
- The bottleneck moves as load grows; plan the whole path, not each service alone.
- Capacity planning links business drivers, technical load, and spend on a calendar.
- Keep headroom for peaks and failure of a zone, not only average load.

**Show:** a call-fan-out diagram for one order across ten services with calls per order on each edge and the current limiting service highlighted.

**Check:** Why plan capacity along the whole request path? *(The weakest link limits throughput and the bottleneck shifts as load grows.)*

---

## SRA-007-L02 · Forecasting from business drivers (12 min)
**Goal:** turn business plans into load forecasts instead of extrapolating graphs.

**Key points**
- Drivers: orders, sellers, listings, countries, campaigns, each with its own load factor.
- Convert drivers to technical load with ratios (requests per order, rows per listing) from measurements.
- Show ranges and sensitivity: what if growth is 1.5x or 3x rather than 2x.
- Revisit assumptions regularly; track forecast error.

**Show:** a model table: driver, annual value, ratio, resulting load, with low, base, and high cases for three years.

**Check:** Why not extend last year's traffic curve? *(New products, countries, and campaigns change the drivers and shape of load.)*

---

## SRA-007-L03 · Workload modeling (12 min)
**Goal:** model traffic mixes realistically, including new products.

**Key points**
- A workload model describes the mix: reads and writes, endpoints, payload sizes, peak shape.
- Build from production data for existing flows and from analogies and assumptions for new ones.
- Marketplace sellers add new shapes: bulk listing uploads, inventory sync, payout batches.
- Validate with load tests of representative mixes and compare with later production.

**Show:** a workload table for the marketplace launch: buyer browsing, checkout, seller bulk uploads, inventory feeds, each with rate, burst pattern, and source of the estimate.

**Check:** What new traffic shape might sellers add that buyers do not? *(Bulk listing uploads, inventory sync, and payout batches.)*

---

## SRA-007-L04 · Cost-performance optimization (12 min)
**Goal:** optimize cost and latency together, not separately.

**Key points**
- Use cost per transaction at a target latency as the common measure.
- Options: caching, right-sizing, batching, async processing, different storage tiers, reserved capacity.
- Every latency target has a price; ask the business what it is worth.
- Measure after a change; optimizations that save little at high complexity are not worth it.

**Show:** a curve sketch: cost per order against p99 latency, with the knee where extra speed becomes expensive, and a marked target.

**Check:** What measure combines cost and performance? *(Cost per transaction at the target latency.)*

---

## SRA-007-L05 · Performance budgets for teams (8 min)
**Goal:** give each team a share of the latency and cost budget and track it.

**Key points**
- Split the end-to-end budget: for example 800 ms for checkout allocated across steps.
- Each team owns its share, measured continuously and visible.
- Budgets are enforced by checks in CI or release gates and by alerts.
- Revisit budgets as workloads change and when a team needs more.

**Show:** a budget table for checkout: step, owner, p99 budget, current value, cost per order share.

**Check:** Why split an end-to-end latency budget among teams? *(So each team knows its limit and the sum stays within the customer-facing target.)*

---

## SRA-007-L06 · Demo: forecasting the marketplace launch's load (15 min)
**Goal:** forecast the load of a new product from drivers; prepares SRA-007-LAB1.

**Steps**
1. Define drivers: sellers onboarded, listings per seller, orders per listing, countries.
2. Measure existing ratios (requests per order) and choose analogies for new ones, marking assumptions.
3. Build low, base, and high cases for years one to three and add campaign peaks.
4. Identify the services that saturate first and the lead time for each fix.
5. **Planned mistake:** assume marketplace traffic looks like retail traffic. Fix: model seller bulk uploads and feed syncs, which move the bottleneck to listing ingestion and search indexing.
6. Present the forecast with sensitivity and the review schedule.

---

## SRA-007-L07 · Demo: trading 10 ms of latency for 25% lower cost (15 min)
**Goal:** run a leadership discussion that prices a latency target; prepares SRA-007-LAB1.

**Steps**
1. Start with the situation: a search service costs a given amount per month at p99 of 120 ms.
2. Find options: smaller cache, fewer replicas, and coarser indexing that raise p99 by 10 ms and cut cost about 25% (verify by measurement).
3. Measure customer impact: check whether 10 ms changes conversion in an experiment or historical data.
4. Present the trade-off to product and finance: saved cost, risk, and rollback.
5. **Planned mistake:** accept the saving without measuring impact. Fix: run an experiment, set a guardrail, and decide with data.
6. Record the decision, budget change, and review date.
