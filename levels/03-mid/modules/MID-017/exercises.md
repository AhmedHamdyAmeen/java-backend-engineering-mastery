# MID-017 · Connection pooling — Exercises and lab

## Lab
### MID-017-LAB1 · Pool tuning
**Outcomes:** 1–4 · **Time:** ~2 h
Load-test Shop's checkout with pool sizes 5, 10, 50, and 200 (same test, same database). Record throughput, p95 latency, pending threads, and database CPU, and explain the results.
**Acceptance:** a chart plus a written pool-size recommendation with reasoning.

## Exercises (assessment: sizing scenarios)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-017-EX01 | 1 | List four costs of opening a new PostgreSQL connection per request. |
| MID-017-EX02 | 1 | Explain what happens when all HikariCP connections are in use and a thread asks for another. |
| MID-017-EX03 | 2 | A service handles 300 req/s with 20 ms average connection hold time and runs on 4 instances. Estimate the pool size per instance. |
| MID-017-EX04 | 2 | The database allows 100 connections; you have 12 instances. Choose a pool size and justify it, leaving room for admin and migrations. |
| MID-017-EX05 | 3 | Configure `connectionTimeout`, `leakDetectionThreshold`, and `statement_timeout`, and say what each protects against. |
| MID-017-EX06 | 3 | Given a thread dump excerpt with 40 threads in `getConnection`, list the next three diagnostic steps. |
| MID-017-EX07 | 4 | Explain in a paragraph why a pool of 200 can give lower throughput than a pool of 10. |

## Solutions
- **EX01** TCP handshake, TLS, authentication, backend process creation and server memory.
- **EX02** The thread waits up to `connectionTimeout`, then gets an exception; the pool's pending count rises.
- **EX03** 300 × 0.02 = 6 connections in use in total, about 1.5 per instance on average; use 3–5 per instance for headroom and bursts.
- **EX04** About 5–6 per instance (60–72 total), leaving room for admin sessions and migrations; check whether the database can actually serve that concurrency.
- **EX05** Timeout fails fast instead of piling up threads; leak detection logs holder stack traces; statement timeout stops runaway queries.
- **EX06** Look at the holders' stacks (what are they doing), pool metrics (active/pending), and slow queries or remote calls inside transactions.
- **EX07** Too many concurrent queries cause CPU contention, context switches, lock contention, and cache pressure; a small pool queues work cheaply in the app.
- Outcome 1 is also covered in the quiz.
