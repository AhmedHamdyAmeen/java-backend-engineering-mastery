# SRC-015 · Advanced troubleshooting — Lecture scripts

**Video:** 91 min · **Running case:** *Order Processing at 10×* — Shop Platform's order subsystem must handle a 10× growth forecast, a 99.95% availability commitment, and a 15-minute recovery objective.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRC-015-L01 · Troubleshooting as hypothesis testing (10 min)
**Goal:** investigate systematically instead of guessing.

**Key points**
- Loop: observe the symptoms, form hypotheses, pick the cheapest test that separates them, run it, update.
- Write hypotheses and evidence down; it keeps a team aligned and prevents re-testing.
- Stop mitigation and diagnosis from blocking each other: restore service first when safe, but capture evidence (thread dumps, heap, logs) before restarting.
- Beware anchoring: the first plausible cause is often a symptom of a deeper one.

**Show** An investigation log: time | observation | hypothesis | test | result | next. Keep it in the incident channel.

**Check:** Why capture evidence before restarting? *(A restart destroys the state needed to find the cause.)*

---

## SRC-015-L02 · Thread starvation (10 min)
**Goal:** recognize and diagnose exhausted thread pools.

**Key points**
- Symptom: latency climbs while CPU stays low; requests queue.
- Causes: blocking calls on a small pool, a slow dependency holding threads, a pool used for both work and waiting (pool deadlock).
- Evidence: take thread dumps a few seconds apart; many threads waiting in the same call point to the culprit; check pool queue depth and active counts metrics.
- Fixes: timeouts, bulkheads (separate pools per dependency), bounded queues with load shedding, virtual threads for blocking I/O where suitable (verify version support and pinning issues).

**Show** Thread dump excerpt: 200 `http-nio-exec` threads in `WAITING` inside a payment client `read()`. Interpretation: dependency slowness plus no timeout.

**Check:** CPU is low yet requests are slow. What do you suspect? *(Threads blocked waiting, such as pool exhaustion from a slow dependency.)*

---

## SRC-015-L03 · Connection exhaustion (10 min)
**Goal:** diagnose exhausted connection pools and database connection limits.

**Key points**
- Symptom: threads waiting for a connection; timeouts "unable to acquire connection".
- Causes: slow queries holding connections, leaked connections, transactions open across remote calls, a pool larger than the database can serve across all instances.
- Evidence: pool metrics (active, idle, pending), database session list showing idle-in-transaction, long-running queries.
- Fixes: shorter transactions, no remote calls inside transactions, correct pool sizing per instance times replicas, timeouts, leak detection.

**Show** Arithmetic: 40 pods times a pool of 20 equals 800 connections against a database limit of 500. At 10× scale this becomes a failure.

**Check:** Why avoid remote calls inside a transaction? *(They hold a connection while waiting on something slow.)*

---

## SRC-015-L04 · Distributed deadlocks and lock convoys (10 min)
**Goal:** recognize deadlocks and convoys within and across services.

**Key points**
- Database deadlock: two transactions hold locks and wait for each other; the database aborts one. Fix with consistent lock ordering and shorter transactions.
- Distributed deadlock: A waits on B while B waits on A through synchronous calls and limited pools.
- Lock convoy: many requests queue on one hot row or lock, so throughput collapses to one at a time.
- Evidence: lock wait views, deadlock logs, thread dumps showing the lock owner; hot-row metrics.

**Show** Two orders updating the same two stock rows in opposite order; fix by sorting item IDs before locking. For a hot row, consider sharding counters or optimistic updates.

**Check:** What is the standard fix for a lock-order deadlock? *(Acquire locks in a consistent global order.)*

---

## SRC-015-L05 · Cascading and metastable failures (14 min)
**Goal:** recognize failure patterns that sustain themselves and break them.

**Key points**
- Cascading failure: overload in one component pushes load to others (failover traffic, retries) until many fail.
- Metastable failure: a trigger (a short slowdown) leaves the system in a bad state sustained by its own reaction, such as retries or queue backlog, even after the trigger is gone.
- Retry storm: clients retry failing calls, multiplying load; layered retries multiply (3 × 3 × 3 = 27 calls).
- Breaking the loop: shed load, disable or limit retries, circuit breakers, backoff with jitter, drain queues or reduce inflow, then restore capacity gradually.
- Prevent: retry budgets, timeouts that shrink down the call chain, admission control.

**Show** Diagram description: slow database leads to timeouts, which cause retries, which increase load, which slows the database further; a loop with the trigger removed but the loop still running.

**Check:** What makes a failure metastable? *(The system's own reaction, such as retries or backlog, keeps it failing after the trigger ends.)*

---

## SRC-015-L06 · Cross-layer investigations (10 min)
**Goal:** follow a symptom through JVM, database, network, and Kubernetes layers.

**Key points**
- Walk layers deliberately: application, JVM (GC, threads), OS and container limits, network, database, dependencies.
- Use correlating signals: same timestamps across layers; compare healthy and unhealthy instances.
- Typical cross-layer causes: GC pauses from a too-small memory limit, CPU throttling, DNS delays, packet loss, noisy neighbors, query plan change.
- Keep a layer map and note which evidence ruled out each layer.

**Show** Table: layer | tool | signal | verdict. Example rows: JVM | GC logs | pause length; container | cgroup throttling metrics | throttled periods; network | latency percentiles per hop.

**Check:** How do you use a healthy instance in an investigation? *(Compare it with the unhealthy one to isolate the difference.)*

---

## SRC-015-L07 · Demo: a retry storm that won't stop by itself (15 min)
**Goal:** diagnose and break a metastable retry storm; prepares SRC-015-LAB1.

**Steps**
1. Start from the symptoms: orders failing and database CPU high, although the original slowdown ended 20 minutes ago.
2. Form hypotheses (the database is still slow, a deploy broke it, a retry loop sustains load) and test each with request-rate and attempt metrics.
3. Find retries at three layers multiplying traffic about 27 times.
4. **Planned mistake:** restart the order service, and the storm resumes within a minute. Fix: shed load at the edge and disable layered retries first, then restore gradually.
5. Break the loop: enable load shedding, reduce retries to the outer layer only, ramp traffic back.
6. Write the follow-ups: retry budgets, jitter, shrinking timeouts, admission control.

**Check:** Why did the restart not help? *(Clients' retries immediately recreated the overload.)*

---

## SRC-015-L08 · Demo: latency caused by Kubernetes CPU throttling (12 min)
**Goal:** find a cross-layer cause where the app looks fine but the container is throttled; prepares SRC-015-LAB1.

**Steps**
1. Symptom: p99 spikes in bursts while average CPU looks low.
2. Rule out the database and GC from their metrics.
3. Check container metrics for CPU throttling (cgroup throttled periods); correlate with latency spikes.
4. **Planned mistake:** raise the JVM heap. Fix: the evidence points at CPU limits, so adjust the limit or request, and review JVM thread and GC thread counts relative to the container CPU; verify JVM container awareness for your version.
5. Re-test and confirm the spikes disappear.

**Check:** Why can average CPU look low while throttling harms latency? *(Throttling occurs in short bursts when the quota is used up within a period.)*
