# MID-039 · Caching patterns — Exercises and lab

## Lab
### MID-039-LAB1 · Fresh catalog
**Outcomes:** 1–3 · **Time:** ~2.5 h
Implement cache-aside for product reads. When the catalog service publishes `ProductUpdated`, the cache consumer evicts the key. Keep a TTL as safety net. Measure the delay between a price change and the new price being visible.
**Acceptance:** price change visible within one second.

## Exercises (assessment: pattern-choice scenarios)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-039-EX01 | 1 | Write a cache-aside `getProduct` and `updateProduct` and state what happens if Redis is down. |
| MID-039-EX02 | 1 | Compare read-through and write-through: who calls the database in each, and what fails when the database is slow? |
| MID-039-EX03 | 3 | Decide whether write-behind is acceptable for: page-view counts, orders, user profile edits. Justify. |
| MID-039-EX04 | 2 | Choose an invalidation strategy for product price, category names, and the home-page banner. |
| MID-039-EX05 | 1 | Explain what goes wrong with "update the cache, then the database" if the database write fails. |

## Solutions
- **EX01** See L01 code. Redis down: reads go to the database (slower, correct); writes still succeed; wrap cache calls so cache errors do not fail the request.
- **EX02** Read-through: cache layer loads on miss. Write-through: cache layer writes to the database synchronously. Slow database makes cache misses and writes slow too.
- **EX03** Page views: yes (loss tolerable). Orders: no. Profile edits: no, users expect saved data.
- **EX04** Price: event-driven eviction plus a short TTL. Category names: TTL of an hour is fine. Banner: TTL or delete on admin change.
- **EX05** The cache holds a value that was never stored: readers see data that does not exist. Write the database first, then delete the cache entry.

**Outcome 2** is also covered by the lab criterion (price visible within one second).
