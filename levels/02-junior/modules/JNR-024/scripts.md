# JNR-024 · API security fundamentals — Lecture scripts

**Video:** 55 min · **Analogy used throughout:** an office building: the front desk checks your ID (authentication), your badge decides which floors you may enter (authorization), and a sealed corridor (HTTPS) stops anyone listening on the way in.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## JNR-024-L01 · Who are you vs what may you do (8 min)
**Goal:** separate authentication from authorization.

**Key points**
- **Authentication** answers "who are you?" (login, token). Failing it gives `401`.
- **Authorization** answers "what may you do?" (roles, ownership). Failing it gives `403`.
- Authentication comes first; authorization uses its result.
- Example: a customer can read their own orders (allowed) but not another customer's (forbidden).
- Check authorization on the server for every request; never trust the client to hide buttons.

**Show**
| Situation | Status |
| --- | --- |
| No token | 401 |
| Valid token, wrong role | 403 |
| Valid token, allowed | 200 |

**Check:** Which status for a logged-in user who is not allowed? *(`403`.)*

---

## JNR-024-L02 · Sessions vs tokens (10 min)
**Goal:** compare the two common ways to stay logged in.

**Key points**
- **Session:** after login the server stores state and gives the client a session ID, usually in a cookie. Each request sends it back.
- **Token:** after login the server gives a signed token (for example a JWT) that the client sends in `Authorization: Bearer ...`. The server verifies it without stored state.
- Sessions are simple to revoke but need shared storage when you run several instances.
- Tokens scale easily across instances but are harder to revoke before they expire.
- Browser apps often use cookie sessions; mobile apps and APIs often use tokens. JNR-P5 implements them.

**Show**
```
Session: Cookie: JSESSIONID=abc123
Token:   Authorization: Bearer eyJhbGciOi...
```

**Check:** Which approach keeps state on the server? *(Sessions.)*

---

## JNR-024-L03 · HTTPS for APIs (7 min)
**Goal:** know what HTTPS protects.

**Key points**
- HTTPS is HTTP inside **TLS**, an encrypted channel.
- It protects against eavesdropping (passwords, tokens, data) and tampering on the network.
- It lets the client verify it talks to the real server, through a certificate.
- It does not stop bugs in your API or tell you who the user is.
- Production APIs must never run on plain HTTP; tokens and passwords would travel readable. Commonly TLS ends at a load balancer or reverse proxy.

**Show:** a sketch of a request through a public Wi-Fi: plain HTTP shows the token to everyone; HTTPS shows scrambled bytes.

**Check:** Does HTTPS make an API free of vulnerabilities? *(No; it only protects the connection.)*

---

## JNR-024-L04 · CORS demystified (10 min)
**Goal:** understand why browsers block some cross-origin calls.

**Key points**
- An **origin** is scheme + host + port. `http://localhost:3000` and `http://localhost:8080` are different origins.
- Browsers apply the **same-origin policy**: a page may not read responses from another origin unless that server allows it.
- **CORS** is how the server allows it, with headers such as `Access-Control-Allow-Origin`.
- For some requests the browser first sends a **preflight** `OPTIONS` request to ask permission.
- CORS is enforced by browsers only. It does not protect your server from `curl` or other programs.

**Show**
```java
registry.addMapping("/**")
        .allowedOrigins("https://shop.example.com")
        .allowedMethods("GET", "POST", "PUT", "DELETE");
```

**Check:** Does CORS stop a script on a server calling your API? *(No; only browsers enforce it.)*

---

## JNR-024-L05 · CSRF and when it applies (10 min)
**Goal:** know when cross-site request forgery matters.

**Key points**
- **CSRF:** a malicious site makes the user's browser send a request to your site, and the browser attaches the user's cookies automatically.
- It matters when authentication is carried by cookies that the browser sends by itself.
- Defenses: CSRF tokens, `SameSite` cookies, and checking the request origin.
- If your API uses an `Authorization` header token that scripts add explicitly, the browser does not add it on its own, so CSRF is not the same risk.
- CORS and CSRF are different: CORS controls which pages may read responses; CSRF defends state-changing requests that use cookies.

**Show**
| | CORS | CSRF |
| --- | --- | --- |
| Concern | Which origins may read responses | Forged actions using cookies |
| Applies | Browser calls across origins | Cookie-authenticated browsers |

**Check:** Why is a bearer-token API less exposed to CSRF? *(The browser does not attach the header automatically.)*

---

## JNR-024-L06 · Demo: watching CORS fail and fixing it (10 min)
**Goal:** see the browser error and fix it for one origin. Prepares JNR-024-LAB1.

**Steps**
1. Run Shop API on port 8080 and serve a small HTML page from another port (for example 3000) that calls `fetch("http://localhost:8080/products")`.
2. Open the browser console and read the CORS error; check in the network tab that the server still answered.
3. Configure CORS for exactly `http://localhost:3000` and restart.
4. **Planned mistake:** use `allowedOrigins("*")` together with credentials. Fix: list the explicit origin; the wildcard with credentials is not allowed and is unsafe.
5. Reload the page and see the call succeed; try from another origin (port 3001) and see it still fail.
