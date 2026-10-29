# MID-006 · Async programming — Lecture scripts

**Video:** 62 min · **Analogy used throughout:** ordering at a food court: you place several orders at once, get buzzers (futures), and combine the dishes on one tray when all are ready or the lunch break ends (deadline).
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-006-L01 · Futures vs CompletableFuture (8 min)
**Goal:** see why `Future` is limiting and what `CompletableFuture` adds.

**Key points**
- `Future.get()` blocks; there is no way to say "when done, do X".
- `CompletableFuture<T>` is a future you can chain, combine, and complete manually.
- `supplyAsync` runs a value-producing task; `runAsync` a no-result task.
- Each stage returns a new future; build a pipeline instead of blocking.
- Block only at the edge of the system, if at all.

**Show**
```java
CompletableFuture<Product> p = CompletableFuture.supplyAsync(() -> productClient.get(id), ioPool);
```

**Check:** What can a `CompletableFuture` do that `Future` cannot? *(Chain callbacks and combine results without blocking.)*

---

## MID-006-L02 · Composing stages (14 min)
**Goal:** pick the right combinator.

**Key points**
- `thenApply(fn)`: transform the result (map).
- `thenCompose(fn)`: fn returns another future; flattens (flatMap). Use for dependent calls.
- `thenCombine(other, fn)`: join two independent futures.
- `allOf(...)`: completes when all do; it returns `Void`, so read each future afterwards. `anyOf` takes the first.
- `thenAccept`/`thenRun` for side effects at the end.

**Show**
```java
var page = product.thenCombine(stock, PageParts::new)
                  .thenCombine(reviews, (parts, r) -> parts.with(r));
CompletableFuture<Order> o = userF.thenCompose(u -> loadLastOrder(u.id()));
```

**Check:** Which combinator for "call B using A's result, where B is async"? *(`thenCompose`.)*

---

## MID-006-L03 · Errors in async code (10 min)
**Goal:** propagate and handle failures.

**Key points**
- An exception completes the stage exceptionally; dependent stages are skipped and carry it forward.
- `exceptionally(fn)`: recover with a fallback value.
- `handle((v, ex) -> ...)`: see both result and error; `whenComplete` observes without changing.
- `join()` throws `CompletionException`; `get()` throws `ExecutionException`; the cause is wrapped.
- An unobserved failed future loses the error silently; always attach handling or read it.

**Show**
```java
CompletableFuture<List<Review>> r = reviewsF.exceptionally(ex -> List.of()); // degrade gracefully
```

**Check:** What does a downstream `thenApply` do when its source failed? *(It is skipped and the failure propagates.)*

---

## MID-006-L04 · Timeouts and cancellation (10 min)
**Goal:** bound waiting time.

**Key points**
- `orTimeout(d, unit)` fails with `TimeoutException`; `completeOnTimeout(value, d, unit)` supplies a default (Java 9+).
- `cancel(true)` on a `CompletableFuture` does not interrupt the running task; design tasks to check for cancellation.
- Apply a deadline to the whole fan-out and per-call timeouts to each.
- A timeout does not stop the remote work; pair with client-side timeouts.
- Combine: timeout then fallback.

**Show**
```java
reviews.completeOnTimeout(List.of(), 300, TimeUnit.MILLISECONDS);
```

**Check:** Does `cancel(true)` interrupt the thread in a `CompletableFuture`? *(No.)*

---

## MID-006-L05 · Which thread runs my stage? (8 min)
**Goal:** choose executors deliberately.

**Key points**
- Without an executor, async methods use the common `ForkJoinPool`, sized for CPU work.
- Blocking I/O in the common pool starves everything else that uses it, including parallel streams.
- Pass a dedicated executor for blocking calls: `supplyAsync(task, ioPool)`.
- Non-`Async` methods (`thenApply`) run on whichever thread completes the previous stage (or the caller if already complete); `thenApplyAsync` hops to a pool.
- Never call `join()` inside a stage on a pool that may be exhausted.

**Show:** a diagram: HTTP calls on an `ioPool`; light mapping stays on the completing thread.

**Check:** Why avoid blocking I/O on the common pool? *(It is small and shared; blocking starves other work.)*

---

## MID-006-L06 · Demo: fan-out to three services with a deadline (12 min)
**Goal:** aggregate product, stock, and reviews with a deadline; prepares MID-006-LAB1.

**Steps**
1. Create three simulated clients with delays 100, 150, and 400 ms using a dedicated `ioPool`.
2. Start all three, combine with `thenCombine`; measure total about 400 ms, not 650.
3. Make reviews fail; add `exceptionally` for an empty list and a `degraded` flag.
4. Add `completeOnTimeout` of 300 ms for reviews; show partial results.
5. **Planned mistake:** call `.join()` inside a `thenApply` on the common pool, then run many requests and watch throughput stall. Fix: compose futures (`thenCombine`/`thenCompose`) and join only at the end.
6. Print timings per scenario.
