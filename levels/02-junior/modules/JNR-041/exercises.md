# JNR-041 · Common vulnerabilities — Exercises and lab

## Lab
### JNR-041-LAB1 · Vulnerable Shop
**Outcomes:** 1–4 · **Time:** ~2.5 h
On a deliberately vulnerable branch with six planted flaws, find each, exploit it locally, fix it, and add a regression test for it.
**Acceptance:** 5 of 6 found and fixed, each with a regression test.

## Exercises (assessment: the lab, graded on fixes and tests)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-041-EX01 | 1 | Name six OWASP Top 10 categories and give one Shop example for each. |
| JNR-041-EX02 | 2 | Exploit and fix a JPQL query built by string concatenation. |
| JNR-041-EX03 | 2 | Register with `"role":"ADMIN"`, then fix it with a DTO. |
| JNR-041-EX04 | 2 | Fix a broken-access-control bug where a customer can update another's profile. |
| JNR-041-EX05 | 3 | Explain stored vs reflected XSS and state two things a JSON backend does to reduce the risk. |
| JNR-041-EX06 | 4 | Explain SSRF with one example for an "import from URL" feature. |
| JNR-041-EX07 | 4 | Write an allow-list check for a URL-fetching feature and a test that rejects an internal address. |

## Solutions
- **EX01** For example: access control (IDOR), injection (JPQL concatenation), cryptographic failures (MD5 passwords), security misconfiguration (open Actuator), vulnerable components (old library), SSRF (URL import). Verify names against the current edition.
- **EX02** Attack `name=' or '1'='1`; fix with `:name` and `setParameter`, or a Spring Data derived query.
- **EX03** Use a `RegisterRequest(email, password)` record and set the role server-side to CUSTOMER.
- **EX04** Take the user from the principal and update only that user's record; return 404 for other ids.
- **EX05** Stored: payload saved and shown to others; reflected: echoed from the request. Backend: correct `Content-Type` and no unencoded HTML; encode output for HTML and set `nosniff`/CSP headers.
- **EX06** The attacker supplies `http://localhost:8080/actuator/env` or a cloud metadata address and the server fetches it for them.
- **EX07** Parse the URL, require `https`, check host is in an allow-list, resolve the address and reject loopback/private ranges; test with `http://127.0.0.1/`.
