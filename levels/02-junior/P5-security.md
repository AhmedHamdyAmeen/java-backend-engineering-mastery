# JNR-P5 — Authentication and Application Security

**Phase goal:** the learner secures a Spring API — authenticating users, authorizing every request including ownership checks, and avoiding the common vulnerabilities — and can explain each control they add.

**Running project:** *Shop API* gains registration, login, roles (customer, admin), and per-customer data isolation.

**Phase total:** ~8.3 h video · ~20 h practice · `version:` current Spring Security major

---

### JNR-035 · Security fundamentals
`n: 89` · **Video:** 50 min · **Practice:** 1.5 h

**Prerequisites:** JNR-024

**Learning outcomes** — the learner can:
1. Describe the CIA triad and common attacker goals against a web API.
2. Identify trust boundaries in a system diagram.
3. Apply least privilege and defense in depth to a concrete design.
4. List the assets, entry points, and likely threats for the Shop API.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-035-L01 | Thinking like an attacker | 8 |
| JNR-035-L02 | Confidentiality, integrity, availability | 8 |
| JNR-035-L03 | Trust boundaries | 10 |
| JNR-035-L04 | Least privilege and defense in depth | 8 |
| JNR-035-L05 | A first threat list | 6 |
| JNR-035-L06 | Demo: drawing Shop's trust boundaries | 10 |

**Lab** — `JNR-035-LAB1` *Shop threat list:* draw the Shop API's data flow with trust boundaries and list the top 10 threats with a planned control for each. Acceptance: becomes the capstone's "documented security controls" seed.

**Common mistakes:** security as a final checklist; trusting anything from the client.

**Assessment:** threat list review.

**Career relevance:** threat modeling (MID-052) and security reviews (SRC-018).

---

### JNR-036 · Spring Security
`n: 90` · **Video:** 84 min · **Practice:** 4 h

**Prerequisites:** JNR-011, JNR-035

**Learning outcomes** — the learner can:
1. Explain the servlet filter chain and where Spring Security sits in it.
2. Configure a `SecurityFilterChain` bean with request-matcher rules.
3. Load users from the database with a `UserDetailsService`.
4. Return correct 401 vs 403 responses with Problem Details bodies.
5. Test secured endpoints with security test support.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-036-L01 | Filters and the security filter chain | 12 |
| JNR-036-L02 | Configuring `SecurityFilterChain` | 12 |
| JNR-036-L03 | Users from the database | 10 |
| JNR-036-L04 | 401 vs 403 and error bodies | 8 |
| JNR-036-L05 | Testing security | 10 |
| JNR-036-L06 | Reading Spring Security's debug output | 8 |
| JNR-036-L07 | Demo: securing the Shop API endpoint by endpoint | 12 |
| JNR-036-L08 | Demo: testing the access matrix | 12 |

**Lab** — `JNR-036-LAB1` *Secure Shop:* public catalog reads; authenticated cart and orders; admin-only catalog writes. Acceptance: tests cover anonymous, customer, and admin access for every endpoint.

**Common mistakes:** `permitAll` on `/**` while debugging and forgetting it; deny rules ordered after broad allow rules.

**Assessment:** access-matrix test suite.

**Career relevance:** every secured Spring service.

---

### JNR-037 · Password security
`n: 91` · **Video:** 45 min · **Practice:** 2 h

**Prerequisites:** JNR-036

**Learning outcomes** — the learner can:
1. Explain why passwords are hashed (not encrypted) and why salts and slow algorithms matter.
2. Store passwords with `PasswordEncoder` (bcrypt or Argon2) and support future algorithm upgrades.
3. Implement registration with sensible password rules (length over complexity, breached-password check concept).
4. Implement rate limiting or lockout for failed logins and explain the denial-of-service trade-off.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-037-L01 | How passwords get stolen | 8 |
| JNR-037-L02 | Hashing, salting, and slow hashes | 10 |
| JNR-037-L03 | `PasswordEncoder` and upgrades | 7 |
| JNR-037-L04 | Brute force, lockout, and throttling | 10 |
| JNR-037-L05 | Demo: registration with password hashing and throttling | 10 |

**Lab** — `JNR-037-LAB1` *Registration:* register with hashed passwords; throttle after 5 failed logins per account and IP. Acceptance: no plaintext or reversible password anywhere, including logs.

**Common mistakes:** MD5/SHA-256 for passwords; revealing whether an email exists.

**Assessment:** review a flawed registration flow.

**Career relevance:** identity architecture (ARC-017).

---

### JNR-038 · Sessions and tokens
`n: 92` · **Video:** 74 min · **Practice:** 3 h

**Prerequisites:** JNR-024, JNR-036

**Learning outcomes** — the learner can:
1. Explain cookie-based sessions and secure cookie attributes (`HttpOnly`, `Secure`, `SameSite`).
2. Decode a JWT and explain header, claims, and signature.
3. Validate a JWT correctly (signature, algorithm, issuer, audience, expiry).
4. Compare stateful sessions and stateless tokens, including revocation and expiry trade-offs.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-038-L01 | Cookies and server sessions | 10 |
| JNR-038-L02 | Bearer tokens | 7 |
| JNR-038-L03 | Inside a JWT | 10 |
| JNR-038-L04 | Validating tokens correctly | 12 |
| JNR-038-L05 | Expiry, refresh, and revocation | 11 |
| JNR-038-L06 | Demo: issuing and validating JWTs | 12 |
| JNR-038-L07 | Demo: attacking token validation (tampering, expiry, audience) | 12 |

**Lab** — `JNR-038-LAB1` *Token auth for Shop:* issue short-lived signed JWTs at login; secure the API as a resource server validating them. Acceptance: tampered, expired, and wrong-audience tokens rejected by tests.

**Common mistakes:** secrets or personal data in JWT claims; accepting `alg: none`; tokens that never expire.

**Assessment:** token-validation exercise.

**Career relevance:** OAuth 2.0 (JNR-039, MID-051).

---

### JNR-039 · OAuth 2.0 and OIDC basics
`n: 93` · **Video:** 74 min · **Practice:** 2.5 h

**Prerequisites:** JNR-038

**Learning outcomes** — the learner can:
1. Name the OAuth 2.0 roles (resource owner, client, authorization server, resource server).
2. Explain the authorization code flow with PKCE and the client credentials flow, and when each applies.
3. Distinguish OAuth 2.0 (delegated API access) from OIDC (login, ID tokens).
4. Configure the Shop API as a resource server trusting an external authorization server.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-039-L01 | The problem OAuth solves | 8 |
| JNR-039-L02 | Roles and tokens | 8 |
| JNR-039-L03 | Authorization code + PKCE | 12 |
| JNR-039-L04 | Client credentials | 7 |
| JNR-039-L05 | OIDC: adding login | 8 |
| JNR-039-L06 | Spring as a resource server | 7 |
| JNR-039-L07 | Demo: Keycloak setup and the authorization code + PKCE flow | 12 |
| JNR-039-L08 | Demo: switching Shop to Keycloak-issued tokens | 12 |

**Lab** — `JNR-039-LAB1` *External identity:* run Keycloak locally, obtain tokens with Postman, and switch the Shop API to validate Keycloak-issued tokens, mapping realm roles to authorities. Acceptance: self-issued tokens from JNR-038 no longer accepted.

**Common mistakes:** the implicit or password grant in new systems; using ID tokens to call APIs.

**Assessment:** flow-selection scenarios.

**Career relevance:** advanced API security (MID-051) and identity federation (ARC-027).

---

### JNR-040 · Role-based authorization
`n: 94` · **Video:** 64 min · **Practice:** 2.5 h

**Prerequisites:** JNR-029, JNR-036

**Learning outcomes** — the learner can:
1. Model roles and authorities and apply RBAC at URL and method level (`@PreAuthorize`).
2. Enforce ownership checks so users can access only their own resources.
3. Explain insecure direct object references (IDOR) and test for them.
4. Decide where authorization logic belongs (filter, method, domain query).

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-040-L01 | Roles, authorities, permissions | 8 |
| JNR-040-L02 | Method security | 10 |
| JNR-040-L03 | Ownership checks | 12 |
| JNR-040-L04 | IDOR: the most common API bug | 10 |
| JNR-040-L05 | Demo: finding and fixing an IDOR | 12 |
| JNR-040-L06 | Demo: method security with ownership checks | 12 |

**Lab** — `JNR-040-LAB1` *My orders only:* customers see only their own carts and orders; admins see all. Acceptance: a test where customer A requests customer B's order receives 404 (no existence leak).

**Common mistakes:** checking roles but not ownership; trusting a `customerId` from the request body.

**Assessment:** find IDOR bugs in a provided API.

**Career relevance:** broken access control is the top OWASP risk; authorization design in MID-051.

---

### JNR-041 · Common vulnerabilities
`n: 95` · **Video:** 65 min · **Practice:** 2.5 h

**Prerequisites:** JNR-025, JNR-035

**Learning outcomes** — the learner can:
1. Explain the current OWASP Top 10 categories with a backend example of each.
2. Demonstrate and fix SQL/JPQL injection, broken access control, and mass assignment.
3. Explain stored vs reflected XSS and the backend's role (output encoding, content types).
4. Explain SSRF and protect a URL-fetching feature with an allow-list.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-041-L01 | The OWASP Top 10 tour | 12 |
| JNR-041-L02 | Injection beyond SQL | 10 |
| JNR-041-L03 | Mass assignment | 8 |
| JNR-041-L04 | XSS from the backend's view | 8 |
| JNR-041-L05 | CSRF revisited | 7 |
| JNR-041-L06 | SSRF | 10 |
| JNR-041-L07 | Demo: exploiting and fixing mass assignment and SSRF | 10 |

**Lab** — `JNR-041-LAB1` *Vulnerable Shop:* a deliberately vulnerable branch with six planted flaws; find, exploit locally, fix, and add a regression test for each. Acceptance: 5 of 6 found and fixed.

**Common mistakes:** binding request bodies directly to entities; fetching user-provided URLs unrestricted.

**Assessment:** the lab, graded on fixes and tests.

**Career relevance:** OWASP API Security (MID-052).

---

### JNR-042 · Secure configuration
`n: 96` · **Video:** 45 min · **Practice:** 2 h

**Prerequisites:** JNR-006, JNR-012

**Learning outcomes** — the learner can:
1. Supply secrets through environment variables or a secret store, never source control.
2. Enforce HTTPS-only behavior (redirects, HSTS) and secure headers.
3. Restrict Actuator endpoints in production.
4. Scan dependencies for known vulnerabilities and keep them updated (Dependabot or OWASP Dependency-Check).
5. Audit logs for sensitive data.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-042-L01 | Secrets management basics | 8 |
| JNR-042-L02 | HTTPS and security headers | 8 |
| JNR-042-L03 | Locking down Actuator | 6 |
| JNR-042-L04 | Vulnerable dependencies | 8 |
| JNR-042-L05 | Secure logging checklist | 5 |
| JNR-042-L06 | Demo: hardening the prod profile | 10 |

**Lab** — `JNR-042-LAB1` *Production hardening:* a `prod` profile with secrets from environment, restricted Actuator, security headers, and dependency scanning in the build. Acceptance: completes the capstone's security controls document.

**Common mistakes:** exposing `/actuator/env`; ignoring scanner warnings forever.

**Assessment:** hardening checklist review.

**Career relevance:** dependency security (MID-053) and secrets (MID-054).
