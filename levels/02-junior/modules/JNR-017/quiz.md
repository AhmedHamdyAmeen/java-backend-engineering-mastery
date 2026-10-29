# JNR-017 · HTTP in depth — Quiz

Outcomes: O1 safe and idempotent · O2 content negotiation · O3 caching · O4 HTTP versions.

**Q01 (O1)** Which method is safe? A. POST B. PUT C. DELETE D. GET
**Q02 (O1)** Which method is idempotent but not safe? A. PUT B. GET C. POST D. HEAD
**Q03 (O1)** Why does idempotency matter? A. It makes JSON smaller B. Retrying is then harmless C. It encrypts traffic D. It speeds up queries
**Q04 (O2)** The `Accept` header says: A. What the body is B. Which formats the client can read C. Who the user is D. How long to cache
**Q05 (O2)** A client posts a body type the server cannot read. Expected status: A. 404 B. 406 C. 415 D. 201
**Q06 (O3)** A `304` response means: A. Created B. Server error C. Moved permanently D. Not modified, reuse your copy
**Q07 (O3)** Which header sends the client's stored ETag back? A. If-None-Match B. ETag C. Location D. Accept
**Q08 (O3)** Which is right for a response with a user's private data? A. `public, max-age=3600` B. `Cache-Control: private` or `no-store` C. No header, caches decide D. `max-age=31536000`
**Q09 (O4)** HTTP/2 multiplexing means: A. Many requests share one connection B. Responses are encrypted C. Servers use UDP only D. Bodies are always XML
**Q10 (O4)** Why reuse connections? A. To change the method B. To avoid repeated TCP/TLS setup cost C. To skip headers D. To get 304 responses

## Answers
Q01 D · Q02 A · Q03 B · Q04 B · Q05 C · Q06 D · Q07 A · Q08 B · Q09 A · Q10 B

## Practical part
Six exercises `JNR-017-EX01` to `EX06` plus the ETag lab. Pass: at least five exercises and a lab where the second request returns `304` with no body.
