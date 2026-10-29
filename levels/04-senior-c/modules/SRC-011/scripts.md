# SRC-011 · Production readiness — Lecture scripts

**Video:** 94 min · **Running case:** *Order Processing at 10×* — Shop Platform's order subsystem must handle a 10× growth forecast, a 99.95% availability commitment, and a 15-minute recovery objective.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRC-011-L01 · Why launches fail (10 min)
**Goal:** name the recurring causes of failed launches so a review can target them.

**Key points**
- Most launch failures are not bugs in the happy path: they are missing alerts, untested capacity, unrehearsed rollback, and unclear ownership.
- Big-bang cutovers hide the cause: too many changes land at once to tell which one broke things.
- "Done" meant "merged", not "operable": nobody asked who is paged and what they do.
- Launch pressure turns checklists into paperwork when the decision is already made.

**Show** A table of three past launches (yours or public postmortems): trigger, what was missing (alert, capacity, rollback, owner), and which readiness question would have caught it.

**Check:** Why is a big-bang launch harder to debug than a staged one? *(Many changes land together, so a failure cannot be attributed to one of them.)*

---

## SRC-011-L02 · The readiness review (14 min)
**Goal:** run a review that covers observability, capacity, failure handling, security, and support.

**Key points**
- Five areas, each with questions that need evidence, not opinions: dashboards and alerts exist; load test passed at forecast; dependency failure tested; threat review done; on-call runbook and owner named.
- Evidence is a link or a result, not "we think so".
- Findings get a severity: blocker, must-fix-soon, accepted risk with a named owner.
- The review happens before the launch date is fixed, and it is a conversation with the service team, not an audit of them.

**Show** One-page review template: area | question | evidence link | status | owner. Example row: *Failure handling | what happens when the payment provider times out? | chaos test result | pass | owner: orders team.*

**Check:** What distinguishes evidence from opinion in a review? *(Evidence is something checkable, such as a test result or dashboard link.)*

---

## SRC-011-L03 · Progressive delivery and canaries (12 min)
**Goal:** limit the blast radius of a change by exposing it gradually.

**Key points**
- Progressive delivery: release to a small share of traffic, watch, then widen (for example 1%, 10%, 50%, 100%).
- Canary: a small group running the new version beside the old one, compared on the same traffic.
- Feature flags separate deploy (code present) from release (behavior on); both can be staged.
- Choose the canary population with care: representative traffic, enough volume to detect a difference, and a clear bake time per stage.

**Show** Rollout plan table: stage | traffic | bake time | metrics compared | promote rule. Mention tools by role (service mesh or ingress weights, a rollout controller, a flag service); verify tool versions before recording.

**Check:** What is the difference between deploying and releasing with a feature flag? *(Deploy puts the code in production; release turns the behavior on for users.)*

---

## SRC-011-L04 · Automated verification and rollback (10 min)
**Goal:** let metrics, not people at 2 a.m., decide whether to continue or revert.

**Key points**
- Pick a few guard metrics: error rate, latency percentile, saturation, and one business metric such as orders completed.
- Compare canary against baseline over the same window, with a tolerance that accounts for noise.
- Automate the abort: a failed check reverts traffic without waiting for a human.
- Rehearse rollback; an untested rollback is a hope, not a plan.

**Show** Analysis rule in words: *abort if canary 5xx rate exceeds baseline by more than 0.5 points for 5 minutes, or p99 is more than 20% worse, or order completion drops below baseline minus 2%.* Thresholds are examples to tune.

**Check:** Why include a business metric next to technical ones? *(A change can return 200s yet break checkout outcomes.)*

---

## SRC-011-L05 · Rolling back data (10 min)
**Goal:** make data changes reversible, not just code.

**Key points**
- Code rolls back in minutes; schema and data changes may not.
- Expand and contract: add new columns or tables first (expand), migrate, switch reads, and only later remove the old (contract).
- New code must tolerate the old schema and old code the new, so either version can run during rollout.
- When a change is truly irreversible, say so in the review, take a backup or snapshot, and require an explicit go decision.

**Show** Timeline: release N adds a nullable `status_v2` column and dual-writes; N+1 reads from it; N+2 drops the old column weeks later. Rollback at any step before N+2 is a deploy, not a restore.

**Check:** Why drop the old column in a later release? *(So rollback to earlier code stays possible while the new path is proven.)*

---

## SRC-011-L06 · Go/no-go decisions (8 min)
**Goal:** decide launches against criteria agreed in advance.

**Key points**
- Write the criteria before the review: blockers, thresholds, who decides.
- A no-go is a normal outcome with a dated plan to re-review, not a failure.
- Accepted risks are recorded with an owner and an expiry date.
- Decide with the facts available; do not let sunk cost or a calendar commitment change the criteria.

**Show** Decision record: criteria met/unmet, accepted risks, decision, decider, date, re-review condition.

**Check:** Why agree criteria before the review? *(So pressure at decision time cannot move the bar.)*

---

## SRC-011-L07 · Demo: a canary that catches a regression (15 min)
**Goal:** run a canary where automated analysis halts a seeded regression; prepares SRC-011-LAB1.

**Steps**
1. State the change on the order subsystem and the guard metrics with thresholds.
2. Deploy the new version at 5% traffic; show baseline and canary dashboards side by side.
3. Seed the regression (a slow query that raises p99 under load) and apply realistic traffic.
4. Watch the analysis fail at the first stage and traffic revert automatically; read the verdict.
5. **Planned mistake:** use a canary too small and too short to see the difference, so the bad version passes. Fix: raise volume and bake time to match the detection need.
6. Record what the run proved and what it could not.

**Check:** What makes a canary stage trustworthy? *(Enough traffic and time to detect the difference you care about.)*

---

## SRC-011-L08 · Demo: a readiness review that says no-go (15 min)
**Goal:** run a review on the redesigned order subsystem and reach a defensible no-go; prepares SRC-011-LAB1.

**Steps**
1. Open the template and agree go/no-go criteria with the team first.
2. Walk the five areas, asking for evidence links as you go.
3. Find blockers: no rollback rehearsal for the schema change, no alert for payment timeouts.
4. **Planned mistake:** accept "we will add the alert after launch". Fix: mark it a blocker or an accepted risk with an owner and an expiry.
5. Record the no-go, the fixes needed, and the re-review date.
6. Discuss how to deliver the decision constructively to the team and to product.

**Check:** What should replace an unwritten promise to fix later? *(A tracked item with an owner and a date, or a blocker.)*
