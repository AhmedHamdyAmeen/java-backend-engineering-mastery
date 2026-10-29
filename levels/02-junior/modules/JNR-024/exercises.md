# JNR-024 · API security fundamentals — Exercises and lab

## Lab
### JNR-024-LAB1 · CORS experiment
**Outcomes:** 3, 4 (with 1 and 2 covered by the quiz and exercises) · **Time:** ~1.5 h
Serve a small HTML page from another origin (different port). From it, call the Shop API with `fetch` and observe the browser's CORS error. Then configure CORS for exactly one allowed origin and retry from the allowed and a different origin.

**Acceptance:** only the allowed origin succeeds.

## Exercises (assessment: quiz)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-024-EX01 | 1 | Decide `401` or `403` for five scenarios (no token, expired token, wrong role, other user's order, admin). |
| JNR-024-EX02 | 2 | Write a table comparing sessions and tokens: where state lives, revocation, scaling. |
| JNR-024-EX03 | 3 | Explain in four sentences what HTTPS protects and what it does not. |
| JNR-024-EX04 | 4 | List which of these are different origins from `https://shop.com`: `https://shop.com:8443`, `http://shop.com`, `https://api.shop.com`, `https://shop.com/cart`. |
| JNR-024-EX05 | 4 | Explain why `curl` ignores CORS and what that means for server protection. |
| JNR-024-EX06 | 4 | Describe a CSRF attack on a cookie-authenticated API and one defense; state why a bearer-header API is less exposed. |

## Solutions
- **EX01** No token: 401. Expired token: 401. Wrong role: 403. Other user's order: 403 (or 404 to hide existence). Admin: allowed.
- **EX02** Sessions: state on server, easy revoke, needs shared store to scale. Tokens: state in the token, hard to revoke early, scale easily.
- **EX03** Protects against eavesdropping and tampering, and verifies server identity; does not authenticate users or fix application bugs.
- **EX04** Different: `:8443` (port), `http://` (scheme), `api.shop.com` (host). Same origin: `https://shop.com/cart`.
- **EX05** CORS is a browser rule; other clients do not enforce it, so the server must still do authentication and authorization.
- **EX06** An evil page submits a form to `/orders`; the browser attaches the session cookie. Defense: CSRF token or `SameSite` cookie. A script-set bearer header is not attached automatically.

**Outcomes 1 to 3** are checked by the exercises and quiz Q01 to Q07; the lab covers outcome 4 in practice.
