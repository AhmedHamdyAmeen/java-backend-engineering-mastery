# JNR-024 · API security fundamentals — Quiz

Outcomes: O1 authentication vs authorization · O2 sessions vs tokens · O3 HTTPS · O4 CORS and CSRF.

**Q01 (O1)** "Who are you?" is: A. Authorization B. Encryption C. Authentication D. Caching
**Q02 (O1)** A logged-in user without permission gets: A. 401 B. 403 C. 201 D. 304
**Q03 (O1)** Missing credentials usually gives: A. 403 B. 404 C. 200 D. 401
**Q04 (O2)** Which keeps login state on the server? A. A signed token only B. A cookie of nothing C. A session D. A URL
**Q05 (O2)** A downside of stateless tokens: A. They need server memory B. They are harder to revoke before expiry C. They cannot be sent in headers D. They require cookies
**Q06 (O3)** HTTPS protects against: A. Bugs in your code B. Wrong passwords C. SQL injection D. Eavesdropping and tampering on the network
**Q07 (O3)** In production, an API with tokens over plain HTTP is: A. Fine B. Faster, so preferred C. Unsafe, tokens can be read in transit D. Required
**Q08 (O4)** Two origins differ if they differ in: A. Path only B. Scheme, host, or port C. Query string D. Header order
**Q09 (O4)** CORS is enforced by: A. Browsers B. Every HTTP client C. The database D. The firewall only
**Q10 (O4)** CSRF mainly threatens APIs that authenticate with: A. Nothing B. Header tokens added by scripts C. Cookies the browser sends automatically D. API versions

## Answers
Q01 C · Q02 B · Q03 D · Q04 C · Q05 B · Q06 D · Q07 C · Q08 B · Q09 A · Q10 C

## Practical part
Six exercises `JNR-024-EX01` to `EX06` plus the CORS lab. Assessment is this quiz: pass at 8 of 10 correct and a lab where only the allowed origin succeeds.
