# MID-033 · Resilience — Exercises and lab

## Lab
### MID-033-LAB1 · Resilient checkout
**Outcomes:** 1–4 · **Time:** ~3 h
Protect `orders` calls to `payments` and `inventory` with explicit timeouts derived from a 1 s checkout budget, retries with exponential backoff and jitter (idempotent calls only), a circuit breaker, and a bulkhead (Resilience4j). Make product pages degrade when `reviews` is down. Use Toxiproxy to inject latency, errors, and outages.

**Acceptance:** Toxiproxy experiments show contained failures: product pages stay healthy while `payments` is slow, the breaker opens and recovers, and no non-idempotent request is retried.

## Exercises (assessment: resilience design review)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-033-EX01 | 1 | Compute the latency budget for checkout (target 1 s) across inventory, payments, and own processing; state each timeout. |
| MID-033-EX02 | 2 | List which Shop calls are safe to retry and which are not; add idempotency keys where needed. |
| MID-033-EX03 | 2 | Compute backoff delays for 4 attempts with base 100 ms, factor 2, and describe where jitter goes. |
| MID-033-EX04 | 3 | Write the Resilience4j circuit-breaker configuration for `payments` and explain each value. |
| MID-033-EX05 | 3 | Choose bulkhead limits for `payments`, `inventory`, and `reviews` and justify them. |
| MID-033-EX06 | 4 | Specify fallbacks for reviews, recommendations, stock display, and payment: which degrade, which fail. |
| MID-033-EX07 | 1–4 | Review a given design (no timeouts, retry on POST, shared pool) and list five fixes by priority. |

## Solutions
- **EX01** Example: own work 150 ms, inventory 250 ms, payments 450 ms, margin 150 ms. Downstream timeouts below the caller's.
- **EX02** Safe: GET product, GET stock. Retry only with an idempotency key: `POST /payments`, reserve stock. Never blind-retry a plain POST.
- **EX03** Delays about 100, 200, 400 ms (for retries after attempts 1 to 3); apply jitter by multiplying each by a random factor (for example 0.5 to 1.5) or using "full jitter" (random from 0 to the delay).
- **EX04** Sliding window 20, failure rate 50%, slow-call threshold 500 ms, wait 10 s in open state, 3 permitted half-open calls; count timeouts and 5xx only.
- **EX05** Example: `payments` 20 concurrent, `inventory` 30, `reviews` 10 with zero wait; derive from expected concurrency (rate × latency) plus headroom.
- **EX06** Reviews and recommendations: empty with notice. Stock display: cached or "check at checkout". Payment: fail clearly or keep the order pending.
- **EX07** 1 add timeouts; 2 remove blind POST retry or add idempotency key; 3 separate pools per dependency; 4 add breaker; 5 define honest fallbacks.

Outcome 4 is also covered by quiz Q09 and Q10.
