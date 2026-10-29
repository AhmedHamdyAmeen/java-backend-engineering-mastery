# STF-003 · Architecture governance at scale — Exercises and lab

## Lab
### STF-003-LAB1 · Governance model
**Outcomes:** 1–4 · **Time:** ~2.5 h
1. Gather recent architecture disputes and the current review process for Platform 2.0.
2. Write principles (each with a trade-off and example) that would have resolved those disputes.
3. Draft two reference architectures (for example, event-driven service and public API service) with templates outlined.
4. Write the decision-rights matrix with response times and set a review turnaround target.
5. Test with a role-played team lead on five sample decisions; revise.
**Acceptance:** a role-played team lead can tell, for five sample decisions, who decides and how fast.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| STF-003-EX01 | 1 | Rewrite three vague principles ("be scalable", "use best practices", "keep it simple") into decisive ones with a stated trade-off. |
| STF-003-EX02 | 1 | Two teams argue about sync versus async calls between domains. Write a principle that settles it and an example. |
| STF-003-EX03 | 2 | Outline a reference architecture for a public REST service: what is fixed, what is open, what the template contains. |
| STF-003-EX04 | 3 | Classify eight decisions as team, domain, or organization level and name consulted parties. |
| STF-003-EX05 | 4 | A central review board has a three-week queue. Propose a design that scales and the three metrics you would track. |
| STF-003-EX06 | 4 | Three governance rules have no owner and a 60% bypass rate. Decide for each whether to automate, fix, or remove. |

## Solutions
- **EX01** Example: "Prefer managed services over self-hosted, unless a documented need exists; the cost of operating is part of the decision."
- **EX02** Asynchronous events between domains by default; synchronous only for user-facing reads needing immediate answers; accept eventual consistency otherwise.
- **EX03** Fixed: authentication, error format, versioning, observability fields. Open: framework internals, database. Template: repository with CI, deployment manifest, sample tests.
- **EX04** Examples: database for one service (team); event schema between two domains (domain); identity provider (organization). Name consulted roles such as security.
- **EX05** Tiered review: teams decide inside guardrails, light asynchronous review for cross-team items with a response-time target. Metrics: turnaround, queue size, bypass rate.
- **EX06** Automate rules that can be checked in CI; fix those that help but cost too much; remove those with no owner or purpose.

Outcome coverage: all four outcomes are exercised above and in the lab.

**Workplace evidence:** a governance mechanism you designed that sped up or improved decisions.
