# MID-004 · Thread safety — Lecture scripts

**Video:** 96 min · **Analogy used throughout:** a shared whiteboard in a busy office: two people erasing and rewriting at once corrupt it; fixes are one pen at a time (lock), a single-stroke update (atomic), or giving each person their own board (confinement).
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-004-L01 · Race conditions (10 min)
**Goal:** spot a race and a check-then-act bug.

**Key points**
- A race condition: the result depends on thread timing.
- `count++` is read, add, write: three steps, so updates can be lost.
- Check-then-act: `if (stock > 0) stock--;` can oversell when two threads pass the check.
- Races are intermittent; passing tests do not prove safety.
- Shared mutable state is the root; remove sharing or mutation, or guard it.

**Show**
```java
if (stock >= qty) {      // thread A and B both pass
    stock -= qty;        // both subtract: oversell
}
```

**Check:** Why is `count++` unsafe? *(It is not atomic: read, modify, write can interleave.)*

---

## MID-004-L02 · Visibility and happens-before (14 min)
**Goal:** explain why a thread may not see another's write.

**Key points**
- CPU caches and compiler reordering mean a write may not be visible to other threads.
- The Java Memory Model defines happens-before: if A happens-before B, B sees A's writes.
- Practical edges: unlock then lock of the same monitor; write then read of a `volatile`; `Thread.start()` and `join()`; executor submit then task run, and task completion then `Future.get()`.
- Without such an edge, a loop on a plain flag may never stop.
- Visibility and atomicity are different problems.

**Show**
```java
boolean running = true;                  // not volatile
while (running) { work(); }              // may spin forever
```

**Check:** Name two actions that create a happens-before edge. *(Monitor unlock/lock, `volatile` write/read, `start`/`join`.)*

---

## MID-004-L03 · `synchronized` and intrinsic locks (10 min)
**Goal:** use `synchronized` correctly.

**Key points**
- Every object has an intrinsic lock; `synchronized` gives mutual exclusion and visibility.
- Synchronize the whole compound action, and use the same lock everywhere the data is touched.
- Do not lock on mutable fields, public objects, or `String`/boxed values; use a private final lock object.
- It is reentrant; keep critical sections short; never call unknown code while holding a lock.
- `wait`/`notify` exist but higher-level tools are usually better.

**Show**
```java
private final Object lock = new Object();
void reserve(int qty) { synchronized (lock) { if (stock >= qty) stock -= qty; } }
```

**Check:** Why not `synchronized(this)` in a public class? *(Outside code can lock the same object and interfere.)*

---

## MID-004-L04 · Explicit locks (10 min)
**Goal:** know when `ReentrantLock` beats `synchronized`.

**Key points**
- `ReentrantLock` offers `tryLock` (with timeout), interruptible locking, and fairness options.
- Always unlock in `finally`.
- `ReadWriteLock`/`StampedLock` help read-heavy data, but measure before adopting.
- `Condition` replaces `wait`/`notify` with several wait sets.
- Default to `synchronized` for simplicity; use explicit locks for the extra features.

**Show**
```java
if (lock.tryLock(100, TimeUnit.MILLISECONDS)) {
    try { reserve(qty); } finally { lock.unlock(); }
}
```

**Check:** Where must `unlock()` go? *(In a `finally` block.)*

---

## MID-004-L05 · `volatile` and atomics (10 min)
**Goal:** choose `volatile` or atomic classes correctly.

**Key points**
- `volatile` gives visibility and ordering for single reads and writes; not atomic compound actions.
- Good for flags and safe publication of immutable objects.
- `AtomicInteger`, `AtomicLong`, `AtomicReference` use compare-and-set for lock-free updates.
- `LongAdder` scales better than `AtomicLong` under heavy contention.
- Atomics protect one variable; invariants across several variables still need a lock.

**Show**
```java
private final AtomicInteger stock = new AtomicInteger(100);
boolean reserve(int q) {
    int cur;
    do { cur = stock.get(); if (cur < q) return false; }
    while (!stock.compareAndSet(cur, cur - q));
    return true;
}
```

**Check:** Does `volatile int count; count++` fix the race? *(No; `++` is still three steps.)*

---

## MID-004-L06 · Immutability and confinement (8 min)
**Goal:** avoid locking by design.

**Key points**
- Immutable objects (final fields, no setters, records) are safe to share freely.
- Replace state by swapping a reference to a new immutable snapshot.
- Thread confinement: data used by only one thread needs no lock (local variables, `ThreadLocal`).
- Spring singletons are shared by all requests; keep them stateless or hold only thread-safe state.
- Copy defensively when passing mutable data across threads.

**Show**
```java
record StockSnapshot(Map<String,Integer> levels) {}   // copy on update, swap an AtomicReference
```

**Check:** Why is a Spring `@Service` with a mutable field risky? *(One instance serves all requests concurrently.)*

---

## MID-004-L07 · Deadlocks (10 min)
**Goal:** recognize and prevent deadlock.

**Key points**
- Deadlock: threads each hold a lock and wait for another's; none proceeds.
- Four conditions: mutual exclusion, hold and wait, no preemption, circular wait.
- Prevention: acquire locks in a global order; hold fewer locks; use `tryLock` with timeout.
- Livelock and starvation are related: threads busy but no progress, or never scheduled.
- Thread dumps report deadlocks explicitly.

**Show:** transfer(a,b) and transfer(b,a) locking in opposite order; fix by locking the lower ID first.

**Check:** What simple rule prevents circular wait? *(Always acquire locks in the same global order.)*

---

## MID-004-L08 · Demo: reproducing a race with a stress test (12 min)
**Goal:** prove a race exists before fixing it; prepares MID-004-LAB1.

**Steps**
1. Write `StockCounter` with `reserve(int)` using check-then-act.
2. Stress test: 100 threads each reserve 1 unit from 1,000, started together with a `CountDownLatch`; assert final stock is 900.
3. Run repeatedly; the test fails intermittently (stock above 900, or oversold).
4. **Planned mistake:** add `volatile` to the field and re-run; it still fails. Explain: visibility is not atomicity.
5. Fix with `synchronized`; the test passes across many runs.
6. Note that a passing run is evidence only when the test failed before the fix.

---

## MID-004-L09 · Demo: diagnosing a deadlock from a thread dump (12 min)
**Goal:** read a thread dump and fix the cause.

**Steps**
1. Run a Shop `transfer(from, to)` that locks both accounts in argument order; fire opposite transfers concurrently.
2. The app hangs; take a dump with `jcmd <pid> Thread.print`.
3. Find the "Found one Java-level deadlock" section; read which thread holds which lock and waits for which.
4. **Planned mistake:** restart the app and call it solved. Fix: record the dump, identify the lock order, then fix it.
5. Apply ordered locking (lower id first) and rerun the stress test; no hang.
