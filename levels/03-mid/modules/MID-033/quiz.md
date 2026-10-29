# MID-033 · Resilience — Quiz

Outcomes: O1 timeouts and budgets · O2 retries · O3 breakers and bulkheads · O4 fallbacks.

**Q01 (O1)** A remote call without a timeout can: A. Run faster B. Wait indefinitely and hold resources C. Never fail D. Skip retries
**Q02 (O1)** Downstream timeouts should be: A. Longer than upstream ones B. Identical everywhere C. Shorter than the caller's remaining budget D. Disabled in production
**Q03 (O1)** A slow dependency harms unrelated endpoints mainly because: A. Shared threads or connections fill with waiting calls B. JSON gets bigger C. Logs rotate D. DNS changes
**Q04 (O2)** Retrying is appropriate for: A. Validation errors B. Non-idempotent POSTs without keys C. Transient failures of idempotent calls D. Every 4xx
**Q05 (O2)** Jitter is used to: A. Encrypt retries B. Shorten timeouts C. Count failures D. Stop clients retrying in sync
**Q06 (O2)** Which is exponential backoff? A. 100, 200, 400 ms B. 100, 100, 100 ms C. Random per client only D. 1 s, 0 s, 1 s
**Q07 (O3)** An open circuit breaker: A. Retries more B. Fails calls fast C. Doubles timeouts D. Logs only
**Q08 (O3)** Circuit breakers should count as failures: A. All 4xx B. Only 200 C. Timeouts and 5xx D. Nothing
**Q09 (O3)** A bulkhead limits: A. Request size B. Concurrent calls per dependency C. Database rows D. Log levels
**Q10 (O4)** An honest fallback when `reviews` is down: A. Show fake reviews B. Return 500 for the whole page C. Hide the error silently as success D. Show the page with "reviews unavailable"

## Answers
Q01 B · Q02 C · Q03 A · Q04 C · Q05 D · Q06 A · Q07 B · Q08 C · Q09 B · Q10 D

## Practical part
Seven exercises `MID-033-EX01` to `EX07`, the resilience design review, and `MID-033-LAB1`. Pass: at least six exercises and Toxiproxy experiments showing contained failures with a breaker that opens and recovers.
