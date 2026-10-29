# MID-051 · Advanced API security — Quiz

Outcomes: O1 OAuth flows · O2 token validation · O3 scopes, claims, authorization design · O4 service-to-service identity.

**Q01 (O1)** A user-facing SPA should use: A. Implicit flow B. Client credentials C. Password flow D. Authorization code with PKCE
**Q02 (O1)** A nightly job with no user should use: A. Client credentials B. Authorization code C. Implicit flow D. No authentication
**Q03 (O2)** Validating tokens only at the gateway is risky because: A. Gateways are slow B. Direct calls to a service bypass it C. Tokens expire at once D. JWTs cannot be verified
**Q04 (O2)** The audience claim ensures: A. The token is short B. The user is an adult C. The token is encrypted D. The token was meant for this service
**Q05 (O2)** An `X-User-Id` header set by the gateway: A. Is always safe B. Replaces tokens C. Must not replace token validation in the service D. Is a standard claim
**Q06 (O3)** Scopes describe: A. What a client may do B. The user's password C. Server memory D. The database schema
**Q07 (O3)** The check that stops one customer reading another's order is: A. A scope B. A TLS certificate C. A role only D. An ownership check
**Q08 (O3)** Admin operations should: A. Share the read scope B. Have their own scope or role C. Need no check D. Be public
**Q09 (O4)** `orders` calls `inventory` with: A. The customer's password B. No token C. Its own client credentials token with limited scopes D. A shared admin token
**Q10 (O4)** Token exchange is used to: A. Encrypt tokens B. Swap a user token for a narrower one for the next service C. Extend expiry D. Create users

## Answers
Q01 D · Q02 A · Q03 B · Q04 D · Q05 C · Q06 A · Q07 D · Q08 B · Q09 C · Q10 B

## Practical part
Seven exercises `MID-051-EX01` to `EX07` (EX07 is the authorization design review) plus the zero-implicit-trust lab. Pass: at least five exercises including EX07, and a lab where a direct call without a valid token fails at every service.
