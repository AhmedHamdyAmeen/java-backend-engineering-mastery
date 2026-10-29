# SRA-012 · Engineering standards — Exercises and lab

## Lab
### SRA-012-LAB1 · Commerce standards
**Outcomes:** 1–4 · **Time:** ~1.5 h
1. Choose three standards for Commerce 2030: API, events, and observability. Justify each with a recurring pain and the number of teams affected.
2. Write each as principle, default, how-to-check, and exception process.
3. Write an adoption plan for each: paved road or tooling, rollout order, and numeric adoption measures.
4. Process one exception request from a role-played team, with a recorded decision and expiry.
5. Add a retirement review date and criteria for each standard.
**Acceptance:** adoption measurable; one exception processed.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| SRA-012-EX01 | 1 | From a list of ten possible standards, pick the three with the best value-to-cost ratio and justify with the affected teams. |
| SRA-012-EX02 | 1 | A director proposes "all services in one language". Write a short reply that redirects to higher-value standards. |
| SRA-012-EX03 | 2 | Rewrite a mandate ("all services must log in JSON") as principle, default, and exception process. |
| SRA-012-EX04 | 3 | Design the paved road for the event standard: what the template provides and the adoption metrics you will publish. |
| SRA-012-EX05 | 2 | Review an exception request and write a decision with scope, risk accepted, owner, and expiry. |
| SRA-012-EX06 | 4 | Given a yearly table of five standards (exceptions, adoption, pain), decide keep, simplify, or retire for each. |

## Solutions
- **EX01** Typical picks: API error and versioning format, event envelope, observability fields; they cross team boundaries and hurt operations most. Weak candidates: code style, internal layout.
- **EX02** Say the pain is rarely language; name the real pain (incidents crossing services, inconsistent contracts) and offer boundary standards; revisit language choices only with data.
- **EX03** Principle: logs are machine-searchable across services. Default: template logger emits JSON with agreed fields. Exception: a team documents why, with owner and expiry.
- **EX04** Template emits trace context, log fields, and base metrics by default; CI checks conformance; dashboard shows percent of services conforming per team and reasons for non-adoption.
- **EX05** Grant a narrow exception (different payload encoding, standard identity and trace fields kept), expiry three months, review with measurements; consider whether the default needs a fast path.
- **EX06** Retire when the pain is gone or tooling automates it; simplify when many exceptions share a cause; keep when adoption is high and pain remains.

Outcome 3 is also covered by the lab adoption plan; outcome 4 by the lab review criteria.

**Workplace evidence:** a standard you authored that teams adopted voluntarily.
