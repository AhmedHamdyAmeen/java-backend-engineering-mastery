# JNR-053 · Team workflows — Exercises and lab

## Lab
### JNR-053-LAB1 · Team sprint
**Outcomes:** 1–4 · **Time:** ~2 h
In groups of three, deliver two Shop features in a one-week mini-sprint with issues, PRs, and reviews, ending with a retrospective.
**Acceptance:** every change merged through a reviewed PR; retro notes written.

## Exercises (assessment: PR and review quality)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-053-EX01 | 1 | Compare trunk-based development and long-lived branches for a team of five; recommend one. |
| JNR-053-EX02 | 2 | Write a PR template with five sections and fill it in for a real Shop change. |
| JNR-053-EX03 | 2 | Split a 1,500-line change description into three PR-sized changes. |
| JNR-053-EX04 | 3 | Rewrite three harsh review comments constructively. |
| JNR-053-EX05 | 3 | Review a peer's PR: one correctness comment, one test comment, one optional nit. |
| JNR-053-EX06 | 4 | Split the "checkout" feature into five issues with acceptance criteria and rough sizes. |
| JNR-053-EX07 | 4 | Describe what happens in planning, stand-up, review, and retrospective in one sentence each. |

## Solutions
- **EX01** Trunk-based: fewer merge conflicts, faster feedback, needs good CI and feature flags. Long-lived branches: painful merges and late integration. Recommend trunk-based or short-lived branches.
- **EX02** Sections: Summary, Why, How tested, Risks, Linked issue.
- **EX03** Separate refactor, new feature, and tests/docs, each mergeable on its own.
- **EX04** For example "This is wrong" becomes "This fails for an empty list; could we handle it and add a test?"
- **EX05** Comments are specific, polite, and marked blocking or nit.
- **EX06** For example: cart totals, shipping rules, payment call, order confirmation, error handling; each with "done when ..." criteria and S/M/L size.
- **EX07** Planning: choose and size work. Stand-up: share progress and blockers. Review: demo finished work. Retro: improve how the team works.
- Common mistakes (2,000-line PRs, style-only reviews) are assessed through the PR and review quality marking.
