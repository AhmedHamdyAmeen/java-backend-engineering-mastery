# MID-006 · Async programming — Exercises and lab

## Lab
### MID-006-LAB1 · Product page aggregator
**Outcomes:** 1–4 · **Time:** ~3 h
Fetch product, stock, and reviews concurrently from simulated services on a dedicated executor. Apply an overall deadline and per-call timeouts. On failure return partial results with a degraded marker.
**Acceptance:** total latency about equal to the slowest call; failures degrade gracefully.

## Exercises (assessment: fix a broken async chain)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-006-EX01 | 1 | Combine two independent price lookups with `thenCombine`, then fetch the seller using the result with `thenCompose`. |
| MID-006-EX02 | 1 | Wait for ten futures with `allOf` and collect the results into a list. |
| MID-006-EX03 | 2 | Given a chain that swallows an exception, fix it so the error is handled and logged with a fallback. |
| MID-006-EX04 | 3 | Add a 200 ms default-on-timeout to a slow call and show the default arriving. |
| MID-006-EX05 | 4 | Fix a chain that runs blocking HTTP calls on the common pool by passing an executor. |
| MID-006-EX06 | 2 | Explain `CompletionException` vs `ExecutionException` and unwrap the real cause. |

## Solutions
- **EX01** `a.thenCombine(b, Math::min).thenCompose(p -> sellerFor(p))`.
- **EX02** `CompletableFuture.allOf(arr).thenApply(v -> futures.stream().map(CompletableFuture::join).toList())`; `join` is safe here because all are complete.
- **EX03** Replace an empty `catch` or an unread future with `.handle((v, ex) -> { if (ex != null) { log.warn(...); return fallback; } return v; })`.
- **EX04** `slow.completeOnTimeout(DEFAULT, 200, MILLISECONDS)`.
- **EX05** `CompletableFuture.supplyAsync(() -> http.call(), ioPool)`.
- **EX06** `join()` throws `CompletionException` and `get()` throws `ExecutionException`; both wrap the original in `getCause()`.
