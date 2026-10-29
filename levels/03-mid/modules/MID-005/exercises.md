# MID-005 · Concurrent collections — Exercises and lab

## Lab
### MID-005-LAB1 · Order event buffer
**Outcomes:** 1–3 (mainly 2) · **Time:** ~2.5 h
Buffer Shop order events in a bounded queue consumed by worker threads. Count events per product with a `ConcurrentHashMap`. Shut down cleanly with poison pills.
**Acceptance:** producer slows when the queue is full; no events lost (produced equals consumed).

## Exercises (assessment: 4 exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-005-EX01 | 1 | Count words from 4 threads using `HashMap` and `get`/`put`; show lost updates; fix with `merge`. |
| MID-005-EX02 | 1 | Rewrite a `containsKey`/`put` cache fill with `computeIfAbsent`; explain what to avoid inside the function. |
| MID-005-EX03 | 2 | Build a producer-consumer with `ArrayBlockingQueue(10)`; show blocking `put` and a clean poison-pill stop. |
| MID-005-EX04 | 3 | For three cases (listener list, 500k-entry list written often, small read-mostly config), say whether copy-on-write fits and why. |

## Solutions
- **EX01** The `HashMap` total is below the expected count. `map.merge(word, 1, Integer::sum)` on a `ConcurrentHashMap` gives the exact total.
- **EX02** `cache.computeIfAbsent(k, this::load)`. Keep the function short, do not block on slow I/O if avoidable, and never modify the same map inside it.
- **EX03** The producer blocks when 10 items wait. Stop by putting one poison object per consumer; each consumer exits on receiving it.
- **EX04** Listener list: yes (read-mostly, small). 500k list written often: no (copy per write). Small read-mostly config: yes.
- The lab's backpressure criterion also covers outcome 2 in practice.
