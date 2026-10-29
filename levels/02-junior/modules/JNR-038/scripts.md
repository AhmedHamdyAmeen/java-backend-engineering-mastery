# JNR-038 · Sessions and tokens — Lecture scripts

**Video:** 74 min · **Analogy used throughout:** a cinema: a ticket stub kept at the desk (session) versus a signed ticket you carry (token).
Format: **Goal** · **Key points** · **Show** · **Check**.

Note: verify the Spring Security and JWT library versions before recording.

---

## JNR-038-L01 · Cookies and server sessions (10 min)
**Goal:** explain how a browser stays logged in with a session cookie.

**Key points**
- HTTP forgets you between requests; a session remembers you on the server.
- After login the server stores the session and sends a cookie holding only a random session ID.
- The browser sends the cookie automatically with each request.
- `HttpOnly`: JavaScript cannot read the cookie. `Secure`: sent only over HTTPS. `SameSite`: limits sending on cross-site requests.
- Server sessions are easy to revoke (delete the session) but need shared storage when you run many servers.

**Show:** a response header: `Set-Cookie: SESSION=abc; HttpOnly; Secure; SameSite=Lax`.

**Check:** Which attribute stops JavaScript from reading the cookie? *(`HttpOnly`.)*

---

## JNR-038-L02 · Bearer tokens (7 min)
**Goal:** explain token-based API authentication.

**Key points**
- Mobile apps and other services often send a token in a header: `Authorization: Bearer <token>`.
- "Bearer" means whoever holds the token can use it, like cash. Protect it in transit (HTTPS) and at rest.
- No cookie is sent automatically, which also reduces CSRF risk for pure token APIs.
- The server must still check the token on every request.

**Show:** `curl -H "Authorization: Bearer eyJ..." https://shop.example/api/orders`.

**Check:** Why is HTTPS essential for bearer tokens? *(Anyone who copies the token can use it.)*

---

## JNR-038-L03 · Inside a JWT (10 min)
**Goal:** read a JWT and name its three parts.

**Key points**
- A JWT (JSON Web Token) is three Base64URL parts joined by dots: header.payload.signature.
- Header: algorithm and type (`alg`, `typ`). Payload: claims such as `sub` (subject), `iss` (issuer), `aud` (audience), `exp` (expiry), `iat`.
- The signature proves the header and payload were not changed, by a key.
- The payload is encoded, not encrypted: anyone can read it. Never put secrets or personal data in claims.
- Keep tokens small.

**Show:** a decoded token:
```json
{"alg":"HS256","typ":"JWT"}
{"sub":"42","iss":"shop","aud":"shop-api","exp":1893456000,"roles":["CUSTOMER"]}
```

**Check:** Is a JWT payload secret? *(No. It is only encoded, so anyone can read it.)*

---

## JNR-038-L04 · Validating tokens correctly (12 min)
**Goal:** list every check a server must make on a token.

**Key points**
- Verify the signature with the expected key and the expected algorithm; never trust the token's own `alg`, and reject `alg: none`.
- Check `iss` equals your issuer and `aud` includes your API.
- Check `exp` (and `nbf` if used), allowing only a tiny clock skew.
- Use a well-tested library (Spring's resource server uses Nimbus); never hand-write validation.
- Keep signing keys secret (shared secret) or the private key private (asymmetric).

**Show:** a checklist: signature, algorithm, issuer, audience, expiry, then roles.

**Check:** Why reject `alg: none`? *(It means "unsigned", so anyone could forge a token.)*

---

## JNR-038-L05 · Expiry, refresh, and revocation (11 min)
**Goal:** compare sessions and tokens on lifetime and revocation.

**Key points**
- Stateless tokens need no server storage, but cannot be taken back before they expire.
- So use short-lived access tokens (minutes) and, when needed, a refresh token to get new ones.
- A refresh token is long-lived, so store it carefully and make it revocable (kept server side) and rotate it on use.
- Sessions revoke instantly but need server state; tokens scale easily but revocation is harder.
- Logout on a stateless token usually means "forget it on the client" plus a short lifetime.

**Show:** a comparison table: sessions vs tokens: state, revocation, scaling, typical lifetime.

**Check:** Why make access tokens short-lived? *(A stolen token stops working soon, since it cannot be revoked easily.)*

---

## JNR-038-L06 · Demo: issuing and validating JWTs (12 min)
**Goal:** issue and validate signed JWTs in Shop. Prepares `JNR-038-LAB1`.

**Steps**
1. Add a `POST /api/auth/login` that checks credentials and builds a JWT with `sub`, `iss`, `aud`, short `exp`.
2. Sign it with a key read from configuration (not from source code).
3. Configure the API as a resource server: `oauth2ResourceServer(o -> o.jwt(...))` with a `JwtDecoder` that checks issuer and audience.
4. Call the API with the token and see `200`.
5. **Planned mistake:** putting the user's email and phone in the claims. Fix: keep only the ID and roles.
6. Decode the token on a debugger site and point out the readable payload.

---

## JNR-038-L07 · Demo: attacking token validation (tampering, expiry, audience) (12 min)
**Goal:** prove validation works by trying to break it. Prepares `JNR-038-LAB1`.

**Steps**
1. Change a claim (`roles` to `ADMIN`) without re-signing: the API returns 401.
2. Wait for or set an expired token: 401.
3. Issue a token with the wrong `aud`: 401.
4. Try an unsigned `alg: none` token: 401.
5. **Planned mistake:** a decoder configured without an audience check accepts the wrong-audience token. Fix: add an audience validator and re-run.
6. Turn each attack into an automated test.
