# SRC-004 · Capacity planning — Lecture scripts

**Video:** 94 min · **Running case:** *Order Processing at 10×* — Shop Platform's order subsystem must handle a 10× growth forecast, a 99.95% availability commitment, and a 15-minute recovery objective.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRC-004-L01 · From business forecast to load (12 min)
**Goal:** convert "10× orders" into requests per second and concurrency.

**Key points**
- Chain: orders per day, then orders per peak hour, then per second, then requests per order.
- Each order triggers several calls (browse, cart, checkout, payment, tracking); count them.
- Write every factor as a named assumption with an owner.
- Keep the forecast as a range, not a single number.

**Show:** a worksheet: 200k orders/day (verify with data), peak hour 12% of day, 25 requests per order, giving peak RPS with a low, expected, and high column.

**Check:** Why count requests per order? *(Load is requests, not orders; each order produces many calls.)*

---

## SRC-004-L02 · Peaks, seasonality, and burst factors (10 min)
**Goal:** size for the peak, not the average.

**Key points**
- Averages hide peaks; capacity must cover the busiest minute you accept.
- Seasonal events (Black Friday), campaigns, and daily cycles multiply the base.
- Burst factor: ratio of peak second to peak-hour average.
- Decide which peaks you absorb, which you shed, and which you queue.

**Show:** a traffic chart description with daily curve, a weekly bump, a Black Friday spike, and the sizing line placed deliberately.

**Check:** Why is sizing for the average dangerous? *(Peaks exceed it and the system saturates exactly when load matters most.)*

---

## SRC-004-L03 · Back-of-the-envelope estimation (14 min)
**Goal:** estimate quickly and show the arithmetic.

**Key points**
- Use round numbers and powers of ten; state units.
- Know typical figures: a request's CPU time, a disk or network throughput, a row's size (verify against your environment).
- Write assumptions first, then arithmetic, then a sanity check against known data.
- The goal is the order of magnitude and the first bottleneck.

**Show:** an estimate: 6,000 orders/min peak = 100/s; 25 calls each = 2,500 RPS; at 4 ms CPU each = 10 cores busy; with 50% target utilization, about 20 cores.

**Check:** What is the purpose of a back-of-the-envelope estimate? *(Find order of magnitude and the first bottleneck, with visible assumptions.)*

---

## SRC-004-L04 · Storage and data growth (10 min)
**Goal:** project storage with multipliers.

**Key points**
- Rows per day times row size times retention gives raw size.
- Multipliers: indexes, replication, backups, WAL, Kafka retention and replication factor.
- Growth is rarely linear; include history growth and new features.
- Note time to restore, not just space.

**Show:** a table: orders table 1 KB per row, 2M rows/day, 1 year retention, with index factor 1.5 and 2 replicas, giving total storage.

**Check:** Name two multipliers people forget. *(Replication and retention, plus indexes or backups.)*

---

## SRC-004-L05 · Headroom and saturation points (10 min)
**Goal:** know how much margin each component has.

**Key points**
- Headroom: unused capacity before the component degrades.
- Find saturation by load test: CPU, connections, I/O, locks, queue depth.
- Components saturate at different loads; the lowest headroom is the first bottleneck.
- Plan headroom for failure: if one node dies, can the rest cope?

**Show:** a table per component: current peak, tested limit, headroom percent, N-1 headroom.

**Check:** Which component limits the system? *(The one with the least headroom at the target load.)*

---

## SRC-004-L06 · Capacity plans people can act on (8 min)
**Goal:** write a plan that finance and operations can use.

**Key points**
- Include assumptions, numbers, margins, cost, and the date each step is needed.
- Define triggers: "start expansion when peak CPU exceeds 60% for a week."
- Review on a schedule and when an assumption changes.
- Keep it short; link the worksheet.

**Show:** a one-page outline: forecast, current state, gaps, actions with dates, triggers, owners.

**Check:** What makes a plan actionable? *(Concrete actions, dates, owners, and re-planning triggers.)*

---

## SRC-004-L07 · Demo: sizing the order subsystem for Black Friday at 10× (15 min)
**Goal:** size orders, inventory, Kafka, and PostgreSQL step by step; prepares SRC-004-LAB1.

**Steps**
1. Write the forecast chain and assumptions with ranges.
2. Derive peak RPS and write rate for PostgreSQL.
3. **Planned mistake:** size from the daily average. Fix: apply the burst factor and the Black Friday multiplier; the result is several times larger.
4. Estimate Kafka throughput, partitions, and storage with replication and retention.
5. Compare with MID load-test limits; name the first bottleneck.
6. Add headroom and re-planning triggers.

---

## SRC-004-L08 · Demo: checking last year's capacity plan against reality (15 min)
**Goal:** learn from the gap between plan and actual.

**Steps**
1. Collect last year's plan and actual usage from monitoring.
2. Compare each number: forecast, peak RPS, storage, CPU.
3. **Planned mistake:** blame the forecast. Fix: separate forecast error from model error; requests per order was underestimated, not orders.
4. Update the assumptions and the burst factor.
5. Add a trigger that would have caught the drift.
6. Record the lesson in the plan template.
