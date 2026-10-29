# MID-003 · Java concurrency — Lecture scripts

**Video:** 76 min · **Analogy used throughout:** a checkout hall: cashiers are threads, the line is the queue, and the store manager decides how many cashiers to hire.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-003-L01 · Why concurrency: throughput and latency (8 min)
**Goal:** state what concurrency buys and what it costs.

**Key points**
- Throughput: work finished per second. Latency: time for one piece of work.
- Waiting on I/O (database, HTTP) wastes a thread unless other work runs meanwhile.
- Concurrency means tasks in progress together; parallelism means running at the same instant on several cores.
- Costs: complexity, shared-state bugs, context switches, memory per thread.
- Amdahl's law: the serial part limits speed-up.

**Show:** timeline: three 200 ms supplier calls sequentially (600 ms) vs concurrently (about 200 ms).

**Check:** Which concurrent work gains most: CPU-bound or I/O-bound? *(I/O-bound, as waits overlap; CPU-bound is limited by cores.)*

---

## MID-003-L02 · Threads and their lifecycle (10 min)
**Goal:** create threads and read their states.

**Key points**
- `Thread` runs a `Runnable`; call `start()`, never `run()` directly.
- States: NEW, RUNNABLE, BLOCKED (waiting for a monitor), WAITING and TIMED_WAITING (`wait`, `join`, `sleep`), TERMINATED.
- `join()` waits for a thread to finish; `interrupt()` requests it to stop, and blocking calls throw `InterruptedException`.
- Handle interruption: restore the flag or exit; never swallow it.
- Raw threads are rarely created in services; executors manage them.

**Show**
```java
Thread t = new Thread(() -> importPrices("acme"));
t.start();
t.join();
```

**Check:** What does calling `run()` instead of `start()` do? *(Runs on the calling thread; no new thread.)*

---

## MID-003-L03 · Executors and futures (12 min)
**Goal:** submit tasks and collect results.

**Key points**
- `ExecutorService` separates submitting a task from how it runs.
- `Runnable` returns nothing; `Callable<V>` returns a value and may throw.
- `submit` returns a `Future<V>`; `get()` blocks, optionally with a timeout.
- `ExecutionException` wraps the task's exception; the cause is inside.
- `invokeAll` runs a batch and returns when all finish.

**Show**
```java
ExecutorService pool = Executors.newFixedThreadPool(4);
Future<BigDecimal> f = pool.submit(() -> supplier.fetchPrice(sku));
BigDecimal price = f.get(2, TimeUnit.SECONDS);
```

**Check:** Where does a task's exception surface? *(In `Future.get()`, wrapped in `ExecutionException`.)*

---

## MID-003-L04 · Thread pools: size, queue, rejection (14 min)
**Goal:** size a pool and predict its queueing behavior.

**Key points**
- `ThreadPoolExecutor`: core size, max size, queue, rejection policy.
- Order of growth: use core threads, then enqueue, and only add threads up to max when the queue is full. An unbounded queue means max is never used.
- CPU-bound: about the number of cores. I/O-bound: more, roughly cores x (1 + wait/compute); measure.
- Use a bounded queue plus an explicit rejection policy (e.g., caller-runs, or abort and report) to create backpressure.
- `newCachedThreadPool` has unbounded threads; `newFixedThreadPool` has an unbounded queue. Both can hurt under load.

**Show**
```java
new ThreadPoolExecutor(8, 8, 0, TimeUnit.SECONDS,
    new ArrayBlockingQueue<>(100), new ThreadPoolExecutor.CallerRunsPolicy());
```

**Check:** With core 8, max 32, and an unbounded queue, how many threads run? *(8; the queue never fills.)*

---

## MID-003-L05 · Shutdown and failure handling (8 min)
**Goal:** stop pools cleanly and not lose failures.

**Key points**
- `shutdown()` stops accepting tasks and lets queued ones finish; `shutdownNow()` interrupts workers.
- Pattern: `shutdown()`, `awaitTermination(timeout)`, then `shutdownNow()`.
- Non-daemon pool threads keep the JVM alive if you never shut down.
- Tasks given to `execute` that throw print to the thread's uncaught handler; with `submit` the exception hides inside the `Future` until `get()`.
- Always log or collect failures.

**Show**
```java
pool.shutdown();
if (!pool.awaitTermination(30, TimeUnit.SECONDS)) pool.shutdownNow();
```

**Check:** Why can a failed `submit` task go unnoticed? *(The exception is stored in the `Future`; nobody called `get()`.)*

---

## MID-003-L06 · Demo: parallelizing the price-feed import (12 min)
**Goal:** speed up the supplier price import; prepares MID-003-LAB1.

**Steps**
1. Show the sequential import of five suppliers (each about 300 ms): about 1.5 s.
2. Wrap each import in a `Callable`; submit to a fixed pool of 5.
3. Collect with `Future.get(timeout)`; gather successes and failures into a report.
4. Measure again: wall clock near the slowest supplier.
5. **Planned mistake:** forget `shutdown()` and watch the app not exit. Fix: `shutdown` plus `awaitTermination` in `finally` (or try-with-resources on newer JDKs; verify version before recording).
6. Print the report: imported, failed, timed out.

---

## MID-003-L07 · Demo: a thread pool that silently drops work (12 min)
**Goal:** find lost tasks caused by a rejection policy and swallowed errors.

**Steps**
1. Start a pool with 2 threads, a queue of 2, and `DiscardPolicy`.
2. Submit 10 slow tasks; count completions: only 4 finish, with no error.
3. Switch to `AbortPolicy`; catch `RejectedExecutionException` and see the rejected count.
4. **Planned mistake:** use `submit` with a task that throws and never call `get()`; the failure vanishes. Fix: wrap the task body in try/catch with logging, or inspect the futures.
5. Decide a policy: caller-runs for backpressure or abort plus metric; never silent discard for business work.
