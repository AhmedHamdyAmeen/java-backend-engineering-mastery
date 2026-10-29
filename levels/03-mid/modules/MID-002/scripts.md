# MID-002 · Memory management — Lecture scripts

**Video:** 82 min · **Analogy used throughout:** a hotel: guests (objects) get rooms, the housekeeping crew (GC) clears rooms nobody can be reached in, and a guest who never checks out (a leak) fills the building.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-002-L01 · How the JVM allocates objects (10 min)
**Goal:** explain why allocation is cheap and what it costs later.

**Key points**
- Most objects are allocated in the young generation by bumping a pointer inside a thread-local allocation buffer (TLAB); no lock needed.
- Cheap allocation is why short-lived objects are fine in Java.
- Allocation rate (MB/s) drives how often the GC runs.
- Very large objects may go straight to a special region or the old generation (collector-specific).
- `OutOfMemoryError: Java heap space` means the live set no longer fits, not that allocation is slow.

**Show**
```java
List<OrderLine> lines = new ArrayList<>();   // 1 object, then N OrderLine objects
for (var item : cart) lines.add(new OrderLine(item));
```

**Check:** What do you measure to know GC pressure? *(Allocation rate, with GC frequency and pause times.)*

---

## MID-002-L02 · Generations, GC roots, and reachability (12 min)
**Goal:** explain how the GC decides what is garbage.

**Key points**
- An object is live if reachable from a GC root: thread stacks, static fields, JNI references.
- Weak generational hypothesis: most objects die young, so collect the young generation often and cheaply.
- Survivors are copied between survivor spaces; after enough collections they are promoted to old.
- Old generation is collected less often; a leak shows up as old-gen growth.
- Unreachable cycles are collected; reference counting is not used.

**Show:** a diagram: roots -> objects; Eden -> Survivor -> Old; an unreachable island marked as garbage.

**Check:** Is an object in a `static` map live? *(Yes, while the map is reachable from a static root, even if never read.)*

---

## MID-002-L03 · Collectors: G1, ZGC, Parallel (14 min)
**Goal:** pick a collector for a latency or throughput goal.

**Key points**
- Parallel GC: maximizes throughput with stop-the-world pauses; good for batch jobs.
- G1: region-based, targets a pause goal (`-XX:MaxGCPauseMillis`); the default in modern JDKs; a sound general choice.
- ZGC: concurrent, very short pauses even on large heaps; trades some throughput and memory; generational mode in newer JDKs (verify version before recording).
- Choose from a requirement (p99 latency, throughput), then measure.
- Do not switch collectors without a baseline.

**Show**
| Goal | Start with |
| --- | --- |
| Batch throughput | Parallel |
| Typical web API | G1 |
| Strict latency, big heap | ZGC |

**Check:** Which collector for a nightly import with no latency target? *(Parallel.)*

---

## MID-002-L04 · Reading GC logs (12 min)
**Goal:** enable unified GC logging and read its key fields.

**Key points**
- Enable: `-Xlog:gc*:file=gc.log:time,uptime` (verify flags for your JDK).
- Each line shows the collection type, heap before -> after (total), and pause duration.
- Healthy: frequent short young pauses; heap after full/mixed collections returns to a stable floor.
- Warning signs: floor rising over time (leak), full GCs, pauses over the goal, back-to-back collections (allocation pressure).
- Tools such as GCViewer or GCeasy help; learn to read the raw lines first.

**Show**
```
[12.3s] GC(41) Pause Young (Normal) (G1 Evacuation Pause) 612M->140M(1024M) 8.4ms
```

**Check:** What does `612M->140M(1024M)` mean? *(Heap used before and after the pause, with current heap capacity.)*

---

## MID-002-L05 · The JVM inside a container (10 min)
**Goal:** size heap and container limits so they fit together.

**Key points**
- Modern JVMs read cgroup limits; the default max heap is a fraction of container memory.
- Set it explicitly with `-XX:MaxRAMPercentage` (for example 60-75), not a fixed `-Xmx` that ignores the limit.
- Heap is only part of process memory: metaspace, thread stacks, code cache, direct buffers also count.
- If total exceeds the limit, the container is OOM-killed (exit 137), with no Java exception.
- Set CPU limits knowing they change the GC and compiler thread counts.

**Show**
```
container limit 1 GiB -> MaxRAMPercentage=70 -> heap ~700 MiB, ~300 MiB left for non-heap
```

**Check:** Why can a pod be killed while heap usage looks fine? *(Non-heap memory pushed the process over the container limit.)*

---

## MID-002-L06 · Memory leaks in managed languages (10 min)
**Goal:** recognize how leaks happen with a GC.

**Key points**
- A Java leak is an object that is still reachable but no longer needed.
- Classic sources: unbounded caches, static collections, listeners never removed, `ThreadLocal` values in pooled threads, unclosed resources.
- Symptom: old-gen floor rises across GCs; eventually `OutOfMemoryError` and long full GCs.
- Raising `-Xmx` only delays the failure.
- Fix the retention path: bound the cache, remove the reference.

**Show**
```java
private static final Map<Long, Product> CACHE = new HashMap<>(); // never evicted
```

**Check:** Why does the GC not free the leaked entries? *(They are still reachable through the static map.)*

---

## MID-002-L07 · Demo: finding a leak with two heap dumps (14 min)
**Goal:** locate a leak by diffing dumps; prepares MID-002-LAB1.

**Steps**
1. Start Shop with GC logging and the planted cache; run steady load.
2. Confirm in the log that the post-GC floor keeps rising.
3. Take dump A (`jcmd <pid> GC.heap_dump a.hprof`), run load a few more minutes, take dump B.
4. Open both in Eclipse MAT or VisualVM; compare histograms and find the class with growing instance count.
5. **Planned mistake:** raise `-Xmx` first and declare it fixed because the crash is later. Fix: follow the path to GC roots (dominator tree, "path to GC roots") to the static map.
6. Bound the cache (size limit/eviction), rerun, and show a flat floor.
