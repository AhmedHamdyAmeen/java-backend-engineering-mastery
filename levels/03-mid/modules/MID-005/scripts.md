# MID-005 · Concurrent collections — Lecture scripts

**Video:** 50 min · **Analogy used throughout:** a conveyor belt in a packing station: workers put boxes on one end, others take them off the other, and the belt has a fixed length so a fast packer must wait.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-005-L01 · Why `synchronizedMap` is not enough (8 min)
**Goal:** see why per-call locking does not make compound actions safe.

**Key points**
- `Collections.synchronizedMap` locks each call, so single calls are safe.
- A sequence such as `get` then `put` is two calls; another thread can run between them.
- Iterating needs manual locking on the map, or you risk `ConcurrentModificationException`.
- One lock for the whole map limits throughput.
- Use collections designed for concurrency.

**Show**
```java
Integer n = map.get(sku);             // another thread may update here
map.put(sku, n == null ? 1 : n + 1);  // lost update
```

**Check:** Why is `get` then `put` unsafe on a synchronized map? *(The pair is not atomic; another thread can interleave.)*

---

## MID-005-L02 · `ConcurrentHashMap` (12 min)
**Goal:** use atomic map operations correctly.

**Key points**
- Fine-grained internal locking and lock-free reads allow high concurrency.
- `putIfAbsent`, `computeIfAbsent`, `compute`, `merge` are atomic per key.
- Keep the function passed to `compute`/`merge` short, side-effect free, and non-blocking; do not update the same map inside it.
- No `null` keys or values.
- `size()` and iteration are weakly consistent; they give a snapshot-like view, not a frozen one. Do not use them for exact decisions.

**Show**
```java
Map<String, LongAdder> views = new ConcurrentHashMap<>();
views.computeIfAbsent(sku, k -> new LongAdder()).increment();
Map<String, Integer> stock = new ConcurrentHashMap<>();
stock.merge(sku, 1, Integer::sum);
```

**Check:** Which call replaces `get`-then-`put` counting? *(`merge(key, 1, Integer::sum)`.)*

---

## MID-005-L03 · Blocking queues and producer-consumer (12 min)
**Goal:** build a bounded pipeline with backpressure.

**Key points**
- `BlockingQueue`: `put` blocks when full, `take` blocks when empty; `offer`/`poll` accept timeouts.
- `ArrayBlockingQueue` is bounded; `LinkedBlockingQueue` is unbounded unless given a capacity.
- A bounded queue gives backpressure: fast producers slow down instead of exhausting memory.
- Stopping consumers: send a poison pill, or interrupt the workers.
- Choose queue size from latency tolerance, not "large to be safe".

**Show**
```java
BlockingQueue<OrderEvent> q = new ArrayBlockingQueue<>(1_000);
// producer: q.put(event);   consumer: var e = q.take();
```

**Check:** What happens when a producer calls `put` on a full queue? *(It blocks until space is free.)*

---

## MID-005-L04 · Copy-on-write structures (6 min)
**Goal:** know when `CopyOnWriteArrayList` fits.

**Key points**
- Every write copies the whole array; reads need no lock and iterate a stable snapshot.
- Fits read-mostly, small lists such as listeners or configuration.
- Hurts with frequent writes or large lists (copy cost, garbage).
- Iterators do not reflect later changes and do not support `remove`.
- For frequent writes use other structures.

**Show:** a list of 5 event listeners read on every request, changed a few times a day: a good fit.

**Check:** Is it a good choice for a 1 million entry list updated every second? *(No; each write copies the whole array.)*

---

## MID-005-L05 · Demo: a bounded producer-consumer order pipeline (12 min)
**Goal:** build the order event buffer; prepares MID-005-LAB1.

**Steps**
1. Create an `ArrayBlockingQueue<OrderEvent>(50)` and a producer emitting events quickly.
2. Start 3 consumers on a fixed pool that "process" each event in 50 ms.
3. Log queue size and producer wait time; show the producer slowing down once the queue fills.
4. **Planned mistake:** swap in an unbounded `LinkedBlockingQueue` and watch the queue and heap grow without limit. Fix: restore a bound.
5. Add a poison pill per consumer for clean shutdown; verify produced equals consumed.
