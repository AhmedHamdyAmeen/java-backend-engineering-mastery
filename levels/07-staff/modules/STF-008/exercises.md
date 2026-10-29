# STF-008 · Security architecture strategy — Exercises and lab

## Lab
### STF-008-LAB1 · Secure by default
**Outcomes:** 1–4 · **Time:** ~2.5 h
1. Assess the threat landscape for Platform 2.0 and rank the top threats.
2. Draw organization-wide trust boundaries and an identity strategy for people, services, and partners.
3. Define five secure defaults built into the golden path, each tied to a class of audit findings.
4. Draft a multi-year joint roadmap with a role-played CISO.
5. Defend the strategy in review.
**Acceptance:** each default removes a class of findings rather than one finding.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| STF-008-EX01 | 1 | List the top five threats for a marketplace-enabled commerce group and map each to an architectural control. |
| STF-008-EX02 | 2 | Draw a trust-boundary sketch for public edge, services, payments, data, and a partner API; mark controls at each crossing. |
| STF-008-EX03 | 2 | Propose one identity approach for employees, services, and partners, with least-privilege rules. |
| STF-008-EX04 | 3 | Turn "teams commit secrets to repositories" into a platform default; describe enforcement and exception handling. |
| STF-008-EX05 | 3 | Given 40 findings in six classes, choose the three defaults with the biggest reduction and state the expected effect. |
| STF-008-EX06 | 4 | Write a one-page joint roadmap with the security team: roles, year-one goals, measures, and meeting cadence. |

## Solutions
- **EX01** Examples: account takeover (rate limits, MFA), payment fraud (isolated payment zone), injection (framework defaults), supply chain (signed artifacts), insider misuse (least privilege and audit).
- **EX02** Controls: edge firewall and authentication, mutual authentication between services, payment zone isolation, encrypted data zone with access logging, partner gateway with keys and limits.
- **EX03** Central identity provider; workload identities for services; scoped partner credentials; short-lived tokens; review access regularly.
- **EX04** Secrets manager in the template, pipeline secret scan that fails the build, logged exceptions with owner and expiry.
- **EX05** Pick by counts per class and ease; state findings removed per quarter as the target.
- **EX06** Security owns policy and monitoring; platform owns defaults; measures are recurring findings and time to patch; monthly meeting.

Outcome coverage: all four outcomes are covered by exercises and lab.

**Workplace evidence:** a secure default you introduced at organization level and the findings it eliminated.
