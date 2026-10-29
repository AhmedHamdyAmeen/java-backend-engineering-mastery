# ARC-017 · Identity architecture — Exercises and lab

## Lab
### ARC-017-LAB1 · Larkspur identity design
**Outcomes:** 1–4 · **Time:** ~4 h
1. Identify the identity populations and applications: store and head-office staff, customers, partners and suppliers, workloads.
2. Design workforce SSO, federation, and MFA, including store staff.
3. Design customer identity for web and mobile, including recovery and privacy.
4. Choose a protocol (SAML, OAuth 2.0, OIDC) per integration with the reason.
5. Define cloud IAM roles for people and workloads and break-glass access.
**Acceptance:** protocol choice justified per integration; no shared accounts; break-glass access defined.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| ARC-017-EX01 | 1 | Design joiner-mover-leaver for 120 stores with high staff turnover. |
| ARC-017-EX02 | 1 | Choose MFA approach for cashiers on shared tills and for head-office administrators. |
| ARC-017-EX03 | 2 | List what the customer identity service must provide and which privacy rights it must support. |
| ARC-017-EX04 | 2 | The product owner wants a custom login page built in-house. Write the recommendation. |
| ARC-017-EX05 | 3 | Pick a protocol for: HR SaaS sign-in, the mobile app, a partner delivery-status API, a legacy intranet app that only supports SAML. |
| ARC-017-EX06 | 4 | An access key for the order service was found in a repository. Describe the remediation and the better design. |

## Solutions
- **EX01** HR system is the source: hire creates account and role by store; transfers change role/store automatically; termination disables access immediately; periodic access review.
- **EX02** Cashiers: badge or app-based second factor with short sessions and per-user sign-in; admins: phishing-resistant MFA (hardware key or passkey) plus just-in-time elevation.
- **EX03** Registration, login, social login, recovery, MFA option, consent management, data export and deletion, minimal data collection, audit of access to personal data.
- **EX04** Recommend a managed CIAM: lower security risk, faster delivery, built-in recovery and MFA; build only if requirements are unmet, which they are not.
- **EX05** HR SaaS: SAML (or OIDC if supported); mobile app: OIDC with authorization code and PKCE; partner API: OAuth 2.0 client credentials; legacy intranet: SAML.
- **EX06** Revoke and rotate the key now, search logs for use, remove from history; redesign with a workload role and short-lived credentials; add secret scanning to the pipeline.

**Workplace evidence:** an identity or SSO design you delivered.

---
Outcome coverage: all outcomes covered by exercises and the lab.
