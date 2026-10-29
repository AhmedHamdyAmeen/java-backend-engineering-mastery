# ARC-025 · API management — Exercises and lab

## Lab
### ARC-025-LAB1 · Partner API program
**Outcomes:** 1–4 · **Time:** ~3 h
1. List the consumers (mobile app, marketplace partners, internal systems) and what each needs.
2. Define three APIs as products with owner, SLA, and support.
3. Decide which API management capabilities Larkspur needs now and later.
4. Design consumer tiers, quotas, and key handling.
5. Design onboarding through the developer portal and the versioning and deprecation policy.
6. Review with a role-played partner manager and security lead.
**Acceptance:** reviewed by a role-played partner manager and security lead.

## Exercises (case-based; five exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| ARC-025-EX01 | 1 | Decide whether a solution with one internal consumer needs an API management platform; write the reasons. |
| ARC-025-EX02 | 2 | Write six rules for a style guide and a five-step review flow. |
| ARC-025-EX03 | 3 | Create a tier table for internal, partner, and public consumers with quotas and data scope. |
| ARC-025-EX04 | 4 | Write the product card for the Stock availability API. |
| ARC-025-EX05 | 2, 3 | A partner's integration breaks after you remove a field. Write the incident summary and the policy that would have prevented it. |

## Solutions
- **EX01** Probably no: few consumers, trusted network, low risk; use a simple gateway for authentication and logging and revisit when partners arrive.
- **EX02** Consistent naming, standard error format, pagination, auth defaults, idempotency for writes, versioning; flow: design, lint, peer review, security check, publish.
- **EX03** Internal: service identity, high limits; partner: contracted quota, key and OAuth client, selected fields; public: low limit, read-only, no personal data.
- **EX04** Owner team, consumers, SLA and availability, rate limits, support channel, version, deprecation notice period.
- **EX05** Removal is a breaking change; policy: additive changes only within a version, notice period, deprecation headers, consumer notification via portal, contract tests with major consumers.

All outcomes are also covered by the lab review.

**Workplace evidence:** an API program or governance process you designed or improved.
