# MID-007 · Virtual threads — Exercises and lab

## Lab
### MID-007-LAB1 · Load comparison
**Outcomes:** 1–4 · **Time:** ~2.5 h
Run Shop's slow-supplier endpoint under identical load with platform threads and with virtual threads. Record throughput, latency percentiles, and database pool saturation. Add a limit (semaphore or pool size) and re-run.
**Acceptance:** results explained, including the new bottleneck.

## Exercises (assessment: scenario quiz on when virtual threads help)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-007-EX01 | 1 | Explain in five sentences how a virtual thread differs from a platform thread and what happens when it blocks. |
| MID-007-EX02 | 1 | Run 10,000 tasks that sleep 1 s on a fixed pool of 200 and on a virtual-thread-per-task executor; compare times. |
| MID-007-EX03 | 2 | Enable virtual threads in Shop and prove via a log of `Thread.currentThread()` that requests run on virtual threads. |
| MID-007-EX04 | 3 | For four workloads (JDBC-heavy, blocking HTTP, image processing, file hashing), say whether virtual threads help. |
| MID-007-EX05 | 4 | Add a `Semaphore(20)` to protect a downstream client and show requests queueing safely. |
| MID-007-EX06 | 3 | Describe how you would detect pinning in a running service. |

## Solutions
- **EX01** Virtual threads are JVM-managed and cheap; they mount on carrier threads and unmount when blocked on supported I/O, freeing the carrier.
- **EX02** The pool takes about 10,000/200 x 1 s = 50 s; virtual threads take about 1-2 s.
- **EX03** Log `Thread.currentThread().isVirtual()` in a controller; it prints true when enabled.
- **EX04** JDBC-heavy: helps up to the pool limit. Blocking HTTP: helps. Image processing and hashing: CPU-bound, no gain.
- **EX05** Acquire before the call, release in `finally`; excess threads wait cheaply.
- **EX06** Use JFR's virtual-thread pinned event or the tracing flag (verify for the JDK in use), then check for blocking inside `synchronized` or native code.
- Outcome 2's measurement is also covered by the lab.
