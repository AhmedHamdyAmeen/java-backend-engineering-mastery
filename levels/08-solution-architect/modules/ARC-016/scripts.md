# ARC-016 · Database architecture — Lecture scripts

**Video:** 68 min · **Running case:** *Larkspur Retail* — a fictional 120-store retailer replacing its dated on-premises web shop with a web and mobile platform (inventory, payments, fulfillment, customer service, reporting) integrated with the existing ERP and CRM. You are the solution architect.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## ARC-016-L01 · Managed databases: what you still own (10 min)
**Goal:** know what a managed database does for you and what it does not.

**Key points**
- The provider handles hardware, OS, engine patching, and scheduled backups.
- You still own schema design, queries and indexes, sizing, access control, encryption choices, and monitoring.
- Failover and backup features exist but must be configured and tested; they are not automatic disaster recovery.
- Maintenance windows and engine upgrades need planning.
- Managed does not mean "no operations".

**Show:** a two-column list: provider does / you still do, for a managed relational database.

**Check:** Does a managed database guarantee disaster recovery? *(No; you configure and test recovery.)*

---

## ARC-016-L02 · Selecting stores by workload (12 min)
**Goal:** choose relational, NoSQL, cache, or search per workload.

**Key points**
- Relational: transactions, joins, strong consistency; orders, payments, inventory.
- NoSQL (key-value, document): simple access patterns at large scale or flexible schema; carts, sessions, catalogs depending on needs.
- Cache: speeds repeated reads; never the source of truth.
- Search: full-text and faceted queries; fed from the source of truth.
- Polyglot costs operations; add a store only for a real need. One database for everything is also a mistake.

**Show:** a table: workload, access pattern, consistency need, chosen store, source of truth.

**Check:** Is a cache the source of truth? *(No; it is a copy for speed.)*

---

## ARC-016-L03 · Replication, read scaling, failover (12 min)
**Goal:** design for scale and failure per store.

**Key points**
- Multi-AZ standby: synchronous copy in another zone with automatic failover; protects availability, not read capacity.
- Read replicas: asynchronous copies for read scaling; may lag, so some reads are slightly stale.
- Cross-region replicas help disaster recovery but cost more and lag more.
- Failover takes time; applications must reconnect and handle brief errors.
- Test failover regularly.

**Show:** diagram: primary in zone A, synchronous standby in zone B, two read replicas serving catalog and reporting queries.

**Check:** What do read replicas improve? *(Read capacity; they may lag behind the primary.)*

---

## ARC-016-L04 · Backup, PITR, and DR for data (10 min)
**Goal:** define recovery for each data store.

**Key points**
- Automated backups plus transaction logs allow point-in-time recovery (PITR) to a moment before a mistake.
- Recovery point objective (RPO): how much data you can lose; recovery time objective (RTO): how long you can be down.
- Snapshots copied to another region or account support disaster recovery.
- Each store gets its own RPO/RTO; flag gaps where the design cannot meet them.
- Practice restores and measure the real time.

**Show:** a table: store, backup method, PITR window, RPO, RTO, DR copy location.

**Check:** What lets you restore to a minute before an accidental delete? *(Point-in-time recovery.)*

---

## ARC-016-L05 · Migrating databases to the cloud (10 min)
**Goal:** plan a safe migration from an on-premises database.

**Key points**
- Options: dump and restore (simple, downtime), replication-based migration (minimal downtime), application-level dual writes (complex).
- Assess engine and version compatibility, size, and network bandwidth; verify tools before recording.
- Plan cutover: freeze, final sync, validation, switch, rollback path.
- Validate data: row counts, checksums, sample queries.
- Rehearse in non-production first.

**Show:** a cutover timeline with a decision point for rollback.

**Check:** Why rehearse a migration first? *(To measure time, find problems, and prove the rollback.)*

---

## ARC-016-L06 · Demo: Larkspur's data stores and their failover design (14 min)
**Goal:** design Larkspur's data platform and flag RPO/RTO gaps for `ARC-016-LAB1`.

**Steps**
1. List workloads: orders and payments records, inventory, product catalog, sessions and carts, product search, reporting.
2. Choose: managed relational with multi-AZ for orders and inventory; document or key-value store for carts; cache for catalog reads; managed search for product search; read replica for reporting.
3. Set failover and backup per store with PITR windows and cross-region snapshot copies.
4. **Planned mistake:** assuming managed multi-AZ equals DR. Fix: add cross-region snapshot copy and a restore runbook; note the region-loss RTO is hours, not minutes.
5. Compare each store's RPO/RTO with the requirements; flag the gap on search (rebuilt from the source, so RPO is nil but rebuild time is long).
6. Add the web shop database migration approach: replication-based with a rehearsed cutover.

---
