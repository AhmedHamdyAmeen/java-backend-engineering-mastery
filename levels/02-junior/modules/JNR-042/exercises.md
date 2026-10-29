# JNR-042 · Secure configuration — Exercises and lab

## Lab
### JNR-042-LAB1 · Production hardening
**Outcomes:** 1–5 · **Time:** ~2 h
Create a `prod` profile with secrets from the environment, restricted Actuator, security headers, and dependency scanning in the build.
**Acceptance:** completes the capstone's security controls document.

## Exercises (assessment: hardening checklist review)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-042-EX01 | 1 | Move a hard-coded database password and JWT key out of `application.yml` into environment variables. |
| JNR-042-EX02 | 1 | A secret was committed. List the steps to respond. |
| JNR-042-EX03 | 2 | Check response headers with curl and list which security headers are present or missing. |
| JNR-042-EX04 | 2 | Explain HSTS and when it is safe to enable. |
| JNR-042-EX05 | 3 | Configure Actuator so only `health` and `info` are exposed and verify `/actuator/env` returns 404. |
| JNR-042-EX06 | 4 | Add a dependency scanner to the build and triage one finding. |
| JNR-042-EX07 | 5 | Audit sample logs and list every sensitive item found, with the fix. |
| JNR-042-EX08 | 1-5 | Review a prod configuration against a hardening checklist. |

## Solutions
- **EX01** `password: ${DB_PASSWORD}` and `jwt.key: ${JWT_SIGNING_KEY}`; set values in the environment or secret store; keep a sample file with placeholders only.
- **EX02** Rotate the secret first, then remove it from the code; consider history cleanup; check access logs for misuse; add a secret scanner.
- **EX03** `curl -I https://...`; check `X-Content-Type-Options`, `Strict-Transport-Security`, `Content-Security-Policy`, cache and referrer headers; add what is missing.
- **EX04** HSTS makes browsers use HTTPS only for a period; enable once HTTPS works for the whole domain, starting with a short `max-age`.
- **EX05** `management.endpoints.web.exposure.include=health,info`; `curl /actuator/env` returns 404 (or 401 when protected).
- **EX06** Add the scanner plugin or Dependabot; for a finding, update the library, or record the reason and a review date.
- **EX07** Typical findings: password in a request body log, `Authorization` header, personal data in debug lines; remove, mask, or lower the log level.
- **EX08** Cover secrets, HTTPS/headers, Actuator, dependencies, and logging, giving a pass or fix note for each.
