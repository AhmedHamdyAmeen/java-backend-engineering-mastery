# JNR-041 · Common vulnerabilities — Quiz

Outcomes: O1 OWASP Top 10 · O2 injection, access control, mass assignment · O3 XSS · O4 SSRF.

**Q01 (O1)** OWASP publishes: A. A Java compiler B. A list of top web application risks C. A database D. A cloud provider
**Q02 (O1)** An IDOR belongs to: A. Broken access control B. Injection C. Logging failures D. SSRF
**Q03 (O2)** The reliable defense against SQL injection is: A. Parameterized queries B. Hiding the table names C. Longer passwords D. Lowercasing input
**Q04 (O2)** Sort-column names that cannot be parameters should be: A. Trusted B. Concatenated C. Checked against an allow-list D. Hashed
**Q05 (O2)** Mass assignment happens when: A. A request is bound directly to an entity B. A query is slow C. A token expires D. A cookie is missing
**Q06 (O2)** The best fix for mass assignment is: A. Trusting the client B. A request DTO with allowed fields only C. A longer URL D. More roles
**Q07 (O3)** Stored XSS means the payload is: A. Never saved B. Saved and shown to other users C. Only in the URL D. Only in logs
**Q08 (O3)** For a JSON API, XSS risk is reduced by: A. Returning HTML built from input B. Correct content type and never echoing unencoded HTML C. Disabling HTTPS D. Longer tokens
**Q09 (O4)** SSRF means the: A. Browser attacks another browser B. Server is tricked into calling an attacker-chosen URL C. Database copies a table D. Client forges a cookie
**Q10 (O4)** The best protection for a URL-fetching feature: A. A deny-list of `localhost` B. An allow-list of hosts and schemes C. Following all redirects D. No timeout

## Answers
Q01 B · Q02 A · Q03 A · Q04 C · Q05 A · Q06 B · Q07 B · Q08 B · Q09 B · Q10 B

## Practical part
The lab is the assessment: six planted flaws, each found, exploited, fixed, and covered by a regression test. Pass: 5 of 6 fixed with tests, plus quiz 8 of 10.
