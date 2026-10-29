# MID-034 · Rate limiting — Exercises and lab

## Lab
### MID-034-LAB1 · Fair use
**Outcomes:** 1–4 · **Time:** ~2 h
Add per-customer and per-IP limits to search and checkout (at the gateway or in the service, using a shared store so limits hold across replicas). Return `429` with `Retry-After`. Use different limits for search (generous) and checkout (strict). Write a small client that honors `Retry-After`.

**Acceptance:** a load test shows one abusive client cannot degrade others: normal clients keep their latency and success rate while the abuser receives `429`s.

## Exercises (assessment: quiz plus lab)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-034-EX01 | 1 | Simulate a token bucket (rate 2/s, capacity 5) for 10 requests arriving at once; state how many pass. |
| MID-034-EX02 | 1 | Explain the fixed-window double-burst problem with numbers and how a sliding window fixes it. |
| MID-034-EX03 | 2 | Write a Spring `OncePerRequestFilter` or gateway config returning `429` with `Retry-After`. |
| MID-034-EX04 | 2 | Explain why an in-memory limiter fails behind a load balancer and give two fixes. |
| MID-034-EX05 | 3 | Classify as rate limit, quota, or load shedding: 100 req/s per key; 10,000 calls per month; reject recommendation calls at 95% CPU. |
| MID-034-EX06 | 4 | Write client code that retries on `429` honoring `Retry-After`, with a cap. |

## Solutions
- **EX01** Bucket starts full: 5 pass, 5 are rejected; about 2 more pass each following second.
- **EX02** Limit 100/min: 100 requests at 12:00:59 and 100 at 12:01:00 give 200 in two seconds. A sliding window counts the last 60 s so the second burst is rejected.
- **EX03** Filter checks the limiter for the key, sets `429`, header `Retry-After: <seconds>`, and a JSON body; otherwise continues the chain.
- **EX04** Each instance counts separately so the limit multiplies by instance count. Fix: shared Redis counter with an atomic script, or enforce at a single gateway layer.
- **EX05** Rate limit; quota; load shedding.
- **EX06** Loop up to 3 attempts; on `429` parse `Retry-After` (seconds), sleep that long (plus small jitter), else exponential backoff; give up after the cap.

Outcome 1 is also checked by quiz Q02 to Q04.
