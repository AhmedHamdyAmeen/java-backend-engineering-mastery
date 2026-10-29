# MID-052 · Application threats — Quiz

Outcomes: O1 STRIDE and DFDs · O2 OWASP API Top 10 · O3 abuse prevention · O4 threats to tests.

**Q01 (O1)** In STRIDE, the "T" stands for: A. Testing B. Throttling C. Tokens D. Tampering
**Q02 (O1)** Which element is most important to mark in a data-flow diagram? A. Font sizes B. Trust boundaries C. Team names D. Colors
**Q03 (O2)** Changing `/orders/42` to `/orders/43` exposes another user's order: A. SQL injection B. CSRF C. BOLA D. XSS
**Q04 (O2)** A user calling an admin endpoint successfully is: A. Broken function-level authorization B. Weak hashing C. A slow query D. A cache miss
**Q05 (O2)** An API with no rate, size, or pagination limits risks: A. Faster responses B. Unrestricted resource consumption C. Better logging D. Smaller payloads
**Q06 (O3)** Credential stuffing is best slowed by: A. Rate limits, MFA, and breached-password checks B. Longer URLs C. Bigger servers D. Hiding the login page
**Q07 (O3)** Promo-code reuse by parallel requests is best prevented by: A. A front-end check B. A longer code C. A database unique constraint or atomic check D. A CAPTCHA only
**Q08 (O3)** Why do vulnerability scanners rarely find business-logic abuse? A. Requests are valid but misuse the rules B. Scanners are too slow C. Java hides it D. HTTPS blocks them
**Q09 (O4)** A good mitigation for a top threat includes: A. A note in a wiki only B. An automated test in CI C. A meeting D. A new framework
**Q10 (O4)** When should the threat model be updated? A. Never after release B. Only yearly C. When a new flow, service, or data store is added D. Only after a breach

## Answers
Q01 D · Q02 B · Q03 C · Q04 A · Q05 B · Q06 A · Q07 C · Q08 A · Q09 B · Q10 C

## Practical part
Threat model review plus lab `MID-052-LAB1`. Pass: quiz at least 8/10, a reviewed model with a ranked top five, and five security tests running in CI.
