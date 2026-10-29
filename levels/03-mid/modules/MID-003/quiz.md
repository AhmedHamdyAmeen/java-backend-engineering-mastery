# MID-003 · Java concurrency — Quiz

Outcomes: O1 threads and states · O2 executors and futures · O3 pool sizing · O4 shutdown and failures.

**Q01 (O1)** To run code on a new thread you call: A. `run()` B. `start()` C. `join()` D. `wait()`
**Q02 (O1)** A thread waiting to enter a `synchronized` block is in state: A. WAITING B. TERMINATED C. NEW D. BLOCKED
**Q03 (O1)** `join()` on a thread: A. Waits until it finishes B. Kills it C. Starts it D. Interrupts it
**Q04 (O2)** `Callable` differs from `Runnable` by: A. Returning a value and allowing checked exceptions B. Being faster C. Needing no executor D. Running in the same thread
**Q05 (O2)** A task's exception reaches the caller of `Future.get()` as: A. The original type directly B. `ExecutionException` C. `TimeoutException` D. Nothing
**Q06 (O3)** A good starting size for a CPU-bound pool is about: A. 1000 threads B. Half the cores C. The number of cores D. 1
**Q07 (O3)** With an unbounded queue and core size 4, max 16, extra threads beyond 4 are: A. Created at once B. Created when memory runs low C. Created per task D. Never created
**Q08 (O3)** Which factory has an unbounded thread count? A. `newFixedThreadPool` B. `newCachedThreadPool` C. `newSingleThreadExecutor` D. `newWorkStealingPool(2)`
**Q09 (O4)** Correct shutdown order is: A. `shutdownNow` then `shutdown` B. `awaitTermination` only C. Never shut down D. `shutdown`, `awaitTermination`, then `shutdownNow` if needed
**Q10 (O4)** Which policy silently loses tasks? A. `AbortPolicy` B. `CallerRunsPolicy` C. `DiscardPolicy` D. None

## Answers
Q01 B · Q02 D · Q03 A · Q04 A · Q05 B · Q06 C · Q07 D · Q08 B · Q09 D · Q10 C

## Practical part
Six exercises `MID-003-EX01` to `EX06` (including two pool-sizing scenarios) plus the lab. Pass: at least five exercises correct and the lab showing a measured speed-up with no lost tasks.
