# JNR-039 · OAuth 2.0 and OIDC basics — Exercises and lab

## Lab
### JNR-039-LAB1 · External identity
**Outcomes:** 1–4 · **Time:** ~2.5 h
Run Keycloak locally, obtain tokens with Postman, and switch the Shop API to validate Keycloak-issued tokens, mapping realm roles to authorities.
**Acceptance:** self-issued tokens from JNR-038 are no longer accepted.

## Exercises (assessment: flow-selection scenarios)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-039-EX01 | 1 | Name the four OAuth roles in this setup: a user, the Shop web app, Keycloak, the Shop API. |
| JNR-039-EX02 | 2 | Choose the flow: (a) a single-page app where users log in; (b) a nightly job calling an internal API; (c) a mobile app. |
| JNR-039-EX03 | 2 | Explain in your own words what PKCE protects against. |
| JNR-039-EX04 | 3 | Fill in a table of access token vs ID token: purpose, audience, sent to the API or not. |
| JNR-039-EX05 | 3 | A team sends the ID token to the API as a bearer token. Explain the problem. |
| JNR-039-EX06 | 4 | Write the YAML and converter to map `realm_access.roles` to `ROLE_*` authorities. |
| JNR-039-EX07 | 2 | Say why the implicit and password grants should not be used in new systems. |

## Solutions
- **EX01** User: resource owner; Shop web app: client; Keycloak: authorization server; Shop API: resource server.
- **EX02** (a) authorization code + PKCE; (b) client credentials; (c) authorization code + PKCE.
- **EX03** A stolen authorization code cannot be exchanged for tokens without the original `code_verifier`.
- **EX04** Access token: authorizes API calls, audience is the API, sent to the API. ID token: tells the client who logged in, audience is the client, never sent to the API.
- **EX05** The ID token is meant for the client; its audience is wrong for the API, and it is not designed to authorize access.
- **EX06** Set `issuer-uri`; in a `JwtAuthenticationConverter` read the `realm_access` claim's `roles` list and map each to `new SimpleGrantedAuthority("ROLE_" + role.toUpperCase())`.
- **EX07** Implicit exposes tokens in the browser URL; password grant makes the client handle user passwords. Both are discouraged by current best-practice guidance (verify before recording).
