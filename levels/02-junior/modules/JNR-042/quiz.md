# JNR-042 · Secure configuration — Quiz

Outcomes: O1 secrets · O2 HTTPS and headers · O3 Actuator · O4 dependency scanning · O5 secure logging.

**Q01 (O1)** Production secrets should come from: A. The git repository B. Environment variables or a secret store C. The README D. A public file
**Q02 (O1)** A key was committed and then deleted. You should: A. Do nothing B. Rotate the key C. Rename the file D. Make the repo private only
**Q03 (O2)** HSTS tells browsers to: A. Cache images B. Always use HTTPS for the site C. Block cookies D. Compress responses
**Q04 (O2)** `X-Content-Type-Options: nosniff` stops: A. Slow queries B. Browsers guessing the content type C. CSRF tokens D. Redirects
**Q05 (O3)** Which Actuator endpoint is safe to expose publicly? A. `env` B. `heapdump` C. `shutdown` D. `health` (with limited details)
**Q06 (O3)** Exposing all Actuator endpoints in production is: A. Recommended B. Risky C. Required D. Faster
**Q07 (O4)** A dependency scanner reports: A. Slow methods B. Known vulnerabilities in libraries C. Style problems D. Unused classes
**Q08 (O4)** Dependabot mainly: A. Opens update pull requests and alerts B. Deploys the app C. Writes tests D. Hashes passwords
**Q09 (O5)** Which must never be logged? A. Request path B. Status code C. Passwords and tokens D. Response time
**Q10 (O5)** Error responses to clients should be: A. Detailed with stack traces B. Generic, with details kept in logs C. Empty D. HTML

## Answers
Q01 B · Q02 B · Q03 B · Q04 B · Q05 D · Q06 B · Q07 B · Q08 A · Q09 C · Q10 B

## Practical part
Eight exercises `JNR-042-EX01` to `EX08` plus the lab; the hardening checklist review (EX08) is the assessment. Pass: at least seven exercises correct, `/actuator/env` not reachable, and no secrets in code or logs.
