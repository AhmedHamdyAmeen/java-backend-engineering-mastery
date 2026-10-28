# MID-P1 — Advanced Java and JVM Internals

**Phase goal:** the learner understands what the JVM does with their code at runtime, writes correct concurrent code, and diagnoses memory, CPU, and threading problems with evidence instead of guesswork.

**Running project:** *Shop Platform* — the Junior Shop API, now treated as a production system. This phase profiles it, fixes its concurrency bugs, and moves its I/O-bound paths to virtual threads. Later phases split it into services.

**Phase total:** ~11.4 h video · ~31 h practice

---

### MID-001 · JVM architecture
`n: 109` · **Video:** 68 min · **Practice:** 3 h

**Prerequisites:** BEG-007, BEG-038, JNR-001

**Learning outcomes** — the learner can:
1. Describe class loading (loading, linking, initialization) and the class-loader hierarchy.
2. Read bytecode for a small method with `javap -c` and relate it to the source.
3. Name the runtime data areas (heap, stacks, metaspace, code cache) and what lives in each.
4. Explain interpretation, JIT compilation (C1/C2, tiered), and why performance changes during warm-up.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-001-L01 | From `.class` file to running code | 10 |
| MID-001-L02 | Class loading and class loaders | 12 |
| MID-001-L03 | Reading bytecode with `javap` | 12 |
| MID-001-L04 | Runtime data areas | 10 |
| MID-001-L05 | The JIT compiler and warm-up | 12 |
| MID-001-L06 | Demo: watching the JIT with `-XX:+PrintCompilation` | 12 |

**Lab** — `MID-001-LAB1` *Warm-up effect:* measure Shop's checkout latency for the first 1,000 requests after startup vs steady state; explain the curve. Acceptance: chart plus explanation referencing JIT tiers.

**Common mistakes:** benchmarking cold code; assuming the JVM runs bytecode as written.

**Assessment:** bytecode-reading quiz and a class-loading scenario (`NoClassDefFoundError` vs `ClassNotFoundException`).

**Career relevance:** basis for memory tuning (MID-002) and profiling (MID-008).

---

### MID-002 · Memory management
`n: 110` · **Video:** 82 min · **Practice:** 4 h

**Prerequisites:** MID-001

**Learning outcomes** — the learner can:
1. Explain generational collection, allocation, promotion, and GC roots.
2. Compare G1, ZGC, and Parallel GC and choose one for a latency- or throughput-focused service.
3. Enable and read GC logs, and identify allocation pressure and long pauses.
4. Size heap and container memory limits so the JVM respects the container.
5. Diagnose a memory leak by comparing heap dumps.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-002-L01 | How the JVM allocates objects | 10 |
| MID-002-L02 | Generations, GC roots, and reachability | 12 |
| MID-002-L03 | Collectors: G1, ZGC, Parallel | 14 |
| MID-002-L04 | Reading GC logs | 12 |
| MID-002-L05 | The JVM inside a container | 10 |
| MID-002-L06 | Memory leaks in managed languages | 10 |
| MID-002-L07 | Demo: finding a leak with two heap dumps | 14 |

**Lab** — `MID-002-LAB1` *Leaky cache:* a planted unbounded cache in Shop leaks under load; find it from GC logs and heap dumps, fix it, and prove the fix. Acceptance: before/after heap charts.

**Common mistakes:** raising `-Xmx` to "fix" a leak; ignoring container memory limits; tuning flags without measurement.

**Assessment:** diagnose a provided GC log.

**Career relevance:** production troubleshooting (SRC-015) and capacity planning (SRC-004).

---

### MID-003 · Java concurrency
`n: 111` · **Video:** 76 min · **Practice:** 4 h

**Prerequisites:** BEG-030, BEG-035

**Learning outcomes** — the learner can:
1. Create and coordinate threads and explain thread states.
2. Submit `Runnable` and `Callable` tasks to an `ExecutorService` and collect `Future` results.
3. Size a thread pool for CPU-bound vs I/O-bound work and explain queueing behavior.
4. Shut executors down correctly and handle task failures.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-003-L01 | Why concurrency: throughput and latency | 8 |
| MID-003-L02 | Threads and their lifecycle | 10 |
| MID-003-L03 | Executors and futures | 12 |
| MID-003-L04 | Thread pools: size, queue, rejection | 14 |
| MID-003-L05 | Shutdown and failure handling | 8 |
| MID-003-L06 | Demo: parallelizing the price-feed import | 12 |
| MID-003-L07 | Demo: a thread pool that silently drops work | 12 |

**Lab** — `MID-003-LAB1` *Parallel import:* import product prices from several suppliers concurrently with a bounded pool, timeouts, and failure reporting. Acceptance: wall-clock improvement measured; no lost tasks.

**Common mistakes:** unbounded queues; `newCachedThreadPool` under load; never calling `shutdown`.

**Assessment:** pool-sizing scenarios plus lab.

**Career relevance:** Tomcat and connection-pool sizing (MID-017).

---

### MID-004 · Thread safety
`n: 112` · **Video:** 96 min · **Practice:** 4 h

**Prerequisites:** MID-003

**Learning outcomes** — the learner can:
1. Identify race conditions and check-then-act bugs in code review.
2. Explain visibility and the Java Memory Model's happens-before at a practical level.
3. Choose between `synchronized`, `ReentrantLock`, `volatile`, and atomics.
4. Prefer immutability and confinement over locking, and avoid deadlocks with lock ordering.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-004-L01 | Race conditions | 10 |
| MID-004-L02 | Visibility and happens-before | 14 |
| MID-004-L03 | `synchronized` and intrinsic locks | 10 |
| MID-004-L04 | Explicit locks | 10 |
| MID-004-L05 | `volatile` and atomics | 10 |
| MID-004-L06 | Immutability and confinement | 8 |
| MID-004-L07 | Deadlocks | 10 |
| MID-004-L08 | Demo: reproducing a race with a stress test | 12 |
| MID-004-L09 | Demo: diagnosing a deadlock from a thread dump | 12 |

**Lab** — `MID-004-LAB1` *Stock counter:* fix a race in an in-memory stock counter three ways (lock, atomic, immutable snapshot) and compare. Acceptance: a stress test fails before and passes after each fix.

**Common mistakes:** `volatile` for compound actions; locking on mutable or public objects; state in Spring singletons.

**Assessment:** find concurrency bugs in five snippets.

**Career relevance:** essential for any shared state; distributed analogues in MID-032.

---

### MID-005 · Concurrent collections
`n: 113` · **Video:** 50 min · **Practice:** 2.5 h

**Prerequisites:** BEG-041, MID-004

**Learning outcomes** — the learner can:
1. Use `ConcurrentHashMap` atomic operations (`compute`, `merge`, `putIfAbsent`) correctly.
2. Build producer-consumer pipelines with `BlockingQueue`.
3. Explain when copy-on-write collections fit and when they hurt.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-005-L01 | Why `synchronizedMap` is not enough | 8 |
| MID-005-L02 | `ConcurrentHashMap` | 12 |
| MID-005-L03 | Blocking queues and producer-consumer | 12 |
| MID-005-L04 | Copy-on-write structures | 6 |
| MID-005-L05 | Demo: a bounded producer-consumer order pipeline | 12 |

**Lab** — `MID-005-LAB1` *Order event buffer:* buffer order events in a bounded queue consumed by worker threads with backpressure. Acceptance: producer slows when the queue is full; no events lost.

**Common mistakes:** `get` then `put` on a concurrent map; unbounded queues.

**Assessment:** 4 exercises.

**Career relevance:** backpressure in messaging (SRB-006).

---

### MID-006 · Async programming
`n: 114` · **Video:** 62 min · **Practice:** 3 h

**Prerequisites:** BEG-035, MID-003

**Learning outcomes** — the learner can:
1. Compose asynchronous work with `CompletableFuture` (`thenApply`, `thenCompose`, `thenCombine`, `allOf`).
2. Propagate and handle exceptions in async chains.
3. Apply timeouts and cancellation.
4. Choose the executor for async stages deliberately.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-006-L01 | Futures vs CompletableFuture | 8 |
| MID-006-L02 | Composing stages | 14 |
| MID-006-L03 | Errors in async code | 10 |
| MID-006-L04 | Timeouts and cancellation | 10 |
| MID-006-L05 | Which thread runs my stage? | 8 |
| MID-006-L06 | Demo: fan-out to three services with a deadline | 12 |

**Lab** — `MID-006-LAB1` *Product page aggregator:* fetch product, stock, and reviews concurrently with an overall deadline and partial results on failure. Acceptance: total latency ≈ slowest call; failures degrade gracefully.

**Common mistakes:** blocking `join()` inside stages; losing exceptions; using the common pool for blocking I/O.

**Assessment:** fix a broken async chain.

**Career relevance:** resilience patterns (MID-033).

---

### MID-007 · Virtual threads
`n: 115` · **Video:** 58 min · **Practice:** 2.5 h · `version:` current LTS

**Prerequisites:** MID-004, MID-006

**Learning outcomes** — the learner can:
1. Explain how virtual threads differ from platform threads and why they suit blocking I/O.
2. Enable virtual threads in Spring Boot and measure the effect.
3. Identify pinning and other cases where virtual threads do not help (CPU-bound work, limited downstream resources).
4. Explain why resource limits (connection pools, semaphores) still matter.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-007-L01 | The thread-per-request problem | 8 |
| MID-007-L02 | Virtual threads explained | 12 |
| MID-007-L03 | Virtual threads in Spring Boot | 8 |
| MID-007-L04 | Pinning and other pitfalls | 10 |
| MID-007-L05 | Structured concurrency (preview status) | 8 |
| MID-007-L06 | Demo: platform vs virtual threads under load | 12 |

**Lab** — `MID-007-LAB1` *Load comparison:* run Shop's slow-supplier endpoint under load with platform and virtual threads; record throughput, latency, and database pool saturation. Acceptance: results explained, including the new bottleneck.

**Common mistakes:** pooling virtual threads; expecting CPU-bound speed-ups; removing all concurrency limits.

**Assessment:** scenario quiz: when virtual threads help.

**Career relevance:** modern Java service design.

---

### MID-008 · Performance profiling
`n: 116` · **Video:** 90 min · **Practice:** 4 h

**Prerequisites:** MID-002, MID-004

**Learning outcomes** — the learner can:
1. Record and analyze a JFR recording in JDK Mission Control.
2. Find CPU hot spots with flame graphs.
3. Capture and read thread dumps to diagnose blocked or starved threads.
4. Capture and analyze a heap dump to find large retainers.
5. Follow a measure → hypothesize → change → re-measure loop.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-008-L01 | Measure before you optimize | 8 |
| MID-008-L02 | Java Flight Recorder | 12 |
| MID-008-L03 | JDK Mission Control tour | 12 |
| MID-008-L04 | CPU profiling and flame graphs | 12 |
| MID-008-L05 | Thread dumps | 10 |
| MID-008-L06 | Heap dumps | 10 |
| MID-008-L07 | Demo: finding a slow endpoint's hot spot with JFR | 14 |
| MID-008-L08 | Demo: thread starvation in a live service | 12 |

**Lab** — `MID-008-LAB1` *Profile Shop:* the instructor plants a CPU hot spot and a lock contention; find both from recordings alone, fix them, and show before/after evidence. Acceptance: written investigation log.

**Common mistakes:** optimizing by intuition; profiling in debug mode; one-off measurements.

**Assessment:** investigation of an unseen recording.

**Career relevance:** performance engineering (SRC-016) and the MID graduation gate.

---

### MID-009 · Advanced generics and reflection
`n: 117` · **Video:** 60 min · **Practice:** 2.5 h

**Prerequisites:** BEG-031, JNR-009

**Learning outcomes** — the learner can:
1. Explain type erasure and its consequences (no `new T()`, bridge methods, heap pollution).
2. Apply PECS to wildcard signatures.
3. Inspect classes, methods, and annotations with reflection and write a custom annotation processed at runtime.
4. Explain how Spring uses reflection and dynamic proxies (and why `@Transactional` self-invocation fails).

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-009-L01 | Type erasure | 10 |
| MID-009-L02 | Wildcards and PECS | 10 |
| MID-009-L03 | Reflection | 10 |
| MID-009-L04 | Custom annotations | 8 |
| MID-009-L05 | Dynamic proxies | 10 |
| MID-009-L06 | Demo: building a mini `@Timed` with a proxy | 12 |

**Lab** — `MID-009-LAB1` *Audit annotation:* an `@Audited` annotation and a proxy-based interceptor that logs calls. Acceptance: works through an interface; self-invocation limitation demonstrated.

**Common mistakes:** reflection in hot paths; raw types from erasure confusion.

**Assessment:** exercises plus a proxy-behavior quiz.

**Career relevance:** reading framework internals when debugging.

---

### MID-010 · Java module system
`n: 118` · **Video:** 43 min · **Practice:** 1.5 h

**Prerequisites:** BEG-027, JNR-002

**Learning outcomes** — the learner can:
1. Write `module-info.java` with `requires`, `exports`, and `opens`.
2. Explain the classpath vs the module path and strong encapsulation.
3. Decide whether a Spring service benefits from JPMS, and use alternatives (e.g., ArchUnit) for module boundaries.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-010-L01 | Classpath problems JPMS solves | 8 |
| MID-010-L02 | Writing module descriptors | 10 |
| MID-010-L03 | Reflection and `opens` | 7 |
| MID-010-L04 | JPMS in practice for backend services | 8 |
| MID-010-L05 | Demo: enforcing boundaries with ArchUnit | 10 |

**Lab** — `MID-010-LAB1` *Boundaries:* modularize Shop Core with JPMS and enforce Shop API's feature boundaries with ArchUnit tests. Acceptance: a forbidden dependency fails the build.

**Common mistakes:** adopting JPMS for frameworks that rely on deep reflection without `opens`.

**Assessment:** quiz plus lab.

**Career relevance:** modular monolith boundaries (MID-059).
