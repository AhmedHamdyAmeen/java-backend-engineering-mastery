# SRB-021 · AI platform capabilities — Exercises and lab

## Lab
### SRB-021-LAB1 · FulfillCo LLM gateway
**Outcomes:** 1, 2, 3, 4 · **Time:** ~4 h
1. Define gateway requirements from the four teams.
2. Prototype auth, quotas, redaction, request logging, and cost attribution.
3. Test a runaway team against another team's quota and scan logs for personal data.
4. Write the AI golden path and decide what stays central versus product-owned.
**Acceptance:** one team's runaway usage cannot exhaust another's quota; cost per team reported; no unredacted personal data in logs.

## Exercises
| ID | Outcome | Task |
| --- | --- | --- |
| SRB-021-EX01 | 1 | List the gateway responsibilities and three non-goals. |
| SRB-021-EX02 | 1 | Design quota tiers for four teams with burst limits. |
| SRB-021-EX03 | 2 | Design a shared retrieval service with per-team data ownership and access control. |
| SRB-021-EX04 | 3 | Write redaction rules and five test inputs including tricky ones. |
| SRB-021-EX05 | 3 | Draft the AI golden path checklist. |
| SRB-021-EX06 | 4 | Decide which of six capabilities to centralize (gateway, prompt library, retrieval engine, eval harness, product prompts, UX). |

## Solutions
- **EX01** Auth, quotas, redaction, logging, cost, routing; not prompts, evaluation of product quality, or business logic.
- **EX02** Per-team daily token budgets, per-minute rate limits, alerts at 80%, hard stop with clear error.
- **EX03** Namespaces per team, source permission filter at query time, deletion path, re-embedding.
- **EX04** Email, phone, address, order number patterns; tests for formats and false positives.
- **EX05** Gateway client, eval harness, observability, security checks, runbook.
- **EX06** Centralize gateway, retrieval machinery, eval harness; leave product prompts and UX to teams; prompt library optional.

**Workplace evidence:** a shared AI capability other teams adopted.
