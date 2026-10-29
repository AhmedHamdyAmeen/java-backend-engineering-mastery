# JNR-038 · Sessions and tokens — Quiz

Outcomes: O1 cookies and sessions · O2 JWT structure · O3 correct validation · O4 sessions vs tokens.

**Q01 (O1)** `HttpOnly` on a cookie means: A. Sent only over HTTPS B. JavaScript cannot read it C. Same-site only D. It never expires
**Q02 (O1)** `Secure` on a cookie means: A. It is encrypted B. It is hashed C. JavaScript cannot read it D. It is sent only over HTTPS
**Q03 (O1)** A session cookie normally holds: A. The password B. The full user record C. A random session ID D. A JWT secret
**Q04 (O2)** A JWT has how many dot-separated parts? A. 2 B. 3 C. 4 D. 1
**Q05 (O2)** The JWT payload is: A. Encrypted B. Hashed C. Secret D. Only encoded, so readable
**Q06 (O3)** Which claim names who the token is for? A. `iss` B. `exp` C. `aud` D. `sub`
**Q07 (O3)** A token with `alg: none` should be: A. Accepted B. Accepted over HTTPS C. Accepted for admins D. Rejected
**Q08 (O3)** Which check is NOT required? A. Signature B. Expiry C. Audience D. The token's color
**Q09 (O4)** Stateless tokens are hard to: A. Scale B. Revoke before expiry C. Send D. Sign
**Q10 (O4)** To limit the damage of a stolen access token: A. Never expire it B. Make it short-lived C. Put it in the URL D. Store it in claims

## Answers
Q01 B · Q02 D · Q03 C · Q04 B · Q05 D · Q06 C · Q07 D · Q08 D · Q09 B · Q10 B

## Practical part
Seven exercises `JNR-038-EX01` to `EX07` plus the lab; the token-validation exercise (EX05) is the assessment. Pass: at least six exercises correct, EX05 fully correct, and the tampered, expired, and wrong-audience tests passing.
