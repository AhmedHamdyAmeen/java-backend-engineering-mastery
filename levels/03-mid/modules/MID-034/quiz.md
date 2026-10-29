# MID-034 · Rate limiting — Quiz

Outcomes: O1 algorithms · O2 implementation and 429 · O3 limits, quotas, shedding · O4 good clients.

**Q01 (O1)** A token bucket allows: A. Only constant spacing B. Bursts up to its capacity C. No bursts D. Unlimited traffic
**Q02 (O1)** The fixed-window weakness is: A. No counting B. Cannot use Redis C. A burst across the window edge can double the rate D. It encrypts requests
**Q03 (O1)** A leaky bucket mainly: A. Grants bursts B. Counts monthly use C. Drops 4xx D. Smooths output to a steady rate
**Q04 (O2)** Correct status when a client exceeds its rate: A. 429 B. 401 C. 404 D. 201
**Q05 (O2)** `Retry-After` tells the client: A. Its identity B. The cache lifetime C. How long to wait before retrying D. The server version
**Q06 (O2)** In-memory limiting behind 3 instances effectively allows: A. The limit divided by 3 B. About 3× the intended limit C. Exactly the limit D. No requests
**Q07 (O3)** A monthly plan allowance is a: A. Quota B. Load shedder C. Token bucket only D. Circuit breaker
**Q08 (O3)** Load shedding reacts to: A. One client's speed B. Plan tier C. Server overload D. DNS failures
**Q09 (O4)** On `429` a good client: A. Retries immediately B. Waits per `Retry-After`, then retries within a cap C. Opens more connections D. Ignores it
**Q10 (O4)** To reduce calls to a limited API: A. Cache and batch where possible B. Increase threads C. Remove timeouts D. Use random keys

## Answers
Q01 B · Q02 C · Q03 D · Q04 A · Q05 C · Q06 B · Q07 A · Q08 C · Q09 B · Q10 A

## Practical part
Six exercises `MID-034-EX01` to `EX06` plus `MID-034-LAB1`. Pass: at least five exercises, 8 of 10 quiz answers, and a load test where one abusive client does not degrade others.
