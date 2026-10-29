# JNR-041 · Common vulnerabilities — Lecture scripts

**Video:** 65 min · **Analogy used throughout:** a locksmith's tour of a house: the same few weak spots (windows, spare keys, unlocked doors) appear in almost every building.
Format: **Goal** · **Key points** · **Show** · **Check**.

Note: verify the current OWASP Top 10 edition and category names before recording.

---

## JNR-041-L01 · The OWASP Top 10 tour (12 min)
**Goal:** know the main risk categories and a backend example for each.

**Key points**
- OWASP (a non-profit) publishes a Top 10 list of the most serious web application risks, updated every few years.
- Typical categories: broken access control, cryptographic failures, injection, insecure design, security misconfiguration, vulnerable components, authentication failures, integrity failures, logging and monitoring failures, SSRF. Names and order change by edition, so verify.
- Broken access control is at or near the top: for example an IDOR.
- OWASP also has an API Security Top 10 that fits our work well.
- Use the list as a checklist for code reviews.

**Show:** a table: category / Shop example / control.

**Check:** Which category does "customer A reads customer B's order" belong to? *(Broken access control.)*

---

## JNR-041-L02 · Injection beyond SQL (10 min)
**Goal:** stop untrusted input from being run as code or queries.

**Key points**
- Injection: input is glued into a command so that data becomes code.
- SQL and JPQL: never concatenate input into a query; use parameters (`:name`, `?`).
- Other targets: OS commands, LDAP, expression languages, log lines (log injection with newlines).
- Validation helps, but parameterization is the real fix.
- Sorting column names and similar cannot be parameters: check them against an allow-list.

**Show**
```java
// Vulnerable
em.createQuery("select p from Product p where p.name = '" + name + "'");
// Safe
em.createQuery("select p from Product p where p.name = :name").setParameter("name", name);
```

**Check:** What stops SQL injection reliably? *(Parameterized queries.)*

---

## JNR-041-L03 · Mass assignment (8 min)
**Goal:** avoid letting clients set fields they should not.

**Key points**
- Mass assignment: binding a request body straight onto an entity lets clients set fields like `role`, `price`, or `enabled`.
- Attack: send `{"name":"Ana","role":"ADMIN"}` to the registration endpoint.
- Fix: bind requests to a separate DTO with only the allowed fields.
- Copy fields explicitly into the entity.
- Entities are for the database; DTOs are for the API.

**Show:** `RegisterRequest(email, password)` DTO versus an entity with a `role` field.

**Check:** Why not bind the request body to the entity? *(A client could set fields such as `role` that it should not control.)*

---

## JNR-041-L04 · XSS from the backend's view (8 min)
**Goal:** know what the backend does about cross-site scripting.

**Key points**
- XSS: an attacker's script runs in another user's browser.
- Stored XSS: the payload is saved (for example in a product review) and shown to others. Reflected XSS: it is echoed back from the request, such as in a link.
- A JSON API is mostly safe if it returns the right `Content-Type: application/json` and never HTML built from input.
- If you produce HTML or emails, encode output for its context.
- Add headers such as `X-Content-Type-Options: nosniff` and a Content-Security-Policy (more in JNR-042).

**Show:** review text `<script>alert(1)</script>` stored as text and shown encoded as `&lt;script&gt;...`.

**Check:** Which is saved and shown to many users: stored or reflected XSS? *(Stored.)*

---

## JNR-041-L05 · CSRF revisited (7 min)
**Goal:** decide when CSRF protection is needed.

**Key points**
- CSRF: a malicious site makes your browser send a request that carries your cookie.
- It matters when authentication is by cookie, which the browser adds automatically.
- A pure bearer-token API, where the token is sent in a header by code, is not affected in the same way.
- Cookie-based apps keep CSRF protection on (token or `SameSite` cookies).
- Do not disable CSRF without being able to say why.

**Show:** a table: cookie session vs bearer token: CSRF needed? yes / no.

**Check:** Why does a bearer-token API not need CSRF protection? *(Browsers do not attach the token automatically.)*

---

## JNR-041-L06 · SSRF (10 min)
**Goal:** protect features that fetch URLs.

**Key points**
- SSRF (server-side request forgery): the server is tricked into calling a URL the attacker picks, such as an internal service or the cloud metadata address.
- Typical features at risk: import from URL, webhooks, image fetch.
- Best fix: an allow-list of permitted hosts and schemes, not a deny-list.
- Resolve the host and block private and loopback addresses; do not follow redirects blindly.
- Set timeouts and size limits.

**Show:** an attack URL `http://169.254.169.254/latest/meta-data/` and the allow-list check that refuses it.

**Check:** Allow-list or deny-list for permitted hosts? *(Allow-list.)*

---

## JNR-041-L07 · Demo: exploiting and fixing mass assignment and SSRF (10 min)
**Goal:** exploit and fix two flaws locally. Prepares `JNR-041-LAB1`.

**Steps**
1. On the vulnerable branch, register with `"role":"ADMIN"` in the body and become an admin.
2. Fix with a `RegisterRequest` DTO; the extra field is now ignored.
3. Call the "import product image from URL" feature with an internal address; see data returned.
4. **Planned mistake:** a deny-list for `localhost` is bypassed with `127.0.0.1` or a redirect. Fix: an allow-list of hosts and resolved-address checks.
5. Add one regression test for each fix.
