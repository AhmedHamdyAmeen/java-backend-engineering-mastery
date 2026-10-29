# MID-044 · Data selection — Lecture scripts

**Video:** 40 min · **Analogy used throughout:** choosing a vehicle: a van, a bike, and a truck are each right sometimes, and every extra vehicle needs fuel, insurance, and a driver. Running project: Shop.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-044-L01 · Characterizing a workload (10 min)
**Goal:** describe a workload with numbers before choosing a store.

**Key points**
- Access patterns: which queries, read/write ratio, point lookups or scans.
- Volume: rows today and in two years, growth, record size.
- Consistency: what must be correct immediately, what can lag.
- Latency and availability targets; query flexibility (will new questions appear?).
- Write the findings down with evidence (logs, metrics), not guesses.

**Show:** a one-page template: access patterns, volume, consistency, latency, flexibility, retention, team skills.

**Check:** Name three things to measure first. *(Access patterns, volume, and consistency needs.)*

---

## MID-044-L02 · PostgreSQL first, and when not (10 min)
**Goal:** justify a default and the conditions for leaving it.

**Key points**
- PostgreSQL handles relational data, JSON, full-text, queues, and moderate scale in one operable system.
- Leave it when the workload clearly needs: massive write throughput or horizontal scale, sub-millisecond key lookups (Redis), rich search (OpenSearch), flexible nested documents at scale (MongoDB), deep graph traversal.
- Prove it with evidence (a load test, a query plan that cannot be fixed), not fashion.
- "PostgreSQL is enough" is a valid and frequent ADR outcome.

**Show**
| Need | Choice |
| --- | --- |
| Orders, payments | PostgreSQL |
| Hot cache, sessions, counters | Redis |
| Full-text with facets | OpenSearch |
| Reviews at high volume, flexible shape | MongoDB, or PostgreSQL if modest |

**Check:** Name a signal that justifies leaving PostgreSQL. *(Measured load or query needs that tuning and scaling cannot meet.)*

---

## MID-044-L03 · The operational cost of another database (8 min)
**Goal:** count the full cost of each extra datastore.

**Key points**
- Run: provisioning, upgrades, patching, capacity planning.
- Protect: backup and restore tested, security, access control, encryption.
- Observe: monitoring, alerts, dashboards, on-call runbooks.
- People: skills, hiring, on-call burden.
- Data: sync with the source of truth, reindex or rebuild, consistency bugs, extra failure modes.
- Cost scales with the number of different stores, not only the size of data.

**Show:** checklist: backup tested, monitoring in place, runbook written, two engineers can operate it, sync strategy defined.

**Check:** Which hidden cost appears when data lives in two stores? *(Keeping them in sync and handling divergence.)*

---

## MID-044-L04 · Demo: writing the reviews datastore ADR (12 min)
**Goal:** write an ADR choosing the store for reviews, from evidence. Prepares MID-044-LAB1.

**Steps**
1. Context: Shop expects 2 M reviews in a year, 50 writes per minute, reads by product and a rating summary, a flexible optional "attributes" part.
2. List options: PostgreSQL (with `jsonb`), MongoDB, wide-column.
3. Score them against the workload and operational cost; include the extra database cost from L03.
4. **Planned mistake:** choose MongoDB because it is "good for reviews", with no numbers. Fix: attach the volume and query evidence; note that 2 M rows with these queries fit PostgreSQL easily.
5. Write the decision, consequences, and a revisit trigger (for example "reconsider above 200 M reviews or 5 000 writes/s").

**Check:** What must an ADR contain besides the decision? *(Context, options, consequences, and a revisit trigger.)*
