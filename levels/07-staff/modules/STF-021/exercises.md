# STF-021 · AI governance and engineering productivity — Exercises and lab

## Lab
### STF-021-LAB1 · AI governance for Platform 2.0
**Outcomes:** 1–4 · **Time:** ~3 h
1. Draft the governance model: roles, decision rights, and review cadence.
2. Write the approved-tool list criteria and data rules by data class (verify vendor terms before recording).
3. Write the evaluation standard for AI features and the rules for AI-generated code.
4. Design platform guardrails (gateway, scanning, review rules) and map each rule to an enforcement point.
5. Write the measurement plan across about 20 teams with baselines and quality counter-metrics.
**Acceptance:** every rule has an enforcement point or an explicit owner; measurement plan has baselines and quality counter-metrics.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| STF-021-EX01 | 1 | A director proposes banning all AI tools. Write a one-page response comparing ban and governance with risks and benefits. |
| STF-021-EX02 | 1 | Define four data classes and which AI tool tiers each may use; name who approves new tools. |
| STF-021-EX03 | 2 | Write an evaluation standard for an AI-powered product search feature: evaluation set, threshold, monitoring, human review points. |
| STF-021-EX04 | 3 | Take five policy rules and assign each an enforcement point (gateway, pipeline, template) or an owner. |
| STF-021-EX05 | 3 | Review a governance proposal where a board reviews every prompt; redesign it so it scales. |
| STF-021-EX06 | 4 | Draft a measurement plan with baselines and counter-metrics; explain two confounders and how you handle them. |

## Solutions
- **EX01** Ban pushes use out of sight and loses benefits; governance gives approved tools, data rules, gateway logging, and measurement; accept residual risk with monitoring.
- **EX02** Classes: payment data (never), customer personal data (approved tools with redaction or none), source code (approved tools only), public material (free). Security and legal approve additions.
- **EX03** Evaluation set of real queries with judged answers; threshold on relevance and safety; monitor drift, cost, and complaints; human review for prompt changes; rollback to the previous version.
- **EX04** Examples: no secrets in prompts (gateway redaction and pipeline scan), approved tools only (gateway allow list), review of generated code (pull request template and required reviewer), data classes (owner: security).
- **EX05** Move to team-owned decisions within guardrails; audit samples through the gateway logs; escalate exceptions only.
- **EX06** Metrics: lead time, review time, defect rate, change failure rate, survey. Confounders: team size and work type; handle by comparing the same team before and after and matching comparison teams; report ranges.

Outcome coverage: all four outcomes appear in exercises and lab.

**Workplace evidence:** AI governance or guardrails you established across several teams.
