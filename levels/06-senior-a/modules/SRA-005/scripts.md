# SRA-005 · Multi-region trade-offs — Lecture scripts

**Video:** 84 min · **Running case:** *Commerce 2030* — the group formed by Shop and FulfillCo has 25 engineering teams and plans a third-party seller marketplace, a five-country expansion, and doubled order volume each year for three years, while its earliest services approach end of life; you are the senior technical leader for the commerce product area.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRA-005-L01 · Multi-region as a business decision (10 min)
**Goal:** frame regions as a business choice with costs, not a default technical goal.

**Key points**
- Reasons: latency for customers, legal residency, resilience to a regional failure, market entry.
- Each reason implies a different design; "go multi-region" alone is not a requirement.
- Complexity and cost rise sharply with each region; ask what the business gets for it.
- The cheapest answer may be one region plus a CDN, or a second region for recovery only.

**Show:** a table for Commerce 2030: driver (latency, residency, resilience, market), which countries it applies to, and the minimum design that satisfies it.

**Check:** Why is "we need multi-region" not yet a requirement? *(It does not say which driver, which capability, or what failure or rule it must meet.)*

---

## SRA-005-L02 · Consistency needs per capability (12 min)
**Goal:** choose availability versus consistency capability by capability.

**Key points**
- Across regions you trade strong consistency against latency and availability (CAP and latency trade-offs).
- Ask the business what a wrong or stale answer costs: a stale product page versus a double-sold item.
- Patterns: single-writer per record, regional ownership of data, eventual consistency with conflict rules.
- Catalog and search tolerate staleness; inventory reservations and payments usually do not.

**Show:** a table listing capabilities (catalog, search, cart, checkout, inventory, payments) with tolerated staleness, conflict handling, and a recommended pattern.

**Check:** Why not choose one consistency model for the whole platform? *(Capabilities have different costs of staleness; a single choice over- or under-pays.)*

---

## SRA-005-L03 · Jurisdiction and data transfer (12 min)
**Goal:** map legal rules about data location onto the architecture.

**Key points**
- Residency: some data must be stored or processed in a country or region.
- Transfer rules govern when data may leave, with lawful mechanisms; work with legal partners, do not guess.
- Local regulators may also require specific retention, reporting, or local entities.
- Design for the rule: regional stores, tokenized references, and clear data flow diagrams.

**Show:** a data flow diagram with country boundaries drawn over it, marking which fields stay local and which may be replicated, with a "verify with legal" note on each.

**Check:** Who decides what a transfer rule requires? *(Legal and compliance partners; engineering translates it into design.)*

---

## SRA-005-L04 · The operational cost of regions (10 min)
**Goal:** count the full operating cost of each added region.

**Key points**
- Infrastructure is only part: add on-call, tooling, deployments, data replication, and testing.
- Each region multiplies the failure modes: replication lag, partial outages, config drift.
- Data transfer and duplicated stateful systems are often the largest costs.
- Include the staffing and learning cost before approving.

**Show:** a cost sheet: infrastructure, data transfer, tooling, on-call share, extra engineering, compliance, with assumptions and per-year totals for one, two, and three regions.

**Check:** Name two costs of a region that are not infrastructure. *(For example on-call load and tooling, extra engineering, compliance.)*

---

## SRA-005-L05 · Sequencing geographic expansion (10 min)
**Goal:** add complexity only when the business needs it.

**Key points**
- Start with the simplest design that meets the first country's needs.
- Add residency or latency measures when a trigger occurs: a regulation, volume, or revenue.
- Keep the design open: tenant or region identifiers in data from the start, regional config.
- Define go and no-go criteria and reassess after each country.

**Show:** a phased plan: country 1 in the existing region, countries 2 and 3 with regional data stores for residency, countries 4 and 5 gated by revenue and legal need.

**Check:** What should the first step of a multi-country plan avoid? *(Building the most complex global design before any trigger demands it.)*

---

## SRA-005-L06 · Demo: a capability-by-capability region decision table (15 min)
**Goal:** build the decision table for Commerce 2030; prepares SRA-005-LAB1.

**Steps**
1. List capabilities: catalog, search, cart, checkout, inventory, payments, seller payouts, identity.
2. For each, ask the business owner the cost of stale or lost data and of downtime.
3. Choose a pattern per capability: global read replicas, regional ownership, single-region with failover.
4. Add residency constraints from legal for personal, seller, and payment data (verify with compliance).
5. **Planned mistake:** choose active-active everywhere because it sounds safest. Fix: show the conflict handling and cost for inventory, and downgrade capabilities that do not need it.
6. Review the table with product and compliance.

---

## SRA-005-L07 · Demo: costing three expansion options (15 min)
**Goal:** compare three expansion strategies with explicit costs and risks; prepares SRA-005-LAB1.

**Steps**
1. Define options: A single region for all five countries, B a second region for two countries needing residency, C a region per country.
2. Estimate for each infrastructure, data transfer, tooling, on-call, and staffing over three years, with assumptions listed.
3. Estimate benefits: revenue enabled, latency gains, compliance risk avoided.
4. Present a recommendation with triggers to move from A to B.
5. **Planned mistake:** compare only infrastructure bills. Fix: add on-call and engineering effort, which shifts the ranking.
6. Record assumptions and a review date; share with finance.
