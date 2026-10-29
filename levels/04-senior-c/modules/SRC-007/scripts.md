# SRC-007 · Database scaling — Lecture scripts

**Video:** 104 min · **Running case:** *Order Processing at 10×* — Shop Platform's order subsystem must handle a 10× growth forecast, a 99.95% availability commitment, and a 15-minute recovery objective.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRC-007-L01 · The scaling ladder (10 min)
**Goal:** climb from the cheapest option upward, with evidence at each rung.

**Key points**
- Order: fix queries and indexes, cache, vertical scale, read replicas, partitioning, sharding or distributed SQL.
- Each rung adds operational and application complexity.
- Move up only when measurements show the current rung cannot meet the target.
- Write load is the hard part; reads are easier to offload.

**Show:** a ladder diagram with the capacity gain and complexity cost per rung.

**Check:** Why exhaust simpler options first? *(Each step up adds complexity and cost that simpler fixes may avoid.)*

---

## SRC-007-L02 · Read replicas and lag-aware design (12 min)
**Goal:** use replicas without breaking correctness.

**Key points**
- Replicas serve reads asynchronously; they lag behind the primary.
- Reads that must see just-written data (read-your-writes) go to the primary or use session stickiness or LSN checks.
- Monitor replica lag and fall back to the primary above a threshold.
- Replicas help read scaling and failover, not write scaling.

**Show:** a routing rule: after a customer's write, read from the primary for N seconds, else a replica.

**Check:** What do replicas not scale? *(Writes.)*

---

## SRC-007-L03 · Partitioning revisited (8 min)
**Goal:** use partitioning inside one database to manage large tables.

**Key points**
- Declarative partitioning splits a table by range, list, or hash within one server (details in earlier modules; verify version features).
- Benefits: pruning, cheaper retention (drop a partition), smaller indexes.
- It does not add write capacity beyond one server.
- Queries must include the partition key to prune.

**Show:** orders partitioned monthly by `created_at`; dropping a partition removes old data fast.

**Check:** Does partitioning in one server increase write capacity beyond that server? *(No.)*

---

## SRC-007-L04 · Sharding and shard keys (14 min)
**Goal:** choose a shard key that fits the main queries.

**Key points**
- Sharding splits data across servers by a key; each shard handles a share of writes.
- A good key has high cardinality, even distribution, and appears in the main queries.
- Cross-shard queries, transactions, and joins become expensive or impossible.
- Candidates for orders: customer id, order id (hash), region or tenant.

**Show:** a table: key, even spread, query fit, risk, e.g. customer id fits "my orders" but makes a large customer hot.

**Check:** What breaks if the shard key is not in the common query? *(The query must hit every shard.)*

---

## SRC-007-L05 · Hot partitions (10 min)
**Goal:** predict and measure skew.

**Key points**
- Skew arises from big customers, time-based keys (all writes to the newest range), and promotions.
- Measure distribution from real data before choosing; estimate the top key's share.
- Mitigations: composite keys, salting, hashing, splitting large tenants, caching.
- Include hot-partition headroom in the capacity plan.

**Show:** a histogram description: top 1% of customers produce 30% of orders; the hot shard needs 3× the average capacity.

**Check:** Why is a timestamp a poor shard key for writes? *(All new writes hit the latest partition.)*

---

## SRC-007-L06 · Resharding (10 min)
**Goal:** plan to change the number of shards.

**Key points**
- Resharding is a data migration under traffic; plan for it before the first shard.
- Approaches: consistent hashing or many logical shards mapped to few servers.
- Steps: copy, replicate changes, verify, cut over, clean up.
- Practice it on staging and keep rollback.

**Show:** 256 logical shards over 4 servers; moving to 8 servers moves logical shards, not rows between keys.

**Check:** What makes resharding easier? *(Many logical shards mapped to physical servers.)*

---

## SRC-007-L07 · Distributed SQL and managed options (10 min)
**Goal:** compare managed distributed SQL with operating sharded PostgreSQL.

**Key points**
- Options: PostgreSQL-compatible distributed databases and managed services (verify current products and compatibility before recording).
- Gains: transparent scaling and failover; costs: latency for distributed commits, compatibility gaps, vendor dependence, price.
- Evaluate against workload: transactions, joins, latency, data residency.
- Run a proof of concept with your own workload.

**Show:** a decision table: criteria, sharded PostgreSQL, managed distributed SQL, score and evidence.

**Check:** How do you evaluate these options fairly? *(Against your workload and requirements with a proof of concept.)*

---

## SRC-007-L08 · Demo: choosing a shard key for orders (15 min)
**Goal:** pick and test a shard key; prepares SRC-007-LAB1.

**Steps**
1. List the main queries: order by id, orders by customer, ops reports by date.
2. Analyze real order data for distribution by customer and by order id.
3. **Planned mistake:** choose order id hash because it spreads evenly. Fix: "my orders" now hits all shards; choose customer id with salting for large customers or keep a lookup table.
4. Quantify hot-partition risk using the top customers' share.
5. Outline resharding and the migration plan.
6. Record the decision in an ADR.

---

## SRC-007-L09 · Demo: read replicas and the stale-read bug they introduce (15 min)
**Goal:** reproduce and fix a read-after-write bug.

**Steps**
1. Add a replica and route reads to it.
2. Place an order, then immediately load "my orders"; the order is missing.
3. **Planned mistake:** blame the cache. Fix: confirm replica lag in metrics; the read went to the replica.
4. Implement read-your-writes: route recent writers to the primary or wait for the replica's position.
5. Add lag monitoring and a fallback threshold.
6. Add a test that fails when the stale read returns.
