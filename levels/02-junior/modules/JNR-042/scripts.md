# JNR-042 · Secure configuration — Lecture scripts

**Video:** 45 min · **Analogy used throughout:** closing up a shop at night: lock the doors, hide the spare key, cover the windows, and check the stock for recalls.
Format: **Goal** · **Key points** · **Show** · **Check**.

Note: verify Spring Boot, Actuator property names, and scanner plugin versions before recording.

---

## JNR-042-L01 · Secrets management basics (8 min)
**Goal:** keep secrets out of source control.

**Key points**
- Secrets: passwords, API keys, signing keys, database credentials.
- Never commit them, even to a private repo; git history keeps them forever.
- Read them from environment variables or a secret store (vault, cloud secret manager) at runtime: `${DB_PASSWORD}` in `application-prod.yml`.
- Use different secrets for dev and prod; rotate them; if one leaks, change it, deleting the commit is not enough.
- Scan for committed secrets (a pre-commit or CI scanner).

**Show**
```yaml
spring:
  datasource:
    password: ${DB_PASSWORD}
```

**Check:** A key was committed and removed in the next commit. Is it safe? *(No. It is in history; rotate it.)*

---

## JNR-042-L02 · HTTPS and security headers (8 min)
**Goal:** force encrypted transport and add protective headers.

**Key points**
- HTTPS encrypts traffic; usually terminated at a reverse proxy or load balancer.
- Redirect HTTP to HTTPS, and send HSTS (`Strict-Transport-Security`) so browsers insist on HTTPS.
- Spring Security adds several headers by default, such as `X-Content-Type-Options: nosniff` and cache controls.
- Add a `Content-Security-Policy` suited to your responses, and `Referrer-Policy` where relevant.
- Behind a proxy, configure forwarded headers so Spring knows the request was HTTPS (verify the property for the version).

**Show:** a response header list with `Strict-Transport-Security: max-age=31536000; includeSubDomains`.

**Check:** What does HSTS tell the browser? *(Always use HTTPS for this site.)*

---

## JNR-042-L03 · Locking down Actuator (6 min)
**Goal:** expose only the safe operational endpoints.

**Key points**
- Actuator exposes health, metrics, environment, and more; some endpoints reveal secrets or allow actions.
- Expose only what is needed: `management.endpoints.web.exposure.include=health,info`.
- Never expose `env`, `heapdump`, `beans`, or `shutdown` publicly.
- Protect the rest with authentication and a role, or run them on a separate management port.
- Hide health details from anonymous callers.

**Show**
```yaml
management:
  endpoints.web.exposure.include: health,info
  endpoint.health.show-details: never
```

**Check:** Which endpoint can leak configuration values? *(`/actuator/env`.)*

---

## JNR-042-L04 · Vulnerable dependencies (8 min)
**Goal:** find and fix known-vulnerable libraries.

**Key points**
- Most of your running code is libraries; each can have known flaws (CVEs).
- Scanners compare your dependency list with vulnerability databases: OWASP Dependency-Check, or GitHub Dependabot alerts and update pull requests.
- Run the scan in the build and fail it above a chosen severity.
- Update regularly in small steps; the tests tell you if it broke.
- Triage every warning: fix, or record why it is not exploitable. Do not ignore forever.

**Show:** a CI step that runs the scanner and a Dependabot config file for Maven or Gradle (verify the syntax before recording).

**Check:** What should you do with a scanner warning? *(Fix it or document why it does not apply, with a review date.)*

---

## JNR-042-L05 · Secure logging checklist (5 min)
**Goal:** audit logs for sensitive data.

**Key points**
- Never log passwords, tokens, API keys, card numbers, or full personal data.
- Do not log full request bodies or `Authorization` headers.
- Keep error responses generic; put details in logs, not in responses.
- Strip newlines from logged user input to avoid log injection.
- Search logs after tests for secrets as a habit.

**Show:** a checklist of five lines with example grep patterns (`Bearer `, `password`).

**Check:** May you log the `Authorization` header? *(No. It contains the token.)*

---

## JNR-042-L06 · Demo: hardening the prod profile (10 min)
**Goal:** apply all controls in one profile. Prepares `JNR-042-LAB1`.

**Steps**
1. Create `application-prod.yml`; replace secrets with environment variables.
2. Restrict Actuator to `health,info`.
3. Add security headers and HSTS; set forwarded-header handling for the proxy.
4. Add the dependency scanner to the build and run it; read the report.
5. **Planned mistake:** leaving `management.endpoints.web.exposure.include=*` from development; `/actuator/env` shows config. Fix: restrict it and re-test.
6. Grep the logs for passwords and tokens.
