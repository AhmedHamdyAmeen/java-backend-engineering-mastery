# JNR-039 · OAuth 2.0 and OIDC basics — Quiz

Outcomes: O1 roles · O2 flows and PKCE · O3 OAuth vs OIDC · O4 resource server configuration.

**Q01 (O1)** The server that logs the user in and issues tokens is the: A. Resource server B. Client C. Resource owner D. Authorization server
**Q02 (O1)** In our setup the Shop API is the: A. Client B. Resource server C. Authorization server D. Resource owner
**Q03 (O2)** For a user logging in to a single-page app, use: A. Password grant B. Implicit grant C. Authorization code with PKCE D. Client credentials
**Q04 (O2)** For a back-end job with no user, use: A. Client credentials B. Authorization code C. Implicit D. Password grant
**Q05 (O2)** PKCE protects against: A. SQL injection B. Slow queries C. XSS D. A stolen authorization code being used
**Q06 (O3)** OIDC adds to OAuth 2.0: A. Encryption B. An ID token for login C. A database D. Faster tokens
**Q07 (O3)** The ID token should be sent to: A. The client app that logged the user in B. The resource API as a bearer token C. Any third party D. The URL
**Q08 (O3)** OAuth 2.0 by itself is mainly about: A. Authentication B. Delegated authorization C. Hashing D. Cookies
**Q09 (O4)** `issuer-uri` lets Spring: A. Send emails B. Discover the keys to validate tokens C. Create users D. Log out users
**Q10 (O4)** Mapping realm roles to authorities is done with: A. `JwtAuthenticationConverter` B. `PasswordEncoder` C. `DataSource` D. `ObjectMapper`

## Answers
Q01 D · Q02 B · Q03 C · Q04 A · Q05 D · Q06 B · Q07 A · Q08 B · Q09 B · Q10 A

## Practical part
Seven exercises `JNR-039-EX01` to `EX07` plus the lab; the flow-selection scenarios (EX02, EX07) are the assessment. Pass: at least six exercises correct, correct flow chosen in every scenario, and old self-issued tokens rejected.
