# MID-040 · Cache consistency — Exercises and lab

## Lab
### MID-040-LAB1 · Flash sale
**Outcomes:** 1–4 · **Time:** ~2 h
Simulate a flash sale: 2000 requests per second on one product whose cache entry expires during the test. Measure database queries per second. Add stampede protection (lock or coalescing plus TTL jitter) and a local short-lived cache for the hot key. Write the staleness budget for the product.
**Acceptance:** database load stays bounded (state the measured maximum queries per second before and after).

## Exercises (assessment: race-condition analysis)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-040-EX01 | 1 | 1000 readers hit an expired key; each query takes 50 ms. Estimate database load without and with a single-flight lock. |
| MID-040-EX02 | 2 | Draw the interleaving that leaves a stale price after "database update then cache delete", and fix it with versioning. |
| MID-040-EX03 | 2 | Explain why "delete cache, then update database" is worse than the reverse. |
| MID-040-EX04 | 3 | Propose a mitigation for a hot product key across 20 instances. |
| MID-040-EX05 | 4 | Write a staleness budget for price, stock display, category tree, and product description. |

## Solutions
- **EX01** Without: up to 1000 identical queries in a 50 ms window. With a lock: 1 query; others wait about 50 ms or get the stale value.
- **EX02** Reader misses and reads old row; writer commits and deletes; reader writes old value. With versions: the cache write is "put if version > cached version", or the stored version is compared with the row version on read; the old value is rejected or short-lived.
- **EX03** A reader between the delete and the update reloads the old row and caches it; it stays stale until TTL.
- **EX04** Local Caffeine L1 with 1-2 s TTL, plus coalescing and jitter; optionally key replicas.
- **EX05** Example: price 1 s (event + short TTL), stock display 30 s (checkout verifies), category tree 1 h, description 10 min.

**Outcome 3** is also covered by the lab (hot key).
