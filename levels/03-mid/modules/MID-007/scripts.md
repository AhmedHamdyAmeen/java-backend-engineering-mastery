# MID-007 · Virtual threads — Lecture scripts

**Video:** 58 min · **Analogy used throughout:** a restaurant with a few waiters (carrier threads) and thousands of tables (virtual threads): a waiter serves another table while one table waits for the kitchen, but the kitchen (database) still has limited capacity.
Format: **Goal** · **Key points** · **Show** · **Check**.

Version note: target the current LTS; verify version before recording for JDK-specific behavior (pinning, structured concurrency status).

---

## MID-007-L01 · The thread-per-request problem (8 min)
**Goal:** explain why blocking I/O wastes platform threads.

**Key points**
- Classic servers give each request one platform thread (an OS thread, about 1 MB of stack by default; verify).
- A thread waiting on a database or HTTP call does no work but still occupies the thread.
- Pool of 200 threads means about 200 concurrent requests; more queue up.
- Reactive code avoids this but is harder to write and debug.
- Wish: simple blocking code that scales.

**Show:** 200 threads, 190 waiting on a slow supplier endpoint; request 201 waits in line.

**Check:** Why does a waiting thread limit throughput? *(It holds a scarce OS thread while doing nothing.)*

---

## MID-007-L02 · Virtual threads explained (12 min)
**Goal:** describe how virtual threads work and when they help.

**Key points**
- A virtual thread is a lightweight thread managed by the JVM, mounted on a small pool of carrier (platform) threads.
- When it blocks on supported I/O, it unmounts and the carrier runs another virtual thread.
- Cheap to create: one per task; do not pool them.
- Create with `Thread.ofVirtual().start(r)` or `Executors.newVirtualThreadPerTaskExecutor()`.
- They help blocking I/O workloads; they do not make CPU work faster.

**Show**
```java
try (var exec = Executors.newVirtualThreadPerTaskExecutor()) {
    suppliers.forEach(s -> exec.submit(() -> importPrices(s)));
}
```

**Check:** Should you pool virtual threads? *(No; create one per task.)*

---

## MID-007-L03 · Virtual threads in Spring Boot (8 min)
**Goal:** turn them on and measure.

**Key points**
- Requires a JDK with virtual threads and a Spring Boot version that supports them (verify version before recording).
- Enable with `spring.threads.virtual.enabled=true`; request handling and async executors then use virtual threads.
- Existing blocking code (JDBC, `RestClient`) stays as is.
- Measure with a load test before and after; do not assume.
- `ThreadLocal` still works but is costly with millions of threads; prefer explicit passing.

**Show**
```yaml
spring:
  threads:
    virtual:
      enabled: true
```

**Check:** What changes in your controller code? *(Nothing; the same blocking code runs on virtual threads.)*

---

## MID-007-L04 · Pinning and other pitfalls (10 min)
**Goal:** know when virtual threads do not help.

**Key points**
- Pinning: a virtual thread cannot unmount while blocked, holding its carrier. Causes include blocking inside `synchronized` on older JDKs and native frames; newer JDKs reduce `synchronized` pinning (verify version).
- Diagnose with JFR's virtual thread pinned event or `-Djdk.tracePinnedThreads` (verify flags).
- CPU-bound work gains nothing; carriers equal about the number of cores.
- Downstream limits: 10,000 virtual threads can hit a 10-connection database pool, so the bottleneck moves.
- Use semaphores or pool limits to protect downstream resources.

**Show:** a table: workload / benefit — blocking HTTP: high; JDBC with small pool: bounded by pool; CPU loop: none.

**Check:** Why can a database pool still be the bottleneck? *(Many virtual threads compete for the same fixed number of connections.)*

---

## MID-007-L05 · Structured concurrency (preview status) (8 min)
**Goal:** understand the idea and its status.

**Key points**
- Structured concurrency: subtasks live inside a scope, and the scope waits for them, so lifetimes are clear.
- A failure can cancel sibling tasks; no leaked threads.
- API: `StructuredTaskScope` with fork and join; its status has been preview and the API has changed (verify version before recording).
- Using preview APIs needs `--enable-preview`; avoid in production unless the team accepts the risk.
- Compare with `CompletableFuture` fan-out from MID-006.

**Show**
```java
// conceptual: fork product, stock; join; failure cancels the other
```

**Check:** Why is a preview API risky for production? *(It may change or be removed between releases.)*

---

## MID-007-L06 · Demo: platform vs virtual threads under load (12 min)
**Goal:** measure the effect on Shop's slow-supplier endpoint; prepares MID-007-LAB1.

**Steps**
1. Start Shop with 200 platform request threads; the endpoint calls a supplier with 500 ms latency and one DB query.
2. Run a load test with 1,000 concurrent clients; record throughput, p95 latency, and pool metrics.
3. Enable virtual threads, restart, and repeat.
4. Observe higher throughput, then database pool saturation (connections pending).
5. **Planned mistake:** also raise the DB pool to 1,000 "to fix it" and hit database limits. Fix: keep a sized pool or a `Semaphore` guard; accept queueing in the right place.
6. Summarize: the bottleneck moved from threads to the database.
