# MID-002 · Memory management — Exercises and lab

## Lab
### MID-002-LAB1 · Leaky cache
**Outcomes:** 1, 3, 5 (and 4) · **Time:** ~4 h
A planted unbounded cache in Shop leaks under load. Enable GC logging, run load, find the rising floor, take two heap dumps, identify the retaining path, fix it (bounded cache), and prove the fix with a second run. Set heap with `MaxRAMPercentage` for a 1 GiB container.
**Acceptance:** before/after heap charts.

## Exercises (assessment: diagnose a provided GC log)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-002-EX01 | 1 | Explain allocation, promotion, and GC roots using a Shop checkout request as the example. |
| MID-002-EX02 | 2 | Pick a collector for: nightly price import; checkout API p99 under 50 ms on a 16 GB heap; typical 2 GB web API. Justify each. |
| MID-002-EX03 | 3 | Enable GC logging on Shop; report allocation rate and average young pause over 5 minutes. |
| MID-002-EX04 | 3 | Given a provided GC log, state whether it shows a leak, allocation pressure, or neither, citing lines. |
| MID-002-EX05 | 4 | A pod has a 2 GiB limit and `-Xmx2g`. Explain the risk and give a corrected setting. |
| MID-002-EX06 | 5 | List the steps to compare two heap dumps and name three leak sources to check first. |

## Solutions
- **EX01** Order objects are allocated in Eden by pointer bump; request-scoped objects die in the next young GC; objects still referenced from static or long-lived structures survive and are promoted. Roots: stacks, statics.
- **EX02** Import: Parallel (throughput). 16 GB strict latency: ZGC. Typical API: G1 (default), tune only after measuring.
- **EX03** Use `-Xlog:gc*`; allocation rate is roughly the sum of (before minus previous after) divided by time; average the young pause durations.
- **EX04** A leak shows the post-collection used size climbing across mixed/full GCs; pressure shows frequent young GCs with a flat floor; "neither" shows flat floor and short pauses.
- **EX05** Heap alone fills the limit; metaspace, stacks and buffers push it over, so the container is OOM-killed. Use `-XX:MaxRAMPercentage=70` or `-Xmx1400m`.
- **EX06** Take dump A and later dump B; compare class histograms; inspect the dominator tree and path to GC roots. Check static collections, caches, and `ThreadLocal`/listeners.
- Outcome 1 is also covered by Q01-Q03 and outcome 5 by the lab.
