# MID-066 · Technical collaboration — Exercises and lab

## Lab
### MID-066-LAB1 · Mentor and review
**Outcomes:** 1–4 · **Time:** ~2 h
1. Review two Junior-level capstone pull requests with labeled, teaching comments.
2. Pair with a Junior learner on one fix; let them drive.
3. Collect feedback from the mentee on how helpful the pairing was.
4. Write a short note on one disagreement you handled and how it was resolved.
**Acceptance:** reviews scored on usefulness; mentee feedback collected.

## Exercises (assessment: review-quality rubric; five exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-066-EX01 | 1 | Review a 60-line diff with a hidden race condition and a missing timeout; write labeled comments. |
| MID-066-EX02 | 2 | Rewrite five harsh or vague review comments so they are specific, kind, and actionable. |
| MID-066-EX03 | 2 | Prepare a design review of a one-page design: list your ten questions and what feedback the author should request. |
| MID-066-EX04 | 3 | Write a well-scoped task brief for a junior to add input validation to one endpoint. |
| MID-066-EX05 | 4 | Two engineers disagree on cache versus read replica. Write a neutral summary for the decider. |

## Solutions
- **EX01** `blocking:` shared mutable state without synchronization, with a failing test idea; `blocking:` call without timeout (MID-023); `question:` what if the list is empty; one praise.
- **EX02** For example "bad naming" becomes "`data` hides what it holds; `pendingOrders` would say it. suggestion:".
- **EX03** Questions on problem, constraints, alternatives, failure modes, load, rollout, rollback, observability, security, cost; the author asks for feedback on risks and alternatives.
- **EX04** Goal, links to patterns, acceptance (tests for valid and invalid input), one hint, stuck limit of 30 minutes, review time.
- **EX05** Context, options with trade-offs (freshness, complexity, cost), measurements to take, recommendation if any, decision date.
