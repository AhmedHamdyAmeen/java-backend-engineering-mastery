# SRC-006 · API and data contracts — Exercises and lab

## Lab
### SRC-006-LAB1 · Contract policy
**Outcomes:** 1–4 · **Time:** ~2 h
1. Write the order domain's compatibility policy for REST APIs and events (allowed changes, notice, deprecation windows, registry mode).
2. Define the governance: ownership, CI checks, review by exception.
3. Pick one breaking change and build the impact map from registry, usage logs, and ownership data.
4. Write the migration plan: sequence, owners, dates, verification, rollback.
**Acceptance:** plan names every consumer, the sequence, and the rollback.

## Exercises (policy review; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| SRC-006-EX01 | 1 | Classify eight proposed changes (add optional field, rename field, change type, tighten validation, etc.) as compatible or breaking. |
| SRC-006-EX02 | 1 | Write a deprecation policy for public order APIs including notice period and signals. |
| SRC-006-EX03 | 2 | A producer wants to drop the `couponCode` field. List how you find who reads it and what you do if some consumers are unknown. |
| SRC-006-EX04 | 3 | Design CI checks and ownership rules that avoid a weekly schema review meeting. |
| SRC-006-EX05 | 4 | Plan the rename of `customerId` to `accountId` across four consumers with a rollback. |
| SRC-006-EX06 | 4 | Review a migration plan that removes the old field in the same release as consumers change; list its failures and a fix. |

## Solutions
- **EX01** Compatible: add optional field. Breaking: rename, change type, remove, tighten validation that rejects previously valid data, change meaning or units.
- **EX02** For example: 6 months notice for public APIs, deprecation headers and release notes, usage tracking, sunset date, direct contact with top consumers.
- **EX03** Registry subjects and consumer groups, usage logs, contract tests, code search; for unknowns, keep the field with a deprecation notice and monitor reads or access, then remove after the window.
- **EX04** Registry compatibility check in CI, owners file, required docs, auto-tagging consumers on PR, human review only for breaking or cross-domain changes.
- **EX05** Add `accountId` while keeping `customerId`; dual publish; migrate consumers one by one with contract tests; verify `customerId` unused; remove; rollback by continuing to publish both.
- **EX06** Removing in the same release breaks consumers not yet changed and prevents rollback; fix with expand and contract and verified zero usage.

**Workplace evidence:** a breaking change you coordinated across teams.
