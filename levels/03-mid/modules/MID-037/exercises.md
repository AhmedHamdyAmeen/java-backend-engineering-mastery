# MID-037 · Caching fundamentals — Exercises and lab

## Lab
### MID-037-LAB1 · Cache candidates
**Outcomes:** 1–4 · **Time:** ~1.5 h
Collect access data for Shop's endpoints (request counts, latency, data change rate) from logs or metrics. Rank them and pick the three worth caching, with an expected hit ratio, TTL, and layer for each. Also list two endpoints you reject and why.
**Acceptance:** decision backed by access data (a table of numbers, not opinions).

## Exercises (assessment: quiz)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-037-EX01 | 1 | For `GET /products/{id}`, name each layer where it could be cached and what a hit there saves. |
| MID-037-EX02 | 2 | Shop runs 4 instances. Compare Caffeine and Redis for the category list; pick one and justify. |
| MID-037-EX03 | 3 | 1000 requests: 700 hits, 300 misses. Compute the hit ratio and the database calls saved. A miss costs 50 ms, a hit 1 ms: compute average latency. |
| MID-037-EX04 | 3 | A 3-slot LRU cache receives A B C A D B. Show the contents after each step. |
| MID-037-EX05 | 4 | Decide for each: `/cart`, `/products/{id}`, `/stock/{id}` during a flash sale, `/categories`. Cache or not, and with what TTL. |

## Solutions
- **EX01** Client (Cache-Control), CDN (static and public product JSON), gateway (short TTL responses), application (Caffeine/Redis: avoids DB), database (buffer pool).
- **EX02** Redis: shared, one invalidation point, survives restarts. Caffeine would be fine for a rarely changing list if a few minutes of drift is acceptable. Either with a stated tolerance is a valid answer.
- **EX03** Ratio 70%; 700 database calls saved. Average = 0.7 × 1 + 0.3 × 50 = 15.7 ms.
- **EX04** After A B C: [A B C]. A hit. D evicts B: [C A D]. B miss, evicts C: [A D B].
- **EX05** `/cart` per-user and changing: no shared cache. `/products/{id}`: yes, minutes. `/stock/{id}` during a flash sale: no, or a very short TTL with the database as authority. `/categories`: yes, long TTL.

**Outcomes 1-4** are also covered by the quiz and the lab criterion "decision backed by access data".
