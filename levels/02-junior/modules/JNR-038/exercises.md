# JNR-038 · Sessions and tokens — Exercises and lab

## Lab
### JNR-038-LAB1 · Token auth for Shop
**Outcomes:** 1–4 · **Time:** ~3 h
Issue short-lived signed JWTs at login and secure the API as a resource server that validates them.
**Acceptance:** tampered, expired, and wrong-audience tokens are rejected by tests.

## Exercises (assessment: token-validation exercise)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-038-EX01 | 1 | Write the `Set-Cookie` header for a session cookie with all three secure attributes and explain each. |
| JNR-038-EX02 | 2 | Decode a given JWT by hand (Base64URL) and name header, claims, and signature. |
| JNR-038-EX03 | 2 | Explain why a JWT payload cannot hold a credit card number. |
| JNR-038-EX04 | 3 | List the checks a server must make on an incoming JWT. |
| JNR-038-EX05 | 3 | Given five tokens (bad signature, expired, wrong issuer, wrong audience, `alg: none`), say which are rejected and why. |
| JNR-038-EX06 | 4 | Compare sessions and tokens in a table covering revocation, scaling, and lifetime. |
| JNR-038-EX07 | 4 | Propose lifetimes for access and refresh tokens in Shop and justify them. |

## Solutions
- **EX01** `Set-Cookie: SESSION=...; HttpOnly; Secure; SameSite=Lax`. HttpOnly hides it from JavaScript; Secure sends it only over HTTPS; SameSite limits cross-site sending.
- **EX02** `header.payload.signature`; the first two parts decode to JSON; the signature is binary and cannot be read.
- **EX03** The payload is only encoded; anyone holding the token can read it.
- **EX04** Signature with the expected key, algorithm, issuer, audience, expiry (and not-before), then authorities.
- **EX05** All five are rejected, each failing one check: signature, `exp`, `iss`, `aud`, and unsigned token.
- **EX06** Sessions: server state, easy instant revocation, need shared store. Tokens: stateless, scale easily, revocation hard, rely on short expiry.
- **EX07** For example access 10 to 15 minutes, refresh a few days with rotation and server-side revocation; shorter access limits damage from theft.
