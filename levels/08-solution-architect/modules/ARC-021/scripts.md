# ARC-021 · Cost architecture — Lecture scripts

**Video:** 79 min · **Running case:** *Larkspur Retail* — a fictional 120-store retailer replacing its dated on-premises web shop with a web and mobile platform (inventory, payments, fulfillment, customer service, reporting) integrated with the existing ERP and CRM. You are the solution architect.
Format: **Goal** · **Key points** · **Show** · **Check**.
Pricing note: all prices and discounts are provider-specific and change; use current price lists and "verify before recording". Numbers in demos are illustrative assumptions.

---

## ARC-021-L01 · Cost as a design input (8 min)
**Goal:** treat cost as a quality attribute designed in from the start.

**Key points**
- Cloud cost is a result of design choices: compute shape, data movement, storage, redundancy.
- Cost is variable and usage-driven, so it can surprise as easily as it can save.
- Compare options by total cost including operating effort, not only the price list.
- Surface the cost of each requirement (for example, a tighter RTO) to the sponsor.
- Cost and other qualities trade off; record the trade-off.

**Show:** two designs for the same requirement with their cost and risk, such as warm standby versus backup-restore.

**Check:** Is cost only a finance concern? *(No; design choices create it, so architects own part of it.)*

---

## ARC-021-L02 · Sizing and pricing assumptions (12 min)
**Goal:** size the solution and state pricing assumptions explicitly.

**Key points**
- Start from load: orders per day, peak per second, data volumes, users, page views.
- Translate load into resources: instances or tasks, database size and I/O, storage, data transfer.
- List pricing assumptions: region, on-demand versus committed use, discounts, currency, date of price list.
- Mark each number as measured, estimated, or guessed, with a confidence level.
- Keep assumptions in one place so they can be changed and the model recalculated.

**Show:** an assumptions sheet: driver, value, source, confidence (orders per month: 600,000, from web shop reports, high confidence).

**Check:** Why mark confidence on each assumption? *(So reviewers know which numbers to challenge and what drives the range.)*

---

## ARC-021-L03 · Building a cost model (12 min)
**Goal:** build a line-by-line cost model from assumptions.

**Key points**
- Break down by component: compute, database, storage, network and data transfer, edge, observability, security, support, third-party SaaS.
- Include the often-forgotten items: data transfer, NAT, logging and metrics volume, backups, non-prod environments, support plans.
- Model normal and peak months separately.
- Add a contingency and show low, expected, and high estimates.
- Keep the model traceable: each line links to a driver and a price.

**Show:** a spreadsheet outline: component, driver, unit price, quantity, monthly low/expected/high, notes.

**Check:** Name two commonly forgotten cost items. *(Data transfer and logging; also non-prod environments and backups.)*

---

## ARC-021-L04 · Unit cost and sensitivity (10 min)
**Goal:** express cost per business transaction and test how it changes with volume.

**Key points**
- Unit cost, such as cost per order, links infrastructure to business value.
- Split fixed costs (baseline) from variable costs (scale with volume).
- Sensitivity: change one driver at a time (orders, page views, data volume) and see the effect.
- Watch for steps and cliffs: a larger database tier, extra zones, new licence bands.
- Compare unit cost with margin per order to see if the platform is economic.

**Show:** a chart sketch: monthly cost versus orders with a fixed base and a rising variable line; cost per order falling then stepping up.

**Check:** Why split fixed and variable costs? *(To see how cost per order changes as volume grows.)*

---

## ARC-021-L05 · Budgets and controls (8 min)
**Goal:** set budgets, alerts, and controls that prevent surprises.

**Key points**
- Budgets per account or team with alerts at thresholds (for example 50, 80, 100 percent) and forecast alerts.
- Anomaly detection catches sudden spikes.
- Controls: quotas, guardrails on expensive services, auto-shutdown of non-prod, rightsizing reviews.
- Commitments (reserved or savings plans) after usage is understood; verify terms before recording.
- Assign an owner who reviews cost monthly.

**Show:** a table: account, monthly budget, alert thresholds, owner, automatic action.

**Check:** When should you buy commitments? *(After usage is stable and understood.)*

---

## ARC-021-L06 · Demo: Larkspur's cloud cost model, line by line (15 min)
**Goal:** build the Larkspur cost model with ranges, preparing `ARC-021-LAB1`.

**Steps**
1. Assumptions: orders per month, peak multiplier, page views, media size, data stored, environments (illustrative; confirm with the web shop data).
2. Components: containers, managed database with standby, cache, search, object storage and CDN, queues, observability, security services, backups, DR copy.
3. Compute each line as driver times price; mark confidence.
4. **Planned mistake:** leaving out data transfer and log ingestion. Add them; show that they rise from 5 to 20 percent of the total in the model.
5. Add non-prod environments and support plan.
6. Present low, expected, and high monthly cost with the main uncertainty drivers.

---

## ARC-021-L07 · Demo: what the cost does at peak season and at 3× growth (14 min)
**Goal:** show how cost and cost per order behave under peak and growth, preparing the sensitivity part of the lab.

**Steps**
1. Define scenarios: normal month, peak month (autoscaled), and three times current volume.
2. Re-run the model with each scenario's drivers.
3. Identify which lines scale linearly (data transfer, requests) and which step (database tier, cache nodes).
4. **Planned mistake:** assuming costs scale linearly and extrapolating from the normal month. Fix: model the database step and pre-scaling for peak.
5. Compute cost per order in each scenario and compare with the margin.
6. Propose controls: peak-season budget, rightsizing after peak, commitments for the base load only.

---
