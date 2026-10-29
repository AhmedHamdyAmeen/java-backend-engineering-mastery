# JNR-036 · Spring Security — Exercises and lab

## Lab
### JNR-036-LAB1 · Secure Shop
**Outcomes:** 1–5 · **Time:** ~3 h
Secure the Shop API: public catalog reads; authenticated cart and orders; admin-only catalog writes. Load users from the database and return Problem Details for 401 and 403.
**Acceptance:** tests cover anonymous, customer, and admin access for every endpoint.

## Exercises (assessment: access-matrix test suite)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-036-EX01 | 1 | Draw the path of a request through the filter chain to a controller and say where a 401 is produced. |
| JNR-036-EX02 | 2 | Write a chain: `GET /api/products/**` public, `POST` and `DELETE` on products admin only, everything else authenticated. |
| JNR-036-EX03 | 2 | Find the bug: `anyRequest().permitAll()` then `requestMatchers("/admin/**").hasRole("ADMIN")`. |
| JNR-036-EX04 | 3 | Implement a `UserDetailsService` that loads a user by email from a repository. |
| JNR-036-EX05 | 4 | Decide 401 or 403: no token; customer token on an admin endpoint; expired token. |
| JNR-036-EX06 | 5 | Write tests for `DELETE /api/products/1` as anonymous, customer, and admin. |
| JNR-036-EX07 | 1, 2 | Turn on security debug logging and find which rule matched a rejected request. |

## Solutions
- **EX01** Request → security filters (auth, authorization, exception translation) → `DispatcherServlet` → controller; the 401 comes from the entry point inside the filter chain, before the controller.
- **EX02** See the `authorizeHttpRequests` example: `GET` permitAll, `POST`/`DELETE` `hasRole("ADMIN")`, then `anyRequest().authenticated()`.
- **EX03** The first matching rule wins, so `permitAll` makes the admin rule unreachable. Put specific rules first, `anyRequest()` last and never `permitAll`.
- **EX04** `findByEmail(...).orElseThrow(UsernameNotFoundException::new)` and build a `User` with the stored hash and role.
- **EX05** 401; 403; 401.
- **EX06** `status().isUnauthorized()` anonymous; `@WithMockUser(roles="CUSTOMER")` expects `isForbidden()`; `@WithMockUser(roles="ADMIN")` expects `isNoContent()` (or the endpoint's success status).
- **EX07** The debug log lines name the matched request matcher and the authorization decision.
