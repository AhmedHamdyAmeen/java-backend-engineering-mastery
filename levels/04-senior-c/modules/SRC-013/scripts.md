# SRC-013 · Disaster recovery — Lecture scripts

**Video:** 96 min · **Running case:** *Order Processing at 10×* — Shop Platform's order subsystem must handle a 10× growth forecast, a 99.95% availability commitment, and a 15-minute recovery objective.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRC-013-L01 · Disasters that actually happen (10 min)
**Goal:** list the realistic disasters a subsystem must survive.

**Key points**
- Common causes are human and software: a bad migration, a deleted volume, a leaked or expired credential, a corrupt deploy, a ransomware or account lockout.
- Infrastructure disasters (zone or region loss) are real but rarer than operator error.
- High availability (surviving a node) is not disaster recovery (surviving the loss of data or a whole site); replication copies mistakes too.
- Scope the subsystem: data stores, event streams, secrets, DNS, configuration, and the people and access needed.

**Show** A table: disaster | likelihood | impact | does HA cover it? | what recovers it. Rows: dropped table, zone outage, region outage, expired certificate, lost cloud account access.

**Check:** Why does replication not protect against an accidental table drop? *(The drop replicates to the copies.)*

---

## SRC-013-L02 · RPO and RTO from business impact (12 min)
**Goal:** set recovery objectives per data set and service from what loss costs.

**Key points**
- RPO (recovery point objective): how much data, measured in time, you can lose. RTO (recovery time objective): how long you can be down.
- Derive each from business impact: lost orders, refunds, regulatory duty, reputation; not from what the technology offers.
- Different data sets differ: orders and payments need a tight RPO; a recommendation cache can be rebuilt.
- Tighter objectives cost more; present the cost per tier so the business chooses.
- The running case has a 15-minute RTO for the order database.

**Show** Tier table: data set | RPO | RTO | rationale | approximate cost tier. Example: orders DB | near zero | 15 min; search index | 24 h | 4 h; session cache | n/a | rebuild.

**Check:** Who should decide the RPO for orders? *(The business, informed by impact and cost, with engineering advising.)*

---

## SRC-013-L03 · Backup and replication strategies (12 min)
**Goal:** choose mechanisms that can actually meet the RPO.

**Key points**
- Backups: full plus incremental or continuous log archiving give point-in-time recovery; snapshots are fast but verify consistency.
- Replication: synchronous gives near-zero RPO with latency cost; asynchronous is cheaper with some loss window.
- Keep backups in another account or region, immutable or access-restricted, encrypted, with keys recoverable separately.
- A backup never restored is unproven; restore time depends on data size and often exceeds expectations.

**Show** Decision table mapping RPO bands (hours, minutes, near zero) to approaches: nightly backup, log shipping or WAL archiving with PITR, async replica, synchronous replica; verify the features of your database version before recording.

**Check:** Why test restores? *(An untested backup may be corrupt or too slow to meet the RTO.)*

---

## SRC-013-L04 · Failover design (12 min)
**Goal:** design failover that works and is safe.

**Key points**
- Topologies: backup and restore, pilot light, warm standby, active-active; cost and RTO fall in that order.
- Failover decisions: automatic (fast, risk of false triggers and split brain) versus manual (slower, deliberate).
- Split brain: two nodes both think they are primary; prevent with fencing and a single authority.
- Recovery depends on more than the database: DNS and traffic switching, secrets, configuration, certificates, access paths, and application readiness.
- Failing back is a separate plan.

**Show** A diagram description: primary region and a warm standby, with data replication, DNS or traffic manager, secrets replicated, runbook steps with owners and timings.

**Check:** What is split brain? *(Two nodes both acting as primary and accepting writes.)*

---

## SRC-013-L05 · Recovering event streams and derived data (10 min)
**Goal:** recover Kafka and caches and rebuild stores derived from the source of truth.

**Key points**
- Identify the source of truth (the orders database) and what is derived (search index, caches, read models, analytics).
- Kafka: replicate across zones or clusters (for example mirroring); consumer offsets need translating or resetting on failover; at-least-once replay means consumers must be idempotent.
- Caches are rebuilt; protect the database from a cold-cache stampede during recovery.
- Derived stores need a tested rebuild path from the source of truth and a time estimate.

**Show** Table: store | source or derived | recovery method | rebuild time. Rebuild path for search: replay orders table or the event log into the index.

**Check:** Why must consumers be idempotent after failover? *(Replays can deliver the same event again.)*

---

## SRC-013-L06 · Recovery exercises (10 min)
**Goal:** design drills that produce measured results.

**Key points**
- Progression: tabletop, restore into a sandbox, partial failover, full game day.
- Measure actual RTO and RPO with timestamps; record gaps.
- Include the awkward parts: finding credentials, paging the right people, DNS time to live.
- Every drill ends with a report and tracked remediation; repeat on a schedule.

**Show** Drill report outline: scenario, start time, steps with durations, achieved RTO and RPO, surprises, actions with owners and dates.

**Check:** Why record timestamps during a drill? *(To measure real RTO and show where time went.)*

---

## SRC-013-L07 · Demo: recovering the order database within a 15-minute RTO (15 min)
**Goal:** restore the order database against the clock; prepares SRC-013-LAB1.

**Steps**
1. State the scenario (primary database lost) and start the timer; confirm the RPO target.
2. Choose the path: promote the replica or restore from the latest backup plus logs; justify.
3. Execute the runbook steps, noting each duration; repoint the application via configuration or DNS.
4. **Planned mistake:** the restored database starts but the application cannot connect, because the secret rotated in the primary region was not replicated. Fix: add secret replication and a runbook step.
5. Verify data loss against the RPO and run smoke tests; stop the timer.
6. Compare with 15 minutes and list improvements.

**Check:** Which clock matters when judging the drill? *(Time from failure to verified service, not time to database start.)*

---

## SRC-013-L08 · Demo: rebuilding derived data after a Kafka cluster loss (15 min)
**Goal:** recover derived data when the event cluster is lost; prepares SRC-013-LAB1.

**Steps**
1. Declare the scenario: the Kafka cluster is lost; the orders database is intact.
2. Stand up a new cluster and recreate topics from configuration as code.
3. Rebuild the search index and read models from the orders database; measure rate and total time.
4. **Planned mistake:** resume consumers from the latest offset and silently skip a gap of events. Fix: backfill from the source of truth for the gap window and reconcile counts.
5. Warm caches gradually to protect the database.
6. Record the timeline, the data gap, and the remediation actions.

**Check:** What is the safe source for a rebuild? *(The source of truth, not another derived store.)*
