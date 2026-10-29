# SRB-016 · Security architecture — Quiz

Outcomes: O1 identity boundaries · O2 zero trust · O3 service-to-service authorization · O4 least-privilege data access.

**Q01 (O1)** After merging two organizations, the safest first step for identity is: A. Merge user databases immediately B. Share admin passwords C. Define authorities per identity type and use federation D. Ignore the difference
**Q02 (O1)** Authentication answers: A. What the caller may do B. Who the caller is C. How fast the call is D. Where the data lives
**Q03 (O2)** "Inside the VPC means trusted" violates: A. Caching rules B. Zero-trust principles C. Naming conventions D. Tagging policy
**Q04 (O2)** "Assume breach" leads to: A. Limiting blast radius and adding detection B. Stopping deployments C. Relying on a firewall D. Longer passwords only
**Q05 (O3)** mTLS provides: A. Business rule checks B. Rate limiting C. Mutual authentication and encryption of the connection D. Data retention
**Q06 (O3)** Why give each service its own identity? A. Faster deploys B. Fewer tokens C. Smaller images D. You can attribute actions and revoke one without affecting others
**Q07 (O3)** Authorization for an event topic is best decided: A. By the caller B. At the callee or policy layer using the caller's identity C. By the network D. By DNS
**Q08 (O3)** A good policy test suite contains: A. Only allow cases B. Only deny cases C. Allow and deny cases D. No tests
**Q09 (O4)** Least privilege for the returns team means: A. Access to the whole database B. Read-only everything C. A shared credential D. Access to only the data and actions the team needs
**Q10 (O2)** Moving to identity checks on an internal API safely starts with: A. Enforcing immediately B. Report-only mode to discover unknown callers C. Deleting the old rule D. Disabling logs

## Answers
Q01 C · Q02 B · Q03 B · Q04 A · Q05 C · Q06 D · Q07 B · Q08 C · Q09 D · Q10 B

## Practical part
Present the merged trust model to a role-played security architect (SRB-016 assessment) and complete `SRB-016-LAB1`. Pass: at least 8/10 on the quiz, an architecture with no network-location-based trust remaining, and a recorded review.
