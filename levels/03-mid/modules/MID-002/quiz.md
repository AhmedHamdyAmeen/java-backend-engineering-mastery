# MID-002 · Memory management — Quiz

Outcomes: O1 generations and roots · O2 collectors · O3 GC logs · O4 containers · O5 leaks.

**Q01 (O1)** Which is a GC root? A. A local variable on a thread stack B. Any object on the heap C. An unreferenced object D. A comment
**Q02 (O1)** The generational hypothesis says: A. Old objects die first B. Most objects die young C. All objects live equally long D. Objects never die
**Q03 (O1)** An unreachable object cycle is: A. Leaked forever B. Collected C. Promoted D. Pinned
**Q04 (O2)** Best fit for a nightly batch import: A. ZGC B. G1 C. Parallel D. None
**Q05 (O2)** Which collector offers very short concurrent pauses on large heaps? A. Serial B. Parallel C. G1 only D. ZGC
**Q06 (O3)** `612M->140M(1024M)` in a GC line shows: A. Pause then total B. Three heaps C. Heap used before and after, then capacity D. Disk usage
**Q07 (O3)** A rising post-GC heap floor suggests: A. Healthy operation B. Too many CPUs C. A fast network D. A leak
**Q08 (O4)** A pod is OOM-killed (exit 137) with heap below `-Xmx`. Likely cause: A. Non-heap memory exceeded the container limit B. A JIT bug C. Java ignores limits D. Disk full
**Q09 (O4)** The better way to size heap in containers is: A. Fixed `-Xmx` larger than the limit B. No setting ever C. `-Xss` D. `-XX:MaxRAMPercentage` below 100
**Q10 (O5)** Fixing a leak by raising `-Xmx` will: A. Remove the leak B. Free the cache C. Only delay the failure D. Speed up the GC

## Answers
Q01 A · Q02 B · Q03 B · Q04 C · Q05 D · Q06 C · Q07 D · Q08 A · Q09 D · Q10 C

## Practical part
Six exercises `MID-002-EX01` to `EX06` including the provided GC-log diagnosis, plus the lab with before/after charts. Pass: at least five exercises correct and the leak located and proven fixed.
