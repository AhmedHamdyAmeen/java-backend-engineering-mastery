# Level 4 — Senior Backend Engineer, Grade C: Interview Preparation

The questions most often asked when hiring a senior backend engineer who will own a significant subsystem, how to answer them, and where in this course you learned and practiced each one.

**How to use this guide**
1. Answer each question **out loud and on a whiteboard** before reading the answer. Senior interviews test how you reason, not what you remember.
2. If you struggle, revisit the module in **Learned in** and redo the lab in **Practiced in**.
3. Prepare the **Show it** line twice: once from your capstone (`SRC-CAP`) and once from your real work (the module's *Workplace evidence*). Senior interviewers probe for the second; the capstone fills gaps, it does not replace them.

> **About "How often":** frequencies reflect commonly reported interview patterns for senior backend roles, not measured statistics. Check them against current job posts in your target market and update this guide when the market moves.

---

## 1. What the market asks for — and where you proved it

| Skill employers list | Learned in | Proven by |
| --- | --- | --- |
| System design for scale and availability | SRC-001 … SRC-009 | `SRC-003-LAB1` option analysis, `SRC-CAP` redesign |
| Capacity planning and performance modeling | SRC-004, SRC-005 | `SRC-004-LAB1` 10× capacity plan, `SRC-005-LAB1` latency budget |
| Database scaling | SRC-007, MID-013, MID-015 | `SRC-007-LAB1` order data at 10× |
| Reliability: SLOs, readiness, DR | SRC-011, SRC-012, SRC-013 | `SRC-012-LAB1`, `SRC-013-LAB1` DR drill |
| Production troubleshooting and performance | SRC-015, SRC-016 | `SRC-015-LAB1` mystery outages, `SRC-016-LAB1` |
| Data correctness across services | SRC-014, MID-029, MID-031 | `SRC-014-LAB1` reconciliation |
| Security-minded design | SRC-018, MID-052 | `SRC-018-LAB1` secure design review |
| Incident leadership | SRC-019 | `SRC-019-LAB1` game-day command |
| Mentoring and technical leadership | SRC-020, SRC-017 | `SRC-020-LAB1`, `SRC-017-LAB1` debt pitch |
| Written design communication | SRC-010, SRC-003 | `SRC-010-LAB1` architecture pack |

**Your portfolio at the end of Level 4:** the `SRC-CAP` package — requirements, ADRs, capacity plan, load-test evidence, DR drill report, runbooks, and the recorded handover — plus a written account of at least three pieces of workplace evidence (a launch, an incident, an engineer you mentored).

## 2. How senior interviews usually run

| Round | What happens | What they check | Prepare with |
| --- | --- | --- | --- |
| Recruiter / hiring manager screen | Scope of past work | Ownership, impact, level fit | Q13, Q14, your project pitch |
| System design (1–2 rounds) | 45–60 min open design problem | Structured reasoning, trade-offs, depth | Q1–Q6 |
| Past-work deep dive | One system you owned, in detail | Real ownership vs participation | Q7–Q10 |
| Coding | Practical coding or code review | Still hands-on, clean code | Junior and Mid guides |
| Behavioral / leadership | Incidents, conflict, mentoring, mistakes | Judgment and influence | Q11–Q14 |

**The design framework used in every design question below:**
1. **Requirements** — clarify functional scope and nonfunctional targets; write them down.
2. **Estimates** — traffic, data size, peak factor; order of magnitude is enough.
3. **High-level design** — components, data ownership, sync vs async flows.
4. **Deep dives** — the one or two parts the interviewer cares about (data model, consistency, hot paths).
5. **Failure modes** — what breaks, how you detect it, how the system degrades.
6. **Trade-offs** — what you chose, what you rejected, and what would change your mind.

---

## 3. System design

### Q1 · Design an order and payment system that stays available during a payment-provider outage and never double-charges.
**How often:** Very common · **Round:** System design

**How to answer:** apply the framework; the interviewer is testing correctness under partial failure.
- **Requirements:** checkout availability target (e.g., 99.95%), no lost orders, no double charges, payment confirmation can be asynchronous.
- **Estimates:** peak orders per second from the business forecast, payment call latency, retry volume during an outage.
- **High-level design:** order service persists the order and an outbox event in one transaction; a payment worker calls the provider with an **idempotency key** per order; results come back as events; the order saga moves `PLACED → PAID` or compensates.
- **Deep dives:** idempotency at the provider and in your consumer; the saga's timeout path; reconciliation against the provider's settlement report.
- **Failure modes:** provider down → orders accepted as "payment pending", circuit breaker open, queued retries with backoff; provider succeeded but response lost → the idempotency key makes the retry safe; consumer crash → at-least-once delivery plus idempotent handling.
- **Trade-offs:** accepting orders while payment is pending improves availability but needs clear customer messaging and cancellation if payment finally fails.

**Common trap:** promising "exactly-once" from Kafka or the database. Say "at-least-once delivery with exactly-once *effects* via idempotency and reconciliation".

**Learned in:** SRC-009, SRC-014, MID-029, MID-031, MID-033
**Practiced in:** `SRC-009-LAB1`, `SRC-014-LAB1`, `SRC-CAP`
**Show it:** the capstone's reconciliation job and FMEA; at work, a reconciliation or idempotency fix you introduced.

---

### Q2 · Your main database will hit its limits within a year at 10× growth. How do you scale it?
**How often:** Very common · **Round:** System design

**How to answer:** walk the scaling ladder and justify each step with evidence.
1. **Measure first:** which resource saturates (CPU, IO, connections, storage), from which queries.
2. **Cheap wins:** query and index fixes, connection pooling, caching hot reads.
3. **Read replicas** for read-heavy paths — and design for replication lag (read-your-writes where needed).
4. **Partitioning** large tables (e.g., orders by month) for maintenance and pruning.
5. **Vertical scaling** — often the cheapest next step; say so.
6. **Sharding** only when the write volume of one primary is the limit: choose a shard key that keeps the most common query on one shard, quantify hot-partition risk, plan resharding.
7. Consider managed distributed SQL and compare operational cost.

**Common trap:** jumping straight to sharding or NoSQL. Interviewers reward exhausting simpler options and quantifying when they run out.

**Learned in:** SRC-007, SRC-004, MID-013, MID-019
**Practiced in:** `SRC-007-LAB1`, `SRC-004-LAB1`
**Show it:** your ADR for order data at 10×; at work, a database scaling change you designed or reviewed.

---

### Q3 · Checkout must meet a p99 latency of 300 ms. How do you design and verify that?
**How often:** Common · **Round:** System design, deep dive

**How to answer:**
- Split the end-to-end budget across hops (gateway, services, database, external calls), leaving headroom.
- Watch **fan-out**: with several parallel calls, the slowest dominates the tail; reduce calls or make them concurrent with deadlines.
- Use **Little's Law** to size thread pools, connection pools, and consumers for target throughput.
- Keep utilization well below saturation, where queueing makes latency explode.
- Verify with a load test at forecast peak, reporting percentiles, and add a regression check in CI.

**Common trap:** budgeting with averages; ignoring retries, which add latency exactly when things are slow.

**Learned in:** SRC-005, SRC-016, MID-046
**Practiced in:** `SRC-005-LAB1`, `SRC-016-LAB1`
**Show it:** the capstone's before/after p99 evidence; at work, a performance target you set or met with a model.

---

### Q4 · Estimate the capacity needed for a flash sale: 2 million users in one hour.
**How often:** Common · **Round:** System design (estimation part)

**How to answer:** state assumptions, compute, sanity-check.
- 2M users/hour ≈ 550 users/s on average; assume a peak factor (e.g., 5× in the first minutes) → ~2,800 users/s.
- Requests per user session (browse, cart, checkout) → requests/s per service.
- Conversion rate → orders/s → database writes/s, Kafka messages/s, payment calls/s.
- Storage: order size × orders; replication and retention multipliers.
- Compare with measured per-instance capacity from load tests → instances, pool sizes, partitions; name the first bottleneck.

**Common trap:** precision theater. Interviewers want explicit assumptions and the right order of magnitude, not five significant digits.

**Learned in:** SRC-004, SRC-005
**Practiced in:** `SRC-004-LAB1`
**Show it:** a capacity estimate you made and later compared with reality.

---

### Q5 · How would you make this system resilient to failures? Walk me through your failure-mode analysis.
**How often:** Very common · **Round:** System design follow-up

**How to answer:**
- Map dependencies, including hidden ones (DNS, identity provider, config service, shared clusters).
- For each: what fails, likelihood, impact, how you **detect** it.
- Mitigations: timeouts, retries with jitter, circuit breakers, bulkheads, fallbacks, graceful degradation that drops features rather than the whole product.
- Prove it: failure-injection experiments, then fix what they find.

**Common trap:** listing patterns without saying which failure each one addresses; degradation that silently corrupts data.

**Learned in:** SRC-009, MID-033
**Practiced in:** `SRC-009-LAB1`
**Show it:** the weakness your capstone's failure injection found; at work, a game day or failure review you led.

---

### Q6 · What are RPO and RTO, and how would you meet "15 minutes to recover, at most 1 minute of data loss"?
**How often:** Common · **Round:** System design, reliability

**How to answer:**
- **RPO:** maximum data loss measured in time. **RTO:** maximum time to restore service.
- RPO 1 min → continuous WAL archiving / streaming replication to another zone or region, not nightly backups.
- RTO 15 min → automated or rehearsed failover, infrastructure as code, secrets and DNS included in the plan.
- Remember derived data (caches, search indexes, read models) and event streams: how are they rebuilt?
- Prove it with a **timed drill**, not a document.

**Common trap:** RTO targets never measured; forgetting that a restore takes longer than a backup.

**Learned in:** SRC-013, MID-018
**Practiced in:** `SRC-013-LAB1`
**Show it:** the capstone's DR drill report with measured times; at work, a recovery exercise you ran.

---

## 4. Ownership and production

### Q7 · How do you know a service is ready for production?
**How often:** Common · **Round:** Past-work deep dive

**How to answer:** describe a readiness review and its evidence.
- Observability: dashboards, alerts tied to SLOs, runbooks.
- Capacity tested at forecast peak; failure modes analysed.
- Safe delivery: canary, automated verification, rollback — including for data changes.
- Security review done; on-call and ownership defined.
- Explicit go/no-go criteria agreed before launch day.

**Common trap:** "QA signed off". Readiness is about operating the service, not only about features working.

**Learned in:** SRC-011, SRC-012
**Practiced in:** `SRC-011-LAB1`, `SRC-012-LAB1`
**Show it:** the capstone's canary that halted a seeded regression; at work, a launch you led.

---

### Q8 · Tell me about the hardest production issue you debugged.
**How often:** Very common · **Round:** Past-work deep dive, behavioral

**How to answer (STAR):**
- **Situation:** impact in user and business terms.
- **Task:** your role — senior answers show you *led* the investigation.
- **Action:** hypotheses, evidence (traces, thread dumps, pool metrics, query plans), how you ruled things out, and how you stopped the bleeding first.
- **Result:** root cause across layers, the fix, and the systemic change (alert, test, runbook) that prevents recurrence.
- What a senior answer must show: method under pressure, not luck.

**Common trap:** a story that ends at "we restarted it and it went away".

**Learned in:** SRC-015, MID-008, MID-047
**Practiced in:** `SRC-015-LAB1`
**Show it:** one of the capstone's mystery-outage write-ups; at work, a hard investigation you led and wrote up.

---

### Q9 · How do you guarantee data stays consistent across services?
**How often:** Common · **Round:** System design, deep dive

**How to answer:**
- Name the invariants that span services (order paid ⇔ payment captured).
- **Prevent** where possible (outbox, idempotent consumers, sagas with compensations).
- **Detect** what you cannot prevent (reconciliation jobs against each other and external systems).
- **Repair** with audited, idempotent corrections.
- Distinguish exactly-once delivery (not available end to end) from exactly-once effects (designable).

**Learned in:** SRC-014, MID-029, MID-031
**Practiced in:** `SRC-014-LAB1`, `SRC-CAP`
**Show it:** the discrepancy types your reconciliation found; at work, an integrity check you introduced.

---

### Q10 · How do you decide which technical debt to pay down?
**How often:** Common · **Round:** Hiring manager, behavioral

**How to answer:**
- Make the **interest** concrete: incident minutes, lead time, onboarding time, cloud cost.
- Prioritize by cost of delay and risk, in a visible register.
- Pay down incrementally alongside features; avoid big rewrites.
- Make the business case in business terms and show the result afterwards.

**Common trap:** "we need a rewrite"; debt lists without costs.

**Learned in:** SRC-017
**Practiced in:** `SRC-017-LAB1`
**Show it:** the debt item the capstone's role-played leadership approved; at work, a debt item you got funded and delivered.

---

### Q11 · How do you review a design for security?
**How often:** Common · **Round:** System design follow-up

**How to answer:**
- Data-flow diagram with trust boundaries; STRIDE per boundary.
- Verify authorization end to end — user to service, service to service, service to data.
- Rate risks by likelihood × impact; agree mitigations or explicit acceptance with an owner.
- Turn the top threats into tests.

**Learned in:** SRC-018, MID-052
**Practiced in:** `SRC-018-LAB1`
**Show it:** findings from the capstone's peer review; at work, a security review you led.

---

## 5. Leadership and behavior

### Q12 · Tell me about an incident where you were the incident commander.
**How often:** Very common · **Round:** Behavioral

**How to answer (STAR):** show coordination, not heroics.
- Roles you assigned, how you kept responders focused on mitigation first.
- Stakeholder updates at a steady cadence.
- A risky decision you made with incomplete information and why.
- The blameless postmortem and the actions that were actually completed.

**Common trap:** describing yourself debugging while nobody coordinated.

**Learned in:** SRC-019, MID-050
**Practiced in:** `SRC-019-LAB1`
**Show it:** the capstone's commanded game day; at work, an incident you led.

---

### Q13 · How have you helped another engineer grow?
**How often:** Very common · **Round:** Behavioral, hiring manager

**How to answer (STAR):**
- Who, their starting point, and the goal you agreed.
- How you delegated work at the right size and coached through reviews instead of rewriting.
- Their measurable growth (scope, independence) and what you learned about mentoring.

**Common trap:** "I answered their questions" — that is support, not mentoring.

**Learned in:** SRC-020, MID-066
**Practiced in:** `SRC-020-LAB1`
**Show it:** mentee feedback from the course; at work, an engineer whose scope grew with your help.

---

### Q14 · Tell me about a design decision you got wrong.
**How often:** Common · **Round:** Behavioral

**How to answer (STAR):** honesty and learning are the point.
- The decision and the reasoning at the time (with what you knew then).
- How you discovered it was wrong — ideally through data, not an outage.
- What you did to correct it and limit the damage.
- What you changed in how you decide (e.g., you now record assumptions in ADRs and revisit them).

**Common trap:** a fake weakness ("I cared too much about quality"), or blaming others.

**Learned in:** SRC-003, SRC-010
**Practiced in:** `SRC-003-LAB1`
**Show it:** an ADR whose consequences section you later updated; at work, a decision you reversed.

---

## 6. Six-week preparation plan

| Week | Focus | Do this |
| --- | --- | --- |
| 1 | Design framework | Practice the six-step framework on Q1 and Q2 on a whiteboard, timed to 45 minutes |
| 2 | Estimation and performance | Q3–Q4; redo `SRC-004-LAB1` without notes; three estimation drills |
| 3 | Reliability | Q5–Q7, Q9; reread your capstone's FMEA and DR drill |
| 4 | Past-work deep dive | Write one-page stories for Q8, Q10, Q11 from real work, backed by the capstone where real work is thin |
| 5 | Leadership stories | Q12–Q14 in STAR form; practice with a peer acting as the hiring manager |
| 6 | Mocks | Two full mock loops (design + deep dive + behavioral) using the Senior C interview simulation |

**Ready when:** you can run the design framework on an unseen problem in 45 minutes with explicit trade-offs, defend every number in your capstone, and tell three real ownership stories (a launch, an incident, a mentee) with outcomes.
