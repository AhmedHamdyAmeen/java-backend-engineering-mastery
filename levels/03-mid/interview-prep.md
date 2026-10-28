# Level 3 — Mid-Level Backend Engineer: Interview Preparation

The questions most often asked in mid-level Java backend interviews, how to answer them, and exactly where in this course you learned and practiced each one.

**How to use this guide**
1. Answer each question **out loud** before reading the answer. At this level, interviewers probe with "why?" and "what if it fails?" — practice the follow-ups too.
2. If you struggle, return to the module in **Learned in** and redo the lab in **Practiced in**.
3. Prepare the **Show it** line for every question. Mid-level interviews reward evidence from systems you ran: measurements, dashboards, incidents, trade-offs you made.

> **About "How often":** frequencies reflect commonly reported interview patterns for mid-level Java backend roles, not measured statistics. Check them against current job posts in your target market (the method from `BEG-004-LAB1`) and update this guide when the market moves.

---

## 1. What the market asks for — and where you proved it

| Skill employers list | Learned in | Proven by |
| --- | --- | --- |
| JVM internals, GC tuning, profiling | MID-001, MID-002, MID-008 | `MID-002-LAB1` leak hunt, `MID-008-LAB1` profiling investigation |
| Concurrency and multithreading | MID-003 … MID-007 | `MID-004-LAB1` stock counter, `MID-007-LAB1` virtual-thread load comparison |
| Advanced SQL and query performance | MID-011, MID-012, MID-013 | `MID-013-LAB1` slow query clinic |
| Transactions, isolation, locking | MID-014, MID-015, MID-016 | `MID-015-LAB1` last item in stock |
| Microservices and service boundaries | MID-059, MID-060, MID-061, MID-025 | `MID-025-LAB1` split Shop, `MID-061-LAB1` split ADR |
| Kafka / messaging | MID-026, MID-028, MID-029 | `MID-028-LAB1`, `MID-029-LAB1` reliable order events |
| Distributed transactions / sagas | MID-030, MID-031 | `MID-031-LAB1` order saga |
| Redis and caching | MID-037 … MID-040 | `MID-038-LAB1`, `MID-040-LAB1` flash sale |
| Resilience patterns | MID-033, MID-034 | `MID-033-LAB1` resilient checkout |
| Observability and SRE practices | MID-047, MID-048, MID-049, MID-050 | `MID-047-LAB1` traceable Shop, `MID-050-LAB1` game day |
| Docker, Kubernetes, cloud, Terraform | MID-056, MID-057, MID-058 | `MID-057-LAB1` Shop on Kubernetes, `MID-058-LAB1` |
| API security (OAuth 2.0 / OIDC) | MID-051, MID-052 | `MID-051-LAB1` zero implicit trust |
| System design | MID-023, MID-024, MID-059 … MID-061 | `MID-CAP` Distributed Order Processing Platform |

**Your portfolio at the end of Level 3:** the Distributed Order Processing Platform (`MID-CAP`) with C4 diagrams, ADRs, a load-test report, dashboards, and a postmortem. In interviews, the load-test report and the postmortem are often more persuasive than the code.

## 2. How mid-level interviews usually run

| Round | What happens | What they check | Prepare with |
| --- | --- | --- | --- |
| Recruiter / hiring-manager screen | 30 min | Scope of past ownership, motivation | Q22, your project pitch |
| Coding | 45–60 min, one or two medium problems or a practical exercise (e.g., implement a thread-safe component) | Correct, clean, tested code; concurrency awareness | Q3, Q4, Level 1 coding drills |
| Technical deep dive | Java, databases, messaging, Spring | Depth beyond "how to use it" | Q1–Q19 |
| System design | 45–60 min, design a system on a whiteboard | Structured thinking, trade-offs, failure handling | Q20, Q21 |
| Behavioral / ownership | Incidents, conflicts, decisions | Ownership, learning from failure | Q22 |

---

## 3. JVM and concurrency

### Q1 · How is JVM memory organized, and how does garbage collection work?
**How often:** Very common · **Round:** Technical deep dive

**How to answer:**
- **Heap** holds objects; **stacks** hold per-thread frames; **metaspace** holds class metadata; the **code cache** holds JIT-compiled code.
- Most collectors are **generational**: most objects die young, so new objects go to the young generation, which is collected often and cheaply; survivors are promoted to the old generation.
- Reachability starts from **GC roots** (thread stacks, static fields, JNI references); unreachable objects are reclaimed.
- Name the collectors and when to choose them: **G1** (default, balanced), **ZGC** (very low pauses, large heaps), **Parallel** (throughput for batch).
- In containers, size the heap relative to the container limit (`-XX:MaxRAMPercentage`) and leave room for non-heap memory.

**Common trap:** treating `-Xmx` increases as a fix. More heap delays a leak; it does not remove it.

**Learned in:** MID-001, MID-002
**Practiced in:** `MID-001-LAB1`, `MID-002-LAB1`
**Show it:** the GC log analysis from the leaky-cache lab, before and after the fix.

---

### Q2 · A service's memory keeps growing / CPU is at 100%. How do you diagnose it?
**How often:** Very common · **Round:** Technical deep dive

**How to answer:** a method, then tools.
1. **Confirm and scope:** which instances, since when, correlated with a deploy or traffic change? Check dashboards first.
2. **Memory growth:** check GC logs (does old-gen occupancy after full GC keep rising?). Take two heap dumps some time apart and compare dominators in a heap analyzer to find what retains the growing objects (typical: unbounded caches, static collections, listeners never removed).
3. **High CPU:** record with **JFR** and read the flame graph, or take several thread dumps a few seconds apart and look for the same hot frames. Also check whether the CPU is GC (allocation pressure) rather than application code.
4. **Fix, then prove:** re-measure under the same load.

**Common trap:** restarting first and losing the evidence. Capture dumps or a recording before mitigating if the situation allows.

**Learned in:** MID-002, MID-008
**Practiced in:** `MID-002-LAB1`, `MID-008-LAB1`
**Show it:** your investigation log from the profiling lab.

---

### Q3 · What do `volatile`, `synchronized`, and atomic classes guarantee? When do you use each?
**How often:** Very common · **Round:** Technical deep dive, coding

**How to answer:**
- **`volatile`:** visibility and ordering for a single variable — a write is seen by subsequent reads in other threads. It does **not** make compound actions (`count++`) atomic.
- **`synchronized`** (or `ReentrantLock`): mutual exclusion **and** visibility for a block; use when several variables must change together or for check-then-act.
- **Atomics** (`AtomicInteger`, `LongAdder`, `compareAndSet`): lock-free atomic updates of one variable; ideal for counters and flags.
- Best option when possible: **immutability** or **confinement** — no shared mutable state, no locking.

```java
private final AtomicInteger reserved = new AtomicInteger();
boolean reserve(int qty, int stock) {
    while (true) {
        int current = reserved.get();
        if (current + qty > stock) return false;
        if (reserved.compareAndSet(current, current + qty)) return true;
    }
}
```

**Common trap:** saying `volatile` "makes a variable thread-safe".

**Learned in:** MID-004, MID-005
**Practiced in:** `MID-004-LAB1`, `MID-005-LAB1`
**Show it:** the stress test that failed before your fix and passed after.

---

### Q4 · How do you size a thread pool, and what goes wrong with the wrong configuration?
**How often:** Common · **Round:** Technical deep dive

**How to answer:**
- **CPU-bound:** roughly the number of cores; more threads only add context switching.
- **I/O-bound:** more threads, estimated as `cores × (1 + wait time / compute time)` — then validated by load testing, because downstream limits (database pool, remote rate limits) usually decide the real maximum.
- Always use a **bounded queue** and an explicit **rejection policy**; unbounded queues hide overload until memory runs out.
- Shut executors down; handle exceptions from tasks (they are captured in the `Future`).

**Common trap:** `Executors.newCachedThreadPool()` under load — unbounded threads.

**Learned in:** MID-003, MID-017
**Practiced in:** `MID-003-LAB1`
**Show it:** the pool that silently dropped work and how you made rejections visible.

---

### Q5 · How do you call three services in parallel with an overall timeout using `CompletableFuture`?
**How often:** Common · **Round:** Coding, technical deep dive

**How to answer:**

```java
var product = CompletableFuture.supplyAsync(() -> catalog.get(id), ioExecutor);
var stock   = CompletableFuture.supplyAsync(() -> inventory.get(id), ioExecutor)
                               .completeOnTimeout(Stock.unknown(), 300, MILLISECONDS);
var reviews = CompletableFuture.supplyAsync(() -> reviewsClient.get(id), ioExecutor)
                               .exceptionally(e -> Reviews.empty());

ProductPage page = product.thenCombine(stock, ProductPage::new)
                          .thenCombine(reviews, ProductPage::withReviews)
                          .orTimeout(800, MILLISECONDS)
                          .join();
```

- Use a dedicated executor for blocking I/O, not the common pool.
- Decide per call: required (fail the whole request) or optional (degrade with a default).
- Explain that total latency ≈ the slowest call, not the sum.

**Learned in:** MID-006
**Practiced in:** `MID-006-LAB1`

---

### Q6 · What are virtual threads, and when do they help or not?
**How often:** Common, and growing · **Round:** Technical deep dive

**How to answer:**
- Virtual threads are lightweight threads scheduled by the JVM onto a small pool of carrier threads. When one blocks on I/O, it unmounts and the carrier runs another.
- They make the **thread-per-request** style scale for **I/O-bound** work without reactive code.
- They do **not** speed up CPU-bound work, and they do not remove downstream limits: a database pool of 20 connections still allows 20 concurrent queries — so keep limits (pools, semaphores).
- Watch for **pinning** (blocking while holding a monitor in some cases, or in native calls) and do not pool virtual threads.

**Learned in:** MID-007
**Practiced in:** `MID-007-LAB1`
**Show it:** your platform-vs-virtual load comparison, including the new bottleneck it revealed.

---

## 4. Databases

### Q7 · A query is slow. How do you find out why and fix it?
**How often:** Very common · **Round:** Technical deep dive

**How to answer:**
1. Find the slow statements with `pg_stat_statements` (total time, not just the slowest single call).
2. Run `EXPLAIN (ANALYZE, BUFFERS)` and read it bottom-up: scan types, join algorithms, **estimated vs actual rows**, buffers read.
3. Typical causes and fixes: missing or wrong-order composite index; a function on an indexed column; stale statistics (`ANALYZE`); deep `OFFSET` pagination (switch to keyset pagination); N+1 queries from the ORM.
4. Re-run the plan and measure under realistic data volume.

```sql
EXPLAIN (ANALYZE, BUFFERS)
SELECT * FROM orders WHERE customer_id = $1 ORDER BY created_at DESC LIMIT 20;
-- Fix: CREATE INDEX CONCURRENTLY ON orders (customer_id, created_at DESC);
```

**Common trap:** running `EXPLAIN` on a tiny development database where every plan looks fast.

**Learned in:** MID-012, MID-013
**Practiced in:** `MID-013-LAB1`
**Show it:** a before/after plan and timing from the slow query clinic.

---

### Q8 · How does a B-tree index work, and when does an index not help?
**How often:** Very common · **Round:** Technical deep dive

**How to answer:**
- A B-tree keeps keys sorted in a balanced tree, giving O(log n) lookups and ordered range scans.
- **Composite indexes** follow the leftmost-prefix rule: `(customer_id, created_at)` helps filters on `customer_id` alone or both, not on `created_at` alone.
- An index does not help when the predicate matches a large fraction of rows (a sequential scan is cheaper), when a function wraps the column, or for leading-wildcard `LIKE '%x'`.
- Indexes cost writes and storage; partial and covering indexes reduce both.
- Name alternatives: GIN for `jsonb`/full-text, BRIN for huge append-only time series.

**Learned in:** MID-012
**Practiced in:** `MID-012-LAB1`

---

### Q9 · Explain transaction isolation levels. How do you prevent a lost update?
**How often:** Very common · **Round:** Technical deep dive

**How to answer:**
- Anomalies: dirty read, non-repeatable read, phantom read, **lost update**, write skew.
- PostgreSQL: **Read Committed** (default) prevents dirty reads; **Repeatable Read** gives a stable snapshot and detects some concurrent updates; **Serializable** prevents all anomalies by aborting conflicting transactions, which the application must **retry**.
- Lost update example: two requests read stock = 1 and both sell it. Fixes:
  - an atomic conditional update: `UPDATE stock SET qty = qty - 1 WHERE product_id = $1 AND qty >= 1` and check the row count;
  - `SELECT … FOR UPDATE` (pessimistic);
  - a version column (optimistic, see Q10).

**Common trap:** assuming `@Transactional` alone prevents lost updates. At Read Committed it does not.

**Learned in:** MID-014, MID-015
**Practiced in:** `MID-015-LAB1`
**Show it:** the concurrent test that never oversells.

---

### Q10 · Optimistic vs pessimistic locking — how do you choose?
**How often:** Common · **Round:** Technical deep dive

**How to answer:**
- **Optimistic** (`@Version`): no lock while reading; the update fails if the version changed. Best when conflicts are rare and requests are user-paced (editing a product). Surface conflicts as **409**.
- **Pessimistic** (`SELECT … FOR UPDATE`): lock the row for the transaction. Best when conflicts are frequent and short (decrementing hot stock), but it reduces concurrency and risks deadlocks.
- Either way, keep transactions short and retry only idempotent work.

**Learned in:** MID-016
**Practiced in:** `MID-016-LAB1`

---

### Q11 · Requests start timing out with "connection is not available". What is happening?
**How often:** Common · **Round:** Technical deep dive, troubleshooting

**How to answer:**
- The **connection pool is exhausted**: all connections are borrowed and new requests wait until the pool timeout.
- Usual causes: slow queries holding connections longer; long transactions (especially with remote calls inside them); connection leaks; a traffic spike; `REQUIRES_NEW` taking a second connection per request.
- Diagnose with pool metrics (active, pending, wait time), thread dumps (threads waiting in the pool), and database activity (`pg_stat_activity`).
- Fix the cause; do not just enlarge the pool — a pool larger than the database can serve makes latency worse. Size from database capacity and Little's Law.

**Learned in:** MID-017, MID-016
**Practiced in:** `MID-017-LAB1`
**Show it:** your pool-size load-test chart (5 / 10 / 50 / 200).

---

## 5. Distributed systems and messaging

### Q12 · How does Kafka guarantee ordering, and how do consumer groups work?
**How often:** Very common · **Round:** Technical deep dive

**How to answer:**
- A topic is split into **partitions**; ordering is guaranteed **within a partition only**.
- Messages with the same **key** go to the same partition, so key by the entity whose order matters (e.g., order ID).
- In a **consumer group**, each partition is assigned to exactly one consumer; parallelism is capped by the number of partitions.
- Consumers commit **offsets**; commit after processing to avoid losing messages. A **rebalance** reassigns partitions when consumers join or leave.
- Producer durability: `acks=all` and the idempotent producer.

**Common trap:** expecting global ordering across a topic, or using random keys for entity events.

**Learned in:** MID-026, MID-028
**Practiced in:** `MID-028-LAB1`

---

### Q13 · What do at-least-once and exactly-once mean? How do you make a consumer idempotent?
**How often:** Very common · **Round:** Technical deep dive

**How to answer:**
- **At-most-once** may lose messages; **at-least-once** may deliver duplicates; end-to-end **exactly-once delivery** is not achievable across arbitrary systems — what you design for is **exactly-once effects**.
- Idempotent consumer options:
  - record processed message IDs in an **inbox** table in the same transaction as the business change, and skip duplicates;
  - make the operation naturally idempotent (upsert, "set status to PAID" rather than "add payment").
- Route messages that keep failing to a **dead-letter queue/topic** after bounded retries.

```sql
INSERT INTO processed_message (message_id) VALUES ($1) ON CONFLICT DO NOTHING;
-- 0 rows inserted → duplicate → skip business logic (same transaction)
```

**Learned in:** MID-026, MID-029
**Practiced in:** `MID-029-LAB1`
**Show it:** the chaos script that kills services mid-flow without duplicates.

---

### Q14 · What is the dual-write problem, and how does the transactional outbox solve it?
**How often:** Very common · **Round:** Technical deep dive, system design

**How to answer:**
- **Problem:** saving to the database and publishing to Kafka are two separate systems; a crash between them loses the event or publishes an event for a rolled-back change.
- **Outbox:** in the same database transaction, write the business change **and** an event row to an `outbox` table. A relay (polling or CDC such as Debezium) publishes outbox rows to the broker and marks them sent.
- The relay can publish twice after a crash, so consumers must be idempotent (Q13).

**Common trap:** "publish inside the transaction" — the broker does not roll back with the database.

**Learned in:** MID-029
**Practiced in:** `MID-029-LAB1`

---

### Q15 · How do you implement a business transaction across several services? Explain sagas.
**How often:** Very common · **Round:** Technical deep dive, system design

**How to answer:**
- Distributed two-phase commit couples services and is rarely available or desirable; use a **saga**: a sequence of local transactions, each with a **compensating action**.
- **Choreography:** services react to each other's events — simple for short flows, hard to follow as it grows.
- **Orchestration:** an orchestrator tells each service what to do and tracks saga state — clearer for complex flows with timeouts.
- Example: place order → reserve stock → authorize payment → confirm. If payment is declined: release stock, cancel order.
- Compensations must be idempotent and semantically correct (a refund, not a delete); handle timeouts and stuck sagas.

**Learned in:** MID-031
**Practiced in:** `MID-031-LAB1`, `MID-CAP`
**Show it:** the saga's sequence diagram and its failure-path tests.

---

### Q16 · Explain the CAP theorem. Is your system CP or AP?
**How often:** Common · **Round:** Technical deep dive, system design

**How to answer:**
- CAP: during a **network partition**, a distributed system must choose between **consistency** (every read sees the latest write or errors) and **availability** (every request gets a response).
- It says nothing about normal operation; **PACELC** adds that, without partitions, you trade **latency vs consistency**.
- Real systems choose **per operation**: payments and stock reservation need strong consistency; product listings and reviews can be eventually consistent.
- Explain how the UI handles eventual consistency ("order pending").

**Common trap:** labeling a whole system "AP" or claiming to have all three.

**Learned in:** MID-023, MID-030
**Practiced in:** `MID-030-LAB1`

---

### Q17 · Which caching strategy would you use, and how do you keep the cache consistent?
**How often:** Very common · **Round:** Technical deep dive, system design

**How to answer:**
- **Cache-aside** (most common): read from cache; on miss, load from the database and populate with a TTL. On write, update the database then **delete** the cache entry.
- **Write-through / write-behind:** cache updated on write; write-behind risks losing data.
- Consistency tools: event-driven invalidation (`ProductUpdated`), TTL as a safety net, versioned values against invalidation races, and an explicit **staleness budget** per data type.
- Protect the database from **stampedes** (request coalescing, locking, early refresh, jittered TTLs) and **hot keys**.

**Common trap:** caching prices or stock with a long TTL and no invalidation.

**Learned in:** MID-037, MID-039, MID-040
**Practiced in:** `MID-039-LAB1`, `MID-040-LAB1`
**Show it:** hit ratio and latency numbers from your catalog cache.

---

### Q18 · How do you stop one slow dependency from taking down your service?
**How often:** Very common · **Round:** Technical deep dive, system design

**How to answer:**
- **Timeouts** on every remote call, derived from a latency budget.
- **Retries** only for transient failures and idempotent operations, with exponential backoff and **jitter**, and a retry budget.
- **Circuit breaker:** stop calling a failing dependency for a while, fail fast, probe for recovery.
- **Bulkheads:** separate thread pools or semaphores per dependency so one cannot exhaust all resources.
- **Fallbacks / degradation:** serve partial results honestly (e.g., product page without reviews).
- Add rate limiting at the edge to shed abusive or excess load.

**Common trap:** retries without timeouts, creating retry storms that keep the dependency down.

**Learned in:** MID-033, MID-034
**Practiced in:** `MID-033-LAB1`, `MID-034-LAB1`
**Show it:** the Toxiproxy experiment showing a contained failure.

---

## 6. Production engineering and architecture

### Q19 · How do you monitor a microservice system? What are SLOs?
**How often:** Very common · **Round:** Technical deep dive

**How to answer:**
- **Metrics** (rates, errors, latency percentiles — RED/USE) for dashboards and alerts; **logs** for detail; **traces** for following one request across services. Correlate logs with trace IDs and propagate context through HTTP **and** Kafka (OpenTelemetry).
- **SLI:** a measure of user experience (e.g., % of checkouts under 500 ms that succeed). **SLO:** the target (99.9% over 30 days). **Error budget:** the allowed failure (0.1%).
- Alert on **symptoms** and **burn rate**, not on CPU; every alert links to a runbook.
- Kubernetes: **readiness** probes control traffic, **liveness** probes restart stuck containers — liveness must not check the database.

**Learned in:** MID-047, MID-048, MID-049, MID-057
**Practiced in:** `MID-047-LAB1`, `MID-049-LAB1`, `MID-057-LAB1`
**Show it:** trace an order across four services live from your dashboards.

---

### Q20 · System design: design an order processing system for an online shop.
**How often:** Very common · **Round:** System design

**How to answer — use the same framework for every design question:**
1. **Clarify requirements (5 min):** functional (place, pay, cancel, track orders) and nonfunctional (peak orders/s, latency target, availability, consistency for stock and payment).
2. **Estimate (3 min):** e.g., 200 orders/s at peak → events/s, storage per year, read/write ratio.
3. **High-level design (10 min):** API gateway → `orders`, `inventory`, `payments` services, each with its own database; Kafka for events; Redis for catalog reads.
4. **Core flow (10 min):** checkout as an orchestrated **saga** (reserve stock → authorize payment → confirm), events published via **outbox**, **idempotent** consumers, idempotency key on the checkout API.
5. **Data and consistency (5 min):** strong consistency for stock reservation (atomic update / row lock); eventual consistency for search and order history views.
6. **Failure handling (5 min):** timeouts, retries with backoff, circuit breakers, DLQs, saga timeouts and compensations, payment provider reconciliation.
7. **Scale and operate (5 min):** partition Kafka by order ID, scale consumers, cache the catalog, observability and SLOs, what you would monitor first.
8. **Trade-offs:** say what you would *not* split into services at first, and why.

**Common trap:** jumping to boxes before requirements; ignoring failure paths.

**Learned in:** MID-025, MID-029, MID-031, MID-033, MID-061
**Practiced in:** `MID-031-LAB1`, `MID-CAP`
**Show it:** your capstone's C4 diagrams — this question is your capstone.

---

### Q21 · System design: design a rate limiter for a public API.
**How often:** Common · **Round:** System design

**How to answer (same framework):**
1. **Requirements:** limits per API key and per IP, e.g., 100 requests/min; correct `429` with `Retry-After`; low added latency; works across many gateway instances.
2. **Algorithm:** **token bucket** (allows bursts up to bucket size, refills at a fixed rate) — explain why over fixed windows (boundary bursts) and sliding logs (memory cost).
3. **Where:** at the API gateway, before business services.
4. **State:** shared counters in **Redis**, updated atomically (a Lua script or atomic increment with expiry) so all instances agree.
5. **Failure mode:** if Redis is down, fail open (allow) or fail closed (deny)? Decide per endpoint and say why.
6. **Scale:** shard keys across Redis nodes; local pre-limiting to reduce Redis calls for hot keys.
7. **Observability:** metrics on throttled requests per client; alert on sudden spikes.

**Learned in:** MID-034, MID-035, MID-038
**Practiced in:** `MID-034-LAB1`, `MID-035-LAB1`

---

### Q22 · Tell me about a production incident you handled.
**How often:** Very common · **Round:** Behavioral / ownership

**How to answer — structured, blameless, measurable:**
1. **Context:** the system and the impact in user terms (e.g., 8% of checkouts failing for 25 minutes).
2. **Detection:** how you found out (alert, customer report) — and whether detection was fast enough.
3. **Mitigation first:** what you did to stop the bleeding (rollback, feature flag, scaling) before root-causing.
4. **Root cause:** found with evidence (traces, dumps, logs), including contributing factors.
5. **Follow-up:** the postmortem actions you owned and what changed (an alert, a test, a design change).
6. **Lesson:** what you do differently now.

If you lack real production experience, use the game-day incident from this course and say so honestly.

**Common trap:** blaming a person; describing heroics instead of process.

**Learned in:** MID-050, MID-065
**Practiced in:** `MID-050-LAB1`
**Show it:** your written postmortem.

---

## 7. Four-week preparation plan

| Week | Focus | Do this |
| --- | --- | --- |
| 1 | JVM, concurrency | Answer Q1–Q6 aloud; implement a thread-safe bounded cache and a parallel aggregator from scratch; re-read your profiling investigation log |
| 2 | Databases | Q7–Q11; redo `MID-013-LAB1` and `MID-015-LAB1` timed; read three real `EXPLAIN ANALYZE` plans out loud |
| 3 | Distributed systems | Q12–Q19; draw your capstone's architecture from memory in 10 minutes; explain the outbox and saga end to end |
| 4 | System design and behavior | Two timed design mocks (Q20, Q21 and one new prompt) with a peer; rehearse Q22 with your postmortem; full Level 3 interview simulation |

**Ready when:** you can design an unseen system in 45 minutes using the framework while discussing failure modes, explain every technology in your capstone down to its trade-offs, and tell one incident story with numbers and lessons.
