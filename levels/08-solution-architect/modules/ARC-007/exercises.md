# ARC-007 · Architecture principles — Exercises and lab

## Lab
### ARC-007-LAB1 · Larkspur principles
**Outcomes:** 1–4 · **Time:** ~2.5 h
1. Gather strategy and constraint inputs from the case.
2. Draft eight to ten principles, each with statement, rationale, and implications.
3. Review with role-played IT leadership; revise.
4. Apply each principle to one real Larkspur decision and record the result.
5. Record one principle conflict and its resolution, plus the exception process.
**Acceptance:** at least one principle changes a decision; one conflict resolved on record.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| ARC-007-EX01 | 1 | Rewrite three platitudes ("use best practices", "be scalable", "keep it simple") as testable principles with implications. |
| ARC-007-EX02 | 1 | Write one full principle (statement, rationale, implications) on interoperability for Larkspur. |
| ARC-007-EX03 | 2 | Use a standardization principle and an evolvability principle to evaluate two API options for carriers. |
| ARC-007-EX04 | 2 | Apply a security principle to a proposal to share the customer database directly with the CRM. |
| ARC-007-EX05 | 3 | Standardization says one event platform; store systems only support file transfer. Write the conflict record and decision. |
| ARC-007-EX06 | 4 | A team requests an exception to use a niche payment SDK. Write an assessment against the principles and a time-limited exception. |

## Solutions
- **EX01** Examples: "Customer data is changed only through its owning service"; "Every service has a stated load target and is tested at 2x"; "Remove a component or interface for each one added, unless a decision record says why not".
- **EX02** Statement: systems integrate through published, versioned interfaces. Rationale: partners and teams change independently. Implications: API governance, no direct database access, versioning policy.
- **EX03** Prefer the option using the standard API style unless a carrier cannot support it; if exceptions, wrap them behind an adapter to preserve evolvability.
- **EX04** Direct database sharing violates the principle of access via owned interfaces and widens attack surface; propose an API or event feed.
- **EX05** Decision: exception for stores via a file gateway that converts to events, owner IT director, review in 12 months.
- **EX06** Assess fit, maintenance, and security; grant a time-limited exception with an owner, conditions (isolate behind an interface), and an exit date.

**Workplace evidence:** principles you wrote that were cited in real design decisions.
