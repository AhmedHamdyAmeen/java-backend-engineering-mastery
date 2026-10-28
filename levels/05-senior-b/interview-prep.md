# Level 5 — Senior Backend Engineer, Grade B: Interview Preparation

The questions most often asked when hiring a senior engineer who will lead cross-team technical initiatives and evolve existing architectures, how to answer them, and where in this course you learned and practiced each one.

**How to use this guide**
1. Answer each question **out loud and on a whiteboard** before reading the answer. At this level, interviewers listen for trade-offs and for how you bring other teams along.
2. If you struggle, revisit the module in **Learned in** and redo the lab in **Practiced in**.
3. Prepare the **Show it** line twice: once from your capstone (`SRB-CAP`, the FulfillCo integration) and once from your real work (the module's *Workplace evidence*). Cross-team leadership claims are probed hard; have names of teams, dates, and outcomes ready.

> **About "How often":** frequencies reflect commonly reported interview patterns for senior and lead backend roles, not measured statistics. Check them against current job posts in your target market and update this guide when the market moves.

---

## 1. What the market asks for — and where you proved it

| Skill employers list | Learned in | Proven by |
| --- | --- | --- |
| Event-driven architecture | SRB-001, SRB-002 | `SRB-002-LAB1` integration events, `SRB-CAP` event catalog |
| Distributed data and multi-region design | SRB-003, SRB-004, SRB-005 | `SRB-004-LAB1` EU expansion, `SRB-005-LAB1` availability budget |
| Messaging at scale (Kafka) | SRB-006 | `SRB-006-LAB1` partner feed at scale |
| Legacy modernization and migrations | SRB-007, SRB-008, SRB-017 | `SRB-008-LAB1` migration plan, `SRB-017-LAB1` phase one executed |
| Platform and infrastructure decisions | SRB-009, SRB-010 | `SRB-009-LAB1` mesh decision, `SRB-010-LAB1` golden path |
| Leading cross-team technical work | SRB-011, SRB-012, SRB-018 | `SRB-011-LAB1` program design, `SRB-018-LAB1` |
| Technology evaluation | SRB-013 | `SRB-013-LAB1` workflow engine choice |
| Engineering metrics and cost | SRB-014, SRB-015 | `SRB-014-LAB1` program dashboard, `SRB-015-LAB1` cost per order |
| Security architecture | SRB-016 | `SRB-016-LAB1` merged trust model |
| Risk and stakeholder management | SRB-019, SRB-020 | `SRB-019-LAB1`, `SRB-020-LAB1` |

**Your portfolio at the end of Level 5:** the `SRB-CAP` package — target architecture with ADRs, event catalog, migration plan with phase-one results, risk register, DORA dashboard, cost analysis, and status reports — plus workplace evidence of a cross-team design you led and a migration you carried through to decommissioning.

## 2. How senior interviews at this level usually run

| Round | What happens | What they check | Prepare with |
| --- | --- | --- | --- |
| Hiring manager screen | Scope and impact of past initiatives | Cross-team scope, not only own-team work | Q8, Q12, your initiative pitch |
| System / architecture design | Evolve an existing system, often with legacy constraints | Migration thinking, trade-offs, risk | Q1–Q7 |
| Past-initiative deep dive | One multi-team project, end to end | Leadership, decisions, outcomes | Q8–Q11 |
| Behavioral / leadership | Conflict, influence, bad news, risk | Judgment without formal authority | Q12–Q14 |
| Coding (sometimes) | Practical coding or code review | Still credible hands-on | Mid guide |

**Design framework (as in Senior C), with one addition for this level:**
1. Requirements → 2. Estimates → 3. High-level design → 4. Deep dives → 5. Failure modes → 6. Trade-offs → **7. Path from today:** how you get there from the current system, in reversible steps, with which teams.

---

## 3. Architecture

### Q1 · How do you evolve event schemas when other teams consume your events?
**How often:** Very common · **Round:** Architecture design

**How to answer:**
- Treat events as a **published contract** with an owner, a schema in a registry, and a compatibility mode (usually backward or full).
- Additive changes (optional fields) are safe; removing or renaming fields, or changing meaning, is breaking.
- For breaking changes: publish a new event version (or topic) alongside the old one, migrate consumers, measure who still reads the old one, then retire it.
- Consumers act as tolerant readers; contract tests catch breaks before production.
- Mention replay: old events must still be readable, and replays must not trigger side effects again (emails, payments).

**Common trap:** "we version every change"; or exposing internal entity models as events.

**Learned in:** SRB-002, MID-062, SRC-006
**Practiced in:** `SRB-002-LAB1`, `SRB-CAP`
**Show it:** the capstone's Shop ↔ FulfillCo event catalog; at work, an event contract another team consumes.

---

### Q2 · When would you use CQRS or event sourcing, and when not?
**How often:** Common · **Round:** Architecture design

**How to answer:**
- **CQRS:** separate write and read models when read and write needs differ sharply (complex queries, very different scale). Often a read model updated from events is enough ("CQRS-lite").
- **Event sourcing:** store state as a sequence of events when the history itself is the business value (audit, temporal queries) or many projections are needed.
- Costs of event sourcing: schema evolution of stored events (upcasting), projection rebuild time, snapshots, harder ad-hoc queries, team learning curve.
- Default: state + outbox; choose event sourcing per aggregate with explicit justification.

**Common trap:** event sourcing the whole system because it is "more scalable".

**Learned in:** SRB-001, MID-022
**Practiced in:** `SRB-001-LAB1`
**Show it:** the shipment-tracking ADR comparing both; at work, a design where you chose the simpler pattern and could show why.

---

### Q3 · Active-active or active-passive across regions? Walk me through the decision.
**How often:** Common · **Round:** Architecture design

**How to answer:**
- Start from requirements per capability: RTO/RPO, latency for users in each region, data residency, consistency needs.
- **Active-passive:** simpler, consistent writes in one region, failover time and data loss bounded by replication; cheaper.
- **Active-active:** lower latency and faster failover, but writes in two places need conflict handling or partitioned ownership (e.g., each customer "homed" in one region).
- Do it **selectively**: only the capabilities that need it. Remember regional dependencies (identity, secrets, CI, DNS).
- Quantify cost and on-call burden.

**Common trap:** active-active everywhere; assuming the database "handles" multi-region conflicts.

**Learned in:** SRB-004, SRB-003, SRB-005
**Practiced in:** `SRB-004-LAB1`, `SRB-005-LAB1`
**Show it:** the EU expansion topology with residency enforced by design; at work, a multi-region or residency design you contributed to.

---

### Q4 · How would you migrate a large legacy monolith to services without downtime?
**How often:** Very common · **Round:** Architecture design

**How to answer:** use the design framework plus the "path from today" step.
- Pick a first capability with clear boundaries and real value — not the hardest one.
- **Strangler fig:** route that capability's traffic at the edge to the new service; **branch by abstraction** inside the monolith.
- Move data ownership deliberately; avoid **dual writes** (two systems writing the same data); use CDC or the outbox so one system is the writer at any time.
- Compare old and new paths with shadow traffic; cut over behind a feature flag; keep rollback per phase.
- Decommission the old path and prove it is unused.
- Name the teams involved and how you align them.

**Common trap:** a big-bang rewrite; dual writes "just for a while".

**Learned in:** SRB-008, SRB-017, SRC-008
**Practiced in:** `SRB-008-LAB1`, `SRB-017-LAB1`, `SRB-CAP`
**Show it:** the measured mismatch rate and decommissioned path from phase one; at work, a strangler step you led into production.

---

### Q5 · How do you integrate with a legacy system whose code you can't change?
**How often:** Common · **Round:** Architecture design

**How to answer:**
- **Change data capture** (e.g., Debezium on the database log) to stream changes without touching the application.
- Translate low-level CDC events into **domain events** in an anti-corruption layer — never expose raw tables as a public contract.
- Filter personal data; handle schema changes in the legacy database; monitor lag.
- Alternatives when CDC is not possible: polling with high-water marks, file drops with idempotent import.

**Common trap:** consumers coupled directly to legacy table structures.

**Learned in:** SRB-007, MID-029
**Practiced in:** `SRB-007-LAB1`
**Show it:** stock sync from the FulfillCo database without code changes; at work, a legacy integration you delivered.

---

### Q6 · Your Kafka consumers are six hours behind. What do you do now, and what do you change afterwards?
**How often:** Common · **Round:** Deep dive, operations

**How to answer:**
- **Now:** assess impact (which business flows are stale); check whether consumers are failing, slow, or rebalancing; scale consumers up to the partition count; pause non-critical consumers; protect downstream systems from the catch-up burst.
- **After:** right-size partitions for growth, lag alerts with clear actions, cooperative rebalancing / static membership, backpressure end to end, capacity plan for retention and throughput.

**Common trap:** adding consumers beyond the number of partitions; catching up so fast that the database behind the consumer falls over.

**Learned in:** SRB-006, MID-028
**Practiced in:** `SRB-006-LAB1`
**Show it:** the backlog-recovery plan and load test from the capstone; at work, a messaging scale problem you diagnosed or prevented.

---

### Q7 · How would you secure service-to-service communication across two merged organizations?
**How often:** Common · **Round:** Architecture design

**How to answer:**
- **Zero trust:** no trust from network location; every request authenticated and authorized.
- **Workload identity** (mTLS certificates from a mesh or SPIFFE-style identity) plus scoped tokens for authorization.
- Policy as code for who may call what; least-privilege data access per service.
- Separate identity boundaries for users, services, and partners; plan the merge of identity providers.

**Common trap:** "it's inside the VPC"; shared credentials across teams.

**Learned in:** SRB-016, SRB-009, MID-051
**Practiced in:** `SRB-016-LAB1`
**Show it:** the merged trust model reviewed by the security role-player; at work, a security architecture change you led.

---

## 4. Leading cross-team work

### Q8 · Tell me about a technical initiative you led across several teams.
**How often:** Very common · **Round:** Hiring manager, deep dive

**How to answer (STAR):** this is the defining Senior B question.
- **Situation:** business goal, number of teams, constraints.
- **Task:** your role — technical lead without formal authority over the teams.
- **Action:** how you mapped dependencies, ran the design process with every team, agreed interfaces and dates, handled a conflict, and kept leadership informed.
- **Result:** measurable outcomes against goals, and what you would do differently.
- A senior B answer shows **alignment work**, not only technical design.

**Common trap:** describing your own team's work and calling it cross-team.

**Learned in:** SRB-011, SRB-019, SRB-020
**Practiced in:** `SRB-011-LAB1`, `SRB-CAP`
**Show it:** the FulfillCo program's dependency map and outcomes report; at work, a cross-team design you led to agreement.

---

### Q9 · How do you evaluate a new technology before adopting it?
**How often:** Common · **Round:** Deep dive

**How to answer:**
- Start from the problem and weighted criteria, written before looking at products.
- Time-boxed proof of concept testing the riskiest assumptions, including failure behavior.
- Evaluation matrix including total cost and **exit cost**; operational burden and team skills.
- Make the decision in an ADR, including when you would revisit it.
- Mention a case where the answer was "no" — or "the simple option is enough".

**Common trap:** criteria chosen after picking a favorite; PoCs that only test the happy path.

**Learned in:** SRB-013, SRB-009
**Practiced in:** `SRB-013-LAB1`, `SRB-009-LAB1`
**Show it:** the workflow-engine evaluation with a three-year cost; at work, an evaluation you ran and the decision it produced.

---

### Q10 · Which engineering metrics do you track, and how do you use them?
**How often:** Common · **Round:** Hiring manager

**How to answer:**
- **DORA:** deployment frequency, lead time for changes, change failure rate, time to restore service.
- Pair with reliability indicators (SLO attainment, incident rate) so speed is not bought with stability.
- Use them to find constraints and run improvement experiments, never to rank teams (Goodhart's law).
- Give one example: metric → hypothesis → change → measured result.

**Common trap:** using metrics as targets for individuals.

**Learned in:** SRB-014
**Practiced in:** `SRB-014-LAB1`
**Show it:** the program dashboard and its improvement experiment; at work, an improvement you drove with metrics.

---

### Q11 · How would you reduce our cloud bill without hurting reliability?
**How often:** Common · **Round:** Architecture, hiring manager

**How to answer:**
- Attribute costs to services and teams (tagging); compute **unit economics** (cost per order).
- Go after the largest drivers first: idle or oversized compute, data transfer, storage tiers, over-provisioned managed services, logs and metrics volume.
- Levers: rightsizing, autoscaling, commitments for steady load, architectural changes (caching, batching).
- Check each saving against reliability and engineering time; never quietly remove redundancy.

**Learned in:** SRB-015, MID-056
**Practiced in:** `SRB-015-LAB1`
**Show it:** the capstone's cost-per-order before and after; at work, a cost reduction you delivered with numbers.

---

## 5. Leadership and behavior

### Q12 · Tell me about a time you had to tell leadership a project was late or at risk.
**How often:** Very common · **Round:** Behavioral

**How to answer (STAR):**
- When you saw the risk and how early you raised it.
- How you framed it in business impact, with **options** (scope, date, resources) and your recommendation.
- The decision leadership took and the outcome.
- What a senior answer shows: no surprises, honest status, a clear ask.

**Common trap:** "green" status until the week before the deadline; arriving with a problem and no options.

**Learned in:** SRB-020, SRB-019
**Practiced in:** `SRB-020-LAB1`, `SRB-019-LAB1`
**Show it:** the capstone's executive update with bad news; at work, a proposal or escalation you wrote for non-engineering leadership.

---

### Q13 · Two senior engineers strongly disagree on a design. What do you do?
**How often:** Common · **Round:** Behavioral

**How to answer (STAR):**
- Separate the people from the positions; make sure each side's argument is stated in a way the other accepts.
- Agree on the decision criteria (from requirements and quality attributes) before comparing options.
- Use evidence (a spike, data) where the disagreement is factual; decide and record it where it is a judgment call.
- Ensure both commit, and set a point to revisit if assumptions fail.

**Common trap:** deciding for them immediately, or letting the debate run for weeks.

**Learned in:** SRB-018, SRB-012
**Practiced in:** `SRB-018-LAB1`
**Show it:** the stock-ledger negotiation from the capstone gate; at work, a disagreement between senior engineers you helped resolve.

---

### Q14 · How do you manage risk in a long technical program?
**How often:** Common · **Round:** Hiring manager

**How to answer:**
- Identify technical, dependency, people, and schedule risks early with the teams.
- Keep a living register: likelihood, impact, owner, trigger, contingency.
- Buy information early (spikes, prototypes) for the biggest uncertainties.
- Review regularly and act when a trigger fires; give an example where a risk changed the plan.

**Learned in:** SRB-019, SRB-011
**Practiced in:** `SRB-019-LAB1`
**Show it:** the risk the assessor triggered in your capstone and your response; at work, a risk you identified early and the action it led to.

---

## 6. Six-week preparation plan

| Week | Focus | Do this |
| --- | --- | --- |
| 1 | Event-driven and data architecture | Q1–Q3 on a whiteboard; reread your event catalog and EU topology |
| 2 | Migration and integration | Q4–Q5; present your migration plan to a peer in 15 minutes |
| 3 | Operations at scale and security | Q6–Q7; redo `SRB-006-LAB1` reasoning without notes |
| 4 | Program leadership | Q8–Q11 as one-page stories from real work, backed by the capstone |
| 5 | Leadership behavior | Q12–Q14 in STAR form; rehearse the bad-news conversation with a peer |
| 6 | Mocks | Two full mock loops (architecture + initiative deep dive + behavioral) using the Senior B interview simulation |

**Ready when:** you can design a migration from an unseen legacy system with a credible, reversible path in 45 minutes; explain one real cross-team initiative end to end with outcomes; and answer every leadership question with a specific story, not a principle.
