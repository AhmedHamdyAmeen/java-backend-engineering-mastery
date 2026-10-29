# SRB-016 · Security architecture — Exercises and lab

## Lab
### SRB-016-LAB1 · Merged trust model
**Outcomes:** 1–4 · **Time:** ~3.5 h
1. Define identity authorities and lifecycles for users, services, and partners across Shop and FulfillCo.
2. Design service-to-service authorization with workload identity, scoped tokens or mTLS, and a policy layer.
3. Plan least-privilege access to data across the four teams, and a migration away from network-based trust.
4. Present the architecture to a role-played security architect and record findings.
**Acceptance:** no network-location-based trust remains; reviewed by a role-played security architect.

## Exercises (assessment: architecture review)
| ID | Outcome | Task |
| --- | --- | --- |
| SRB-016-EX01 | 1 | Case: Shop and FulfillCo each have a user store. Design identity boundaries and federation for staff, services, and partners. |
| SRB-016-EX02 | 1 | Write the identity table (type, authority, credential, lifecycle, revocation) for the merged platform. |
| SRB-016-EX03 | 2 | Review a design that trusts the internal subnet; list five zero-trust changes in priority order. |
| SRB-016-EX04 | 3 | Draft the authorization matrix for three FulfillCo services against Shop order events and the Shop API. |
| SRB-016-EX05 | 3 | Choose between mTLS identities and scoped tokens for event consumers, with reasons and failure behavior. |
| SRB-016-EX06 | 3 | Write five policy test cases (three allow, two deny) for the order-event reader. |
| SRB-016-EX07 | 4 | Plan data access so that the returns team sees only what it needs; include audit and review cadence. |

## Solutions
- **EX01** Federate staff login through one authority; use a workload identity system for services; onboard partners with scoped credentials and separate tenants. Do not merge user stores before federation is proven.
- **EX02** Rows per type with authority, short-lived credentials for services, lifecycle events, and a named revoker.
- **EX03** Order: protect highest-value paths first, add authentication in report-only mode, issue workload identities, enforce, drop subnet allow rules, add audit and monitoring.
- **EX04** Matrix of caller | endpoint or topic | action; least privilege such as read order events but not payment fields.
- **EX05** mTLS gives mutual authentication and encryption; scoped tokens add per-request scope; many designs combine them. Decide fail-closed behavior and certificate or token rotation.
- **EX06** Allow: right identity and topic. Allow: read-only action. Allow: right audience. Deny: unknown identity. Deny: right identity wrong topic.
- **EX07** Views or scoped APIs instead of shared database access, separate credentials per team, periodic access review, audit logs.
- Outcome 2 is also covered by the lab's migration away from network trust and Q03.

**Workplace evidence:** a security architecture change you led across services.
