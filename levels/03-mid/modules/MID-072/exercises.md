# MID-072 · AI-assisted engineering at codebase scale — Exercises and lab

## Lab
### MID-072-LAB1 · AI-assisted refactor
**Outcomes:** 1–5 · **Time:** ~2.5 h
1. Pick one Shop Platform service module; give an AI assistant a focused context (files, tests, conventions).
2. Refactor in small steps under a green suite; commit each step.
3. Add regression tests for a past incident; run mutation testing on the new tests.
4. Submit a pull request with a prompt log, accepted and rejected suggestions, and mutation results.
**Acceptance:** behavior unchanged (all tests and contracts green); reviewer can trace every AI-originated change.

## Exercises (assessment: review an AI-generated pull request; five exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-072-EX01 | 1 | Write a prompt to add a feature to `inventory`: goal, files, constraints, existing pattern, failing test; redact anything sensitive from a sample log. |
| MID-072-EX02 | 2 | From a stack trace with a `LazyInitializationException`-style error, list three hypotheses and the evidence that would confirm each. |
| MID-072-EX03 | 3 | Plan a refactor of a 300-line method into five small steps, each with a verification. |
| MID-072-EX04 | 4 | Review five AI-generated tests; keep, change, or discard each with a reason. |
| MID-072-EX05 | 5 | Define three metrics to judge an AI rollout in your team and how you would collect them. |

## Solutions
- **EX01** Context limited to the relevant files and the pattern to follow; constraints stated; secrets and personal data replaced with synthetic values.
- **EX02** Hypotheses such as access outside a transaction, a changed fetch mode, or a recent refactor; confirm by reproducing, inspecting the transaction boundary, and checking recent diffs.
- **EX03** Characterization test, extract validation, extract pricing, extract persistence, rename; run tests and commit after each.
- **EX04** Keep tests with edge cases and requirement-based expectations; discard those mirroring implementation or asserting a known bug; change tests with wrong expected values.
- **EX05** Review time per PR, escaped defects or change failure rate, mutation score or flaky test rate; collect from the Git host, incident log, and CI.
- Outcome 5 is also covered by the lab's mutation results and the practical review.
