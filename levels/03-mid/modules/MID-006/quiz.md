# MID-006 · Async programming — Quiz

Outcomes: O1 composing stages · O2 errors · O3 timeouts and cancellation · O4 executors.

**Q01 (O1)** For a dependent async call (B needs A's result) use: A. `thenApply` B. `thenCombine` C. `thenCompose` D. `allOf`
**Q02 (O1)** For two independent futures joined into one value use: A. `thenCombine` B. `thenCompose` C. `thenRun` D. `cancel`
**Q03 (O1)** `CompletableFuture.allOf(...)` returns: A. A list of results B. `CompletableFuture<Void>` C. The first result D. A boolean
**Q04 (O2)** To recover from a failure with a default: A. `thenApply` B. `thenAccept` C. `get` D. `exceptionally`
**Q05 (O2)** If a stage fails, a later `thenApply` stage is: A. Run with null B. Run normally C. Skipped, error propagates D. Retried
**Q06 (O2)** `join()` throws: A. `ExecutionException` B. `CompletionException` C. `IOException` D. Nothing
**Q07 (O3)** `completeOnTimeout(v, 300, MILLISECONDS)` does: A. Cancels the remote call B. Throws after 300 ms C. Retries D. Completes with `v` if not done in time
**Q08 (O3)** `cancel(true)` on a `CompletableFuture`: A. Does not interrupt a running task B. Interrupts the thread C. Stops the remote server D. Always throws
**Q09 (O4)** The default pool for `supplyAsync` without an executor is: A. A new thread each call B. A virtual-thread pool C. The common `ForkJoinPool` D. A single thread
**Q10 (O4)** Blocking I/O in async stages should use: A. The common pool B. A dedicated executor C. The caller thread of `main` only D. No executor

## Answers
Q01 C · Q02 A · Q03 B · Q04 D · Q05 C · Q06 B · Q07 D · Q08 A · Q09 C · Q10 B

## Practical part
Six exercises `MID-006-EX01` to `EX06` including fixing a broken async chain, plus the lab. Pass: at least five exercises correct and the lab showing latency near the slowest call with graceful degradation.
