# MID-003 · Java concurrency — Exercises and lab

## Lab
### MID-003-LAB1 · Parallel import
**Outcomes:** 1–4 · **Time:** ~4 h
Import product prices from several simulated suppliers (varying latency, one failing, one timing out) concurrently with a bounded pool, per-task timeouts, and a failure report. Shut the pool down correctly. Compare wall-clock time with the sequential version.
**Acceptance:** wall-clock improvement measured; no lost tasks (imported + failed + timed out equals submitted).

## Exercises (assessment: pool-sizing scenarios plus the lab)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-003-EX01 | 1 | Print a thread's state at NEW, after `start`, while in `sleep`, while blocked on a monitor, and after finish. |
| MID-003-EX02 | 2 | Submit three `Callable<Integer>` tasks, one throwing; collect results and show how the exception appears. |
| MID-003-EX03 | 3 | Size a pool for 8 cores: (a) image resizing, (b) supplier HTTP calls waiting 400 ms with 100 ms compute. |
| MID-003-EX04 | 3 | Predict how many threads run for core 4, max 16, `LinkedBlockingQueue` unbounded and 100 tasks; then for `ArrayBlockingQueue(10)`. |
| MID-003-EX05 | 4 | Write a shutdown helper using `shutdown`, `awaitTermination`, `shutdownNow`. |
| MID-003-EX06 | 4 | Make a pool reject work visibly when full and count rejections. |

## Solutions
- **EX01** `getState()`: NEW, RUNNABLE, TIMED_WAITING, BLOCKED, TERMINATED.
- **EX02** `Future.get()` throws `ExecutionException`; `getCause()` is the task's exception; the other results still arrive.
- **EX03** (a) about 8 threads. (b) cores x (1 + 400/100) = 8 x 5 = 40 threads as a starting point; then measure.
- **EX04** Unbounded queue: 4 threads, 96 queued. Bounded queue of 10: 4 core threads + 10 queued, then up to 12 extra threads (max 16) for the next 12 tasks, remaining tasks rejected: 100 - 26 = 74 rejected under the default abort policy if all submitted at once.
- **EX05** `pool.shutdown(); if (!pool.awaitTermination(t, SECONDS)) pool.shutdownNow();` with interrupt handling around the wait.
- **EX06** `ThreadPoolExecutor` with a bounded queue and a custom `RejectedExecutionHandler` that increments an `AtomicInteger` and throws or runs on the caller.
- Outcome 1's coordination is also in the lab; the L02 `join`/interrupt points are checked in Q02 and Q03.
