# ARC-037 · Migration strategy — Lecture scripts

**Video:** 71 min · **Running case:** *Larkspur Retail* — a fictional 120-store retailer replacing its dated on-premises web shop with a web and mobile platform (inventory, payments, fulfillment, customer service, reporting) integrated with the existing ERP and CRM. You are the solution architect.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## ARC-037-L01 · Cutover approaches (12 min)
**Goal:** compare cutover approaches and choose one with justification.

**Key points**
- Big bang: everything switches at once; fast, but highest risk and hardest rollback.
- Phased by capability: move catalog, then checkout, then returns; needs coexistence.
- Phased by store or region: pilot stores first, then waves; limits blast radius.
- Parallel run: both systems run and results are compared; safe but costly and needs reconciliation.
- Choose by business risk tolerance, data coupling, peak calendar, and team capacity.

**Show:** a decision table: approach, risk, cost, rollback ease, coexistence needed, suits Larkspur because.

**Check:** Why might a retailer avoid a big bang before the holiday season? *(A failure would hit peak revenue and rollback is hardest.)*

---

## ARC-037-L02 · Coexistence of old and new (10 min)
**Goal:** design how old and new systems work together during migration.

**Key points**
- Decide for each data set which system is the master at each stage; never two masters.
- Routing: a facade or gateway sends traffic by capability, store, or customer group.
- Synchronization: events or CDC between old and new, with conflict rules.
- Coexistence has a cost and an end date; plan decommissioning of bridges.

**Show:** a diagram: customers, gateway, old shop and new platform, a sync service, ERP at the back; a table of "master by phase".

**Check:** What is the biggest coexistence risk? *(Two systems both changing the same data, with no single master.)*

---

## ARC-037-L03 · Data migration (12 min)
**Goal:** plan data migration through mapping, cleansing, trial loads, validation, and final load.

**Key points**
- Map source fields to target model; record decisions on what is dropped or transformed.
- Cleanse early: duplicates, invalid addresses, old inactive customers (check retention rules).
- Trial loads: run the full migration several times, time it, and validate.
- Validation: counts, checksums, business samples, and reconciliation with finance totals.
- Final load: rehearsed, timed, with a delta strategy for changes since the last trial.

**Show:** a plan timeline: mapping, trial 1, trial 2, trial 3 (timed), dress rehearsal, final load, validation, sign-off.

**Check:** Why run several trial loads? *(They expose mapping errors, bad data, and timing before the real cutover.)*

---

## ARC-037-L04 · Rollback and go/no-go (10 min)
**Goal:** define rollback plans and go/no-go criteria for each cutover.

**Key points**
- Go/no-go criteria are measurable and agreed before the event: test results, migration validation, staffing, support readiness.
- Every step has a decision owner and a rollback with a point of no return.
- Rollback must handle data written after cutover (orders taken on the new system).
- Rehearse rollback; an untested rollback is a hope.

**Show:** a cutover runbook extract: step, owner, success check, rollback action, time budget, last safe rollback point.

**Check:** What is often missing from rollback plans? *(Handling of data created in the new system after cutover.)*

---

## ARC-037-L05 · Demo: migrating Larkspur's customers and orders from the old web shop (14 min)
**Goal:** worked migration design for customers and orders; prepares ARC-037-LAB1.

**Steps**
1. Inventory the old shop's data: customers, addresses, order history, wishlists, passwords (hashed).
2. Map to the new model and decide scope: active customers plus order history for the retention period (confirm with legal).
3. Plan trial loads with validation: counts, order totals by month against finance, sampled customer checks.
4. **Planned mistake:** plan one final load over a weekend without trial loads. Fix: three timed trial loads plus a dress rehearsal and a delta load for changes after the last extract.
5. Handle password hashes (migrate with re-hash on first login or force reset; security review) and customer communication.

---

## ARC-037-L06 · Demo: a pilot-store rollout and its rollback plan (13 min)
**Goal:** worked rollout for pilot stores with a defined rollback; prepares ARC-037-LAB1.

**Steps**
1. Choose three pilot stores: different sizes and connectivity; stakeholders agree the success measures.
2. Define go/no-go criteria: till tests passed, staff trained, support on site, data validated.
3. Run the cutover for the stores with the runbook; monitor sales, errors, and queue times.
4. **Planned mistake:** a rollback plan that restores the old till configuration but ignores sales recorded on the new system. Fix: define how new-system sales are exported and replayed, with an owner.
5. Review after two weeks; decide the next wave using the exit criteria.
