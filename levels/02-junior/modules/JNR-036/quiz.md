# JNR-036 · Spring Security — Quiz

Outcomes: O1 filter chain · O2 `SecurityFilterChain` rules · O3 `UserDetailsService` · O4 401 vs 403 · O5 security tests.

**Q01 (O1)** Spring Security protects requests mainly through: A. Servlet filters B. Database triggers C. JPA entities D. Maven plugins
**Q02 (O1)** If a security filter rejects a request: A. The controller still runs B. The controller does not run C. The database is queried D. The request is retried
**Q03 (O2)** Rules in `authorizeHttpRequests` are evaluated: A. Randomly B. Bottom to top C. Top to bottom, first match wins D. All at once
**Q04 (O2)** The safest last rule is: A. `anyRequest().permitAll()` B. `anyRequest().authenticated()` C. No last rule D. `anyRequest().anonymous()`
**Q05 (O2)** `hasRole("ADMIN")` checks for the authority: A. `ADMIN_ROLE` B. `admin` C. `ROLE_ADMIN` D. `ROLE:ADMIN`
**Q06 (O3)** `UserDetailsService` has the method: A. `findUser` B. `loadUserByUsername` C. `authenticate` D. `getPassword`
**Q07 (O4)** A request with no credentials to a protected URL gets: A. 403 B. 404 C. 200 D. 401
**Q08 (O4)** A logged-in customer calls an admin-only endpoint and gets: A. 401 B. 403 C. 500 D. 302
**Q09 (O5)** `@WithMockUser(roles = "ADMIN")` is used to: A. Create a database admin B. Run a test as a fake admin C. Disable security D. Log in over HTTP
**Q10 (O5)** An access-matrix test should include: A. Only the admin case B. Anonymous, wrong role, and right role C. Only happy paths D. Only anonymous

## Answers
Q01 A · Q02 B · Q03 C · Q04 B · Q05 C · Q06 B · Q07 D · Q08 B · Q09 B · Q10 B

## Practical part
Seven exercises `JNR-036-EX01` to `EX07` plus the lab; the access-matrix suite is the assessment. Pass: at least six exercises correct, the matrix covers every endpoint for all three callers, and quiz 8 of 10.
