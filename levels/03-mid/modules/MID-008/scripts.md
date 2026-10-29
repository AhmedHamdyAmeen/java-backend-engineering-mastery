# MID-008 · Performance profiling — Lecture scripts

**Video:** 90 min · **Analogy used throughout:** a doctor's workup: take vitals and scans (recordings, dumps) before prescribing, change one thing, then test again.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-008-L01 · Measure before you optimize (8 min)
**Goal:** apply a repeatable performance loop.

**Key points**
- Loop: measure, hypothesize, change one thing, re-measure.
- Intuition about hot spots is often wrong; the profile decides.
- Define the goal first (p95 latency, throughput) and measure under realistic load.
- Profile in production-like mode, not debug mode; run long enough to pass warm-up and repeat runs for variance.
- Keep an investigation log: what was measured, what changed, the result.

**Show:** a log template: symptom, evidence, hypothesis, change, before/after numbers.

**Check:** Why change only one thing per iteration? *(So you know which change caused the effect.)*

---

## MID-008-L02 · Java Flight Recorder (12 min)
**Goal:** record JFR data from a running service.

**Key points**
- JFR is a low-overhead event recorder built into the JVM, with a continuous mode.
- Start at launch: `-XX:StartFlightRecording=filename=shop.jfr,duration=120s`, or on a live process: `jcmd <pid> JFR.start`, then `JFR.dump`.
- Events: CPU samples, allocation, GC, locks, I/O, thread states, exceptions.
- Profiles (default vs profile settings) trade detail against overhead.
- Verify option details for your JDK before recording.

**Show**
```
jcmd <pid> JFR.start name=shop settings=profile duration=120s filename=shop.jfr
```

**Check:** Why is JFR suitable for production? *(Low overhead and built into the JVM.)*

---

## MID-008-L03 · JDK Mission Control tour (12 min)
**Goal:** navigate a recording in JMC.

**Key points**
- Open the `.jfr` file; the Automated Analysis page highlights likely issues first.
- Key views: Java Application (hot methods, allocation), Threads, Memory/GC, Lock Instances, I/O, Exceptions.
- Method Profiling shows stack traces sampled while running.
- Use the time range selector to isolate the load window.
- Treat automated hints as leads, not conclusions.

**Show:** screenshot walk: Automated Analysis, then Method Profiling, then Lock Instances.

**Check:** First page to open in JMC? *(Automated Analysis, for the leads.)*

---

## MID-008-L04 · CPU profiling and flame graphs (12 min)
**Goal:** read a flame graph and find the hot spot.

**Key points**
- Sampling profilers capture stacks many times per second.
- Flame graph: width equals share of samples; a wide frame at the top is hot code; the stack below shows who called it.
- Look for wide plateaus, not tall towers.
- Safepoint bias can mislead some profilers; JFR and async-profiler reduce it (verify).
- Flame graph tells where time goes, not whether time is waiting; combine with thread-state data.

**Show:** a flame graph where `String.format` called from `PriceFormatter` covers 38% of CPU.

**Check:** What does frame width represent? *(The share of samples that included that frame, so the share of time.)*

---

## MID-008-L05 · Thread dumps (10 min)
**Goal:** capture and read dumps for blocked or starved threads.

**Key points**
- Capture: `jcmd <pid> Thread.print` (or `jstack`); take 3 dumps a few seconds apart.
- Each thread shows state, stack, locks held and waited for.
- Many threads BLOCKED on one monitor means lock contention; the owner is named.
- Pool threads all parked and a queue growing means starvation.
- Dumps flag deadlocks explicitly.

**Show:** `"http-nio-8080-exec-17" BLOCKED on <0x...> owned by "exec-3"`.

**Check:** Why take several dumps? *(One shows a moment; repeats show what is stuck versus moving.)*

---

## MID-008-L06 · Heap dumps (10 min)
**Goal:** capture and analyze a heap dump for large retainers.

**Key points**
- Capture: `jcmd <pid> GC.heap_dump file.hprof`; it pauses the app and creates a large file; handle carefully (may contain secrets).
- Open in Eclipse MAT or VisualVM.
- Shallow size is the object itself; retained size is what would be freed if it went away.
- Dominator tree lists biggest retainers; "path to GC roots" explains why it is live.
- Compare two dumps to find growth.

**Show:** dominator tree: `ConcurrentHashMap` retaining 480 MB of `Product`.

**Check:** What is retained size? *(Memory that would be freed if that object were removed.)*

---

## MID-008-L07 · Demo: finding a slow endpoint's hot spot with JFR (14 min)
**Goal:** locate and fix a planted CPU hot spot; prepares MID-008-LAB1.

**Steps**
1. Reproduce: `/orders/report` has p95 of 900 ms under load.
2. Record 2 minutes with JFR (profile settings) during the load test.
3. In JMC, Method Profiling and flame graph: find the dominant frame (a regex compiled on every call).
4. Hypothesis: precompile the pattern. Change only that.
5. **Planned mistake:** "optimize" a different method that looked suspicious in code review. Show it was 1% of samples. Fix: follow the profile.
6. Re-measure under the same load; p95 drops; record before/after in the log.

---

## MID-008-L08 · Demo: thread starvation in a live service (12 min)
**Goal:** diagnose a hung endpoint with thread dumps; prepares MID-008-LAB1.

**Steps**
1. Under load Shop slows then stops responding; CPU is low.
2. Take three thread dumps; most request threads are WAITING in `Future.get` or BLOCKED on one lock.
3. Find the owner thread and the code path holding the lock while doing remote I/O.
4. **Planned mistake:** restart the service and move on. Fix: save the dumps first; they are the evidence.
5. Move the remote call outside the critical section (or increase isolation with a separate pool); repeat the load test.
6. Confirm with a fresh dump and JFR lock-contention events that waiting is gone.
