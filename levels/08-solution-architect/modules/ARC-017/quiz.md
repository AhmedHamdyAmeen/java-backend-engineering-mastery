# ARC-017 · Identity architecture — Quiz

Outcomes: O1 workforce identity · O2 customer identity · O3 protocol choice · O4 cloud IAM.

**Q01 (O1)** SSO means: A. One password written down B. Employees sign in once to an identity provider and reach many apps C. Shared logins per team D. No MFA
**Q02 (O1)** Why federate with the corporate directory? A. To duplicate accounts B. To remove MFA C. To reuse existing identities and joiner-leaver processes D. To avoid roles
**Q03 (O1)** A shared account for a whole store is: A. Acceptable for speed B. Required by SSO C. Good for audit D. Bad practice because actions cannot be attributed
**Q04 (O2)** Which weak point do attackers often target in customer identity? A. Account recovery B. Logo C. Page title D. Color scheme
**Q05 (O2)** For customer login, the recommended starting point is: A. Build in-house B. Use a managed CIAM service C. No authentication D. Shared passwords
**Q06 (O3)** Which protocol adds sign-in on top of OAuth 2.0? A. SAML B. Kerberos only C. OpenID Connect D. Basic auth
**Q07 (O3)** A mobile app should use: A. Implicit flow with a secret in the app B. Authorization code flow with PKCE C. Username and password in the app D. API keys in code
**Q08 (O3)** A SaaS tool that only supports SAML gets: A. SAML B. OIDC regardless C. No SSO D. A shared account
**Q09 (O4)** For workloads, prefer: A. Long-lived access keys B. Keys in config files C. Platform roles with short-lived credentials D. Shared admin keys
**Q10 (O4)** Break-glass access should be: A. Widely shared B. Never defined C. Used daily D. Few, protected, and alert on use

## Answers
Q01 B · Q02 C · Q03 D · Q04 A · Q05 B · Q06 C · Q07 B · Q08 A · Q09 C · Q10 D

## Practical part
Identity design review of the `ARC-017-LAB1` design plus exercises `ARC-017-EX01` to `EX06`. Pass: quiz at least 8/10, at least five of six exercises correct, protocol choice justified per integration, no shared accounts, and break-glass access defined.
