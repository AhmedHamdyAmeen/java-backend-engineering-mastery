# MID-007 · Virtual threads — Quiz (when virtual threads help)

Outcomes: O1 how they work · O2 Spring Boot and measuring · O3 pinning and limits · O4 resource limits.

**Q01 (O1)** A virtual thread blocked on supported I/O: A. Holds its carrier B. Kills the JVM C. Unmounts so the carrier can run another D. Becomes a platform thread
**Q02 (O1)** Virtual threads are best for: A. CPU-bound loops B. Blocking I/O workloads C. GPU work D. Memory leaks
**Q03 (O1)** You should create virtual threads: A. In a fixed pool of 200 B. One per task, not pooled C. Only at startup D. Only for CPU work
**Q04 (O2)** The Spring Boot property to enable them is: A. `spring.threads.virtual.enabled=true` B. `server.virtual=on` C. `spring.async.mode=virtual` D. `jvm.threads=virtual`
**Q05 (O2)** After enabling them you should: A. Assume a speed-up B. Rewrite controllers reactively C. Remove timeouts D. Measure with a load test
**Q06 (O3)** Pinning means: A. Pausing GC B. A virtual thread cannot unmount while blocked C. A thread priority D. A failed deployment
**Q07 (O3)** A CPU-bound endpoint on virtual threads will: A. Run much faster B. Use less CPU C. Show little or no gain D. Fail to start
**Q08 (O1)** The core idea of structured concurrency is: A. Removing all locks B. Pooling virtual threads C. Faster GC D. Subtasks are bounded by a scope that waits for them
**Q09 (O4)** With 10,000 virtual threads and a 10-connection pool, the bottleneck is: A. The pool B. The CPU cache C. Thread creation D. The network card
**Q10 (O4)** To protect a limited downstream service you should: A. Remove all limits B. Use a `Semaphore` or bounded pool C. Pool virtual threads D. Increase carriers to 1,000

## Answers
Q01 C · Q02 B · Q03 B · Q04 A · Q05 D · Q06 B · Q07 C · Q08 D · Q09 A · Q10 B

## Practical part
Six exercises `MID-007-EX01` to `EX06` (including workload scenarios on when virtual threads help) plus the lab. Pass: at least five exercises correct and the lab explaining the new bottleneck.
