# SRB-017 · Large migrations — Lecture scripts

**Video:** 94 min · **Running case:** *The FulfillCo integration* — the engineer leads the four-team program planned in SRB-P1 through delivery; role-players act as team leads, product, finance, and security.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRB-017-L01 · Anatomy of a large migration (10 min)
**Goal:** break a migration into reversible phases with measurable checkpoints.

**Key points**
- Phases: prepare, build new path, run in parallel, shift traffic, verify, decommission.
- Every phase has an entry check, a measurable exit check, and a rollback.
- Prefer many small reversible steps over one big cut-over.
- Name an owner for each phase and a single place that shows current status.

**Show** Phase table: phase | change | exit measure | rollback. Example: *shadow read | compare shipment status old vs new | mismatch rate below threshold | stop shadow, no user impact.* This follows the extraction phases planned in SRB-008.

**Check:** What must every phase have? *(An exit measure and a rollback.)*

---

## SRB-017-L02 · Rollout strategies (12 min)
**Goal:** pick a way to shift traffic that limits risk.

**Key points**
- Canary: a small share of traffic to the new path, widened as checks pass.
- Blue-green: switch between two full environments; fast rollback, higher cost.
- By tenant, region, or cohort: move one group at a time to learn safely.
- Match strategy to risk: reads before writes, internal users before customers.
- Define go and stop criteria before the rollout starts.

**Show** Strategy table: strategy | when to use | rollback speed | cost. Add a rollout plan: 1% internal, 5% customers in one region, 25%, 100%, with a bake time per step.

**Check:** Why migrate reads before writes? *(Reads are easier to compare and to reverse.)*

---

## SRB-017-L03 · Shadow traffic and comparison (12 min)
**Goal:** compare old and new paths in production without affecting users.

**Key points**
- Shadow traffic: send a copy of requests to the new path and discard its answer, or compare it with the old one.
- Compare results and measure mismatch rate; classify mismatches (expected differences versus bugs).
- Be careful with side effects: shadow paths must not write, send messages, or charge.
- Measure latency and load impact of the shadow itself.
- Set a mismatch threshold for cut-over in advance.

**Show** A comparison report: total compared, matches, mismatches by category (timing, format, missing data, bug), trend per day against the threshold.

**Check:** What must a shadow path never do? *(Cause side effects such as writes, messages, or payments.)*

---

## SRB-017-L04 · Feature flags at program scale (10 min)
**Goal:** use flags across teams without leaving a mess.

**Key points**
- Flags decouple deploy from release and give instant rollback of behavior.
- At program scale: name flags consistently, record an owner and purpose, and list them in one registry.
- Each migration flag has an expiry or removal date and a ticket.
- Avoid flag interactions: document which flags depend on which, and test key combinations.
- Remove flags promptly after cut-over; leftover flags become hidden code paths.

**Show** Flag registry rows: name | owner | purpose | default | created | remove-by | removal ticket.

**Check:** Why set a remove-by date at creation? *(To stop migration flags living for years as hidden complexity.)*

---

## SRB-017-L05 · Backfills (12 min)
**Goal:** copy large volumes of historical data safely.

**Key points**
- Throttle: limit rate so production is not hurt; make it adjustable at runtime.
- Idempotency: running a batch twice gives the same result; use upserts and stable keys.
- Resumability: checkpoint progress so you can stop and restart.
- Verification: row counts, checksums or sample comparisons; reconcile continuously with live writes.
- Plan the order and the handling of data that changes during the backfill.

**Show** Backfill job outline: read batch by key range, transform, upsert, record checkpoint, sleep to meet the rate limit; verify with counts per range.

**Check:** Why must a backfill be idempotent? *(So retries and restarts do not duplicate or corrupt data.)*

---

## SRB-017-L06 · Decommissioning (8 min)
**Goal:** turn off the legacy path and prove it is unused.

**Key points**
- Prove no traffic: logs, metrics, or access attempts over a full business cycle.
- Stage the shutdown: block with notice, scream test where acceptable, then remove.
- Keep a data archive and rollback window for a defined period.
- Remove code, flags, dashboards, alerts, access, and cost items.
- Declare it done only when the legacy cost and risk are gone.

**Show** Decommission checklist with owners and dates: traffic zero, notice sent, disabled, archive taken, code and infrastructure removed, flags removed, cost confirmed.

**Check:** How do you prove a legacy path is unused? *(Observed zero traffic over a full business cycle, and a staged shutdown.)*

---

## SRB-017-L07 · Demo: shadow-reading shipment status from both systems (15 min)
**Goal:** run a shadow read of shipment status comparing old and new systems; prepares SRB-017-LAB1.

**Steps**
1. Define the comparison key, fields to compare, and the mismatch threshold for cut-over.
2. Route a copy of read requests to the new path behind a flag; log both results.
3. Review the mismatch report by category after a day of traffic.
4. **Planned mistake:** treat a timing difference as a bug and chase it. Fix: classify expected differences (event delay) and compare after a settle window.
5. Fix a real mismatch (status mapping) and watch the rate fall below the threshold.
6. Record the decision: ready for 5% serving, with a rollback via flag.

**Check:** What must be defined before shadow reads begin? *(The comparison fields and the mismatch threshold.)*

---

## SRB-017-L08 · Demo: a backfill that has to be stopped and resumed (15 min)
**Goal:** pause and resume a backfill when production load rises; prepares SRB-017-LAB1.

**Steps**
1. Start the backfill with checkpoints and a rate limit; show dashboards for source load.
2. Observe database latency rising during a business peak.
3. Lower the rate, then stop the job; confirm the checkpoint.
4. **Planned mistake:** restart from the beginning and duplicate rows. Fix: resume from the checkpoint; confirm idempotent upserts prevent duplicates.
5. Resume at a lower rate off-peak.
6. Verify with counts and checksums per key range, and write the result into the migration report.

**Check:** What makes a stop and resume safe? *(Checkpoints and idempotent writes.)*
