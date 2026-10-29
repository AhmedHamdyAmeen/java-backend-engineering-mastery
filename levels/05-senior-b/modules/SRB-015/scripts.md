# SRB-015 · Cost optimization — Lecture scripts

**Video:** 84 min · **Running case:** *The FulfillCo integration* — the engineer leads the four-team program planned in SRB-P1 through delivery; role-players act as team leads, product, finance, and security.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRB-015-L01 · Cost as an architectural quality (10 min)
**Goal:** treat cost as a design quality next to reliability and performance.

**Key points**
- Cost is shaped by architecture decisions: data movement, redundancy, always-on versus on-demand.
- Cost, reliability, and speed trade against each other; make the trade explicit.
- A merged platform (Shop plus FulfillCo) often duplicates services; duplication is a cost lever.
- Cost needs an owner and a regular review, like any other quality.

**Show** A trade-off line per design choice: *cross-region replication: +reliability, +transfer cost, who pays?*

**Check:** Why is cost an architectural concern? *(Design choices fix much of the running cost long before tuning.)*

---

## SRB-015-L02 · Cloud cost drivers (12 min)
**Goal:** name the main drivers on a cloud bill.

**Key points**
- Compute: instance hours, container resources, serverless invocations; often the largest line.
- Storage: volume, snapshots, object storage tiers, backups kept too long.
- Data transfer: cross-zone, cross-region, and internet egress; easy to overlook.
- Managed services: databases, queues, search; billed by capacity or throughput.
- Idle and forgotten resources: unattached disks, old environments.

**Show** A bill grouped by category with a pie of top ten line items; ask which are tied to load and which are fixed.

**Check:** Which driver is often overlooked in microservice designs? *(Data transfer between zones or regions.)*

---

## SRB-015-L03 · Attribution and unit economics (12 min)
**Goal:** attribute costs to services and teams and compute cost per order.

**Key points**
- Tag resources consistently (service, team, environment); untagged spend is unowned spend.
- Allocate shared costs (clusters, networking) with a stated rule, such as by usage.
- Unit economics: total cost divided by a business unit, such as cost per order, so growth does not hide inefficiency.
- Track unit cost over time and per service.

**Show** Table: service | tagged monthly cost | allocated shared cost | orders | cost per order. Highlight the trend line across months.

**Check:** Why use cost per order instead of total cost? *(Total cost rises with growth; unit cost shows efficiency.)*

---

## SRB-015-L04 · Optimization levers (12 min)
**Goal:** choose levers that reduce cost without harming reliability.

**Key points**
- Rightsizing: match resources to measured usage.
- Autoscaling and scheduling: scale down off-peak, shut non-production at night.
- Commitments: reserved or savings plans for steady baseline load; analyze before committing.
- Storage tiers and lifecycle rules; delete or compress what is not needed.
- Architectural changes: reduce data movement, cache, batch, consolidate duplicate services.

**Show** Lever table: lever | saving estimate | risk | engineering effort | evidence needed. Example: *non-prod nightly shutdown | moderate | low | small | usage data.*

**Check:** What must you check before buying a commitment? *(That the baseline usage is stable enough to use it.)*

---

## SRB-015-L05 · FinOps basics (8 min)
**Goal:** describe the practices that keep cost under control continuously.

**Key points**
- Visibility: dashboards by team and service.
- Accountability: each team sees and owns its cost.
- Regular review with finance and product; budgets and alerts for anomalies.
- Savings tracked as a pipeline with owners, not one-off projects.

**Show** A monthly cost review agenda: top changes, anomalies, savings status, forecast, decisions.

**Check:** What makes cost reviews effective? *(Team-level visibility, owners, and decisions recorded.)*

---

## SRB-015-L06 · Demo: cutting cost per order by 30% (15 min)
**Goal:** plan a 30% cost-per-order reduction on the combined platform with traceable estimates; prepares SRB-015-LAB1.

**Steps**
1. Compute the baseline cost per order from the bill and order counts.
2. Rank line items by cost and by saving potential.
3. Estimate savings per lever (rightsizing, non-production schedules, storage tiers, duplicate service consolidation) with evidence from usage data.
4. **Planned mistake:** pick many small items because they are easy. Fix: focus on the top drivers; small items only if they are quick and safe.
5. Check each saving for reliability impact (redundancy, headroom) and record risks.
6. Sequence the plan and set a measure for each step.

**Check:** What makes the savings estimate credible? *(Each figure is traceable to bill lines and usage data.)*

---

## SRB-015-L07 · Demo: tagging a cloud bill and finding the top three cost drivers (15 min)
**Goal:** tag spend to services and find the top drivers; prepares SRB-015-LAB1.

**Steps**
1. Export the bill and measure how much spend is untagged.
2. Define the tag scheme (service, team, environment) and apply it to resources.
3. Allocate shared costs with a stated rule.
4. **Planned mistake:** leave a large untagged remainder and report precise per-service numbers. Fix: state the untagged share and reduce it before drawing conclusions.
5. Rank services and identify the top three drivers.
6. Compute cost per order for each driver and note the first questions to ask the owners.

**Check:** Why report the untagged share? *(It limits how much trust the per-service numbers deserve.)*
