# SRC-016 · Performance engineering — Lecture scripts

**Video:** 92 min · **Running case:** *Order Processing at 10×* — Shop Platform's order subsystem must handle a 10× growth forecast, a 99.95% availability commitment, and a 15-minute recovery objective.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRC-016-L01 · A performance engineering process (10 min)
**Goal:** work on performance with a repeatable, target-driven loop.

**Key points**
- Start from a target tied to the SLO (for example checkout p99 under a value at 10× load), not from "make it faster".
- Loop: measure, find the biggest bottleneck, change one thing, re-measure, stop when the target is met.
- Use percentiles, not averages; users feel the tail.
- Performance work has a cost; stopping at the target is part of the discipline.

**Show** One-page plan: target, workload model, baseline numbers, hypotheses ranked by expected gain, stop rule.

**Check:** When do you stop optimizing? *(When the agreed target is met with margin.)*

---

## SRC-016-L02 · Microbenchmarks with JMH (12 min)
**Goal:** measure small code paths without common traps.

**Key points**
- JMH (Java Microbenchmark Harness) handles warm-up, forking, and measurement iterations.
- Traps: dead-code elimination (use a `Blackhole` or return values), constant folding, a loop the JIT optimizes away, shared state, unrepresentative data.
- Run several forks and report variance, not one number.
- Microbenchmarks answer narrow questions; confirm that the code path matters in the whole system.

**Show**
```java
@Benchmark
public int parseTotal(Fixture f, Blackhole bh) {
    return f.parser.total(f.line);   // input from @State, result consumed
}
```
Use `@Fork`, `@Warmup`, `@Measurement` with values suited to the case; verify JMH version before recording.

**Check:** Why return or consume the result in a benchmark? *(Otherwise the JIT may remove the computation as dead code.)*

---

## SRC-016-L03 · System benchmarks that predict production (12 min)
**Goal:** design load tests whose results transfer to production.

**Key points**
- Model the workload: request mix, data size, think time, arrival pattern (open model, requests arrive regardless of response time).
- Closed-loop tests slow down when the system slows, hiding overload (coordinated omission); prefer a constant arrival rate with latency recorded from the intended send time.
- Use production-like data volume, resources, and dependencies (or realistic stubs with latency).
- Increase load in steps to find the saturation point; run long enough for warm-up and steady state.

**Show** Test plan: workload mix, rate steps (1×, 5×, 10× forecast), duration, environment spec, pass criteria tied to SLO. Tools by role: a load generator that supports constant-rate arrivals; verify tool choices.

**Check:** Why prefer constant arrival rate? *(Closed loops back off when the system slows, hiding the latency users would see.)*

---

## SRC-016-L04 · Removing bottlenecks in order (10 min)
**Goal:** apply fixes in order of impact, one at a time.

**Key points**
- Find the bottleneck from evidence: profiler flame graphs, database query statistics, thread and pool metrics, resource saturation (USE: utilization, saturation, errors).
- Fix the largest one, re-measure; the next bottleneck then shows.
- Typical order: remove unnecessary work (N+1 queries, missing index), then caching, concurrency, and only then micro-tuning.
- Amdahl's law: removing a part that is 5% of the time can at best gain 5%.

**Show** Table of the checkout path: step | share of p99 | change | new share. Example: 45% in a query with a missing index, fixed first.

**Check:** Why not optimize a step that takes 3% of time? *(Even eliminating it gains at most 3%.)*

---

## SRC-016-L05 · Regression detection in CI (10 min)
**Goal:** catch slowdowns before they reach production.

**Key points**
- Run a small stable set of benchmarks on every change or nightly, on dedicated, consistent hardware.
- Compare against a baseline with a tolerance based on measured noise; use statistics, not a single run.
- Fail or warn with a report showing the difference and confidence.
- Keep the suite small and fast enough that people trust it; quarantine flaky benchmarks.

**Show** CI job description: run JMH subset, store JSON results as artifacts, compare to main-branch baseline, fail when slower by more than the tolerance with significance.

**Check:** Why use a noise-based tolerance? *(Run-to-run variation would otherwise cause false failures.)*

---

## SRC-016-L06 · Reporting results honestly (8 min)
**Goal:** communicate performance results with uncertainty and context.

**Key points**
- Report the setup: hardware, versions, data, workload, configuration.
- Show distributions and percentiles with repeat runs and confidence intervals, not a single average.
- State what the test does not show and what could differ in production.
- Present before and after on the same conditions, with the decision it supports.

**Show** Report outline: question, method, environment, results (chart with repeat runs), limits, recommendation.

**Check:** Why include limits in a performance report? *(So readers do not over-apply results to conditions you did not test.)*

---

## SRC-016-L07 · Demo: halving checkout p99 with evidence (15 min)
**Goal:** reduce checkout p99 by profiling and fixing in order; prepares SRC-016-LAB1.

**Steps**
1. Set the target and run a baseline load test at a constant rate; record percentiles.
2. Profile under load; read the flame graph and query statistics.
3. Fix the largest item (an N+1 query), re-run; record the new p99.
4. **Planned mistake:** tune a serializer that is 4% of time first. Fix: return to the ranked list and attack the largest remaining item.
5. Repeat until the target is met, then stop.
6. Write the before and after report with variance and caveats.

**Check:** What guides the order of fixes? *(Measured share of time in each step.)*

---

## SRC-016-L08 · Demo: a JMH benchmark that lied, and the fixed version (15 min)
**Goal:** expose benchmark traps and fix them; prepares SRC-016-LAB1.

**Steps**
1. Show a benchmark claiming a new parser is 100 times faster.
2. Inspect: the result is unused (dead-code elimination) and input is a constant.
3. **Planned mistake:** run it once in a plain `main` method with a stopwatch. Fix: use JMH with forks, warm-up, and measurement iterations.
4. Fix the benchmark: consume results through a `Blackhole`, use varied input from `@State`.
5. Re-run: the true improvement is modest, with reported error bars.
6. Add a note about what the microbenchmark does not show about the system.

**Check:** What suspicious sign did the first result show? *(An implausibly large speedup, which suggested the work was optimized away.)*
