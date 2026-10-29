# MID-051 · Advanced API security — Exercises and lab

## Lab
### MID-051-LAB1 · Zero implicit trust
**Outcomes:** 1–4 · **Time:** ~2.5 h
Every Shop service validates tokens; `orders` calls `inventory` with its own client credentials; scopes restrict admin operations.
**Acceptance:** a direct call without a valid token fails at every service.

## Exercises (assessment: authorization design review)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-051-EX01 | 1 | Choose a flow for each: web storefront, mobile app, nightly report job, support tool acting for a customer. |
| MID-051-EX02 | 2 | Configure a service as a resource server with issuer and audience validation. |
| MID-051-EX03 | 2 | Write tests: expired token, wrong audience, missing token, tampered signature. |
| MID-051-EX04 | 3 | Design scopes and roles for `orders` and `inventory` and fill in the endpoint matrix. |
| MID-051-EX05 | 3 | Add an ownership check and a negative test for reading another customer's order. |
| MID-051-EX06 | 4 | Configure `orders` to obtain a client-credentials token for `inventory`; limit its scopes. |
| MID-051-EX07 | 1–4 | Review a given design (gateway-only validation, header-based identity, shared service account) and list fixes. |

## Solutions
- **EX01** Storefront and mobile: authorization code with PKCE; nightly job: client credentials; support tool acting for the customer: token exchange (or a delegated, audited flow).
- **EX02** `issuer-uri` plus a `JwtValidator` checking `aud`; verify the exact Spring Security version API before recording.
- **EX03** Expect 401 for missing, expired, tampered, and wrong audience tokens.
- **EX04** Example: `orders:read` customer; `orders:admin` support role; `inventory:write` only for `orders` client and admin.
- **EX05** Compare the order's owner with the token subject; return 404 or 403 for others; test with two users.
- **EX06** Register an `orders` client with the `inventory:read` scope only; use a client-credentials `WebClient` filter.
- **EX07** Validate tokens in every service, take identity from the token, one client per service with minimal scopes.
