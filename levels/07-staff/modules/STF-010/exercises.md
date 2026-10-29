# STF-010 · Technical due diligence — Exercises and lab

## Lab
### STF-010-LAB1 · Acquisition review
**Outcomes:** 1–4 · **Time:** ~2.5 h
1. Review the payments start-up's architecture docs, repository sample, incident history, and team interview notes (case materials).
2. Assess architecture, code health, operations, security, and team capability with a common checklist.
3. Build a risk register separating deal-breakers from fixable debt with costed remediation.
4. Write the report with a go/no-go recommendation and conditions, plus a modernization outline sized to the findings.
5. Present to a role-played deal team and answer challenges.
**Acceptance:** top risks costed; recommendation stated with conditions.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| STF-010-EX01 | 1 | Given a one-page description of a target, list the ten questions and evidence requests you would send in day one. |
| STF-010-EX02 | 1 | Review a sample repository summary (no tests, two-year-old dependencies, one deployer) and rate each area. |
| STF-010-EX03 | 2 | Classify six findings as deal-breaker or fixable debt and estimate cost ranges with confidence. |
| STF-010-EX04 | 2 | A colleague criticizes the target's code style. Redirect the review to risk with three better findings to look for. |
| STF-010-EX05 | 3 | Write the summary page of a due-diligence report with recommendation, conditions, and unknowns. |
| STF-010-EX06 | 4 | For a target with a fragile monolith and strong team, outline a modernization plan sized to the findings. |

## Solutions
- **EX01** Examples: last three incidents, backup restore test, access list, vulnerability scan, payment-compliance evidence, architecture diagram, deployment process, team structure, key-person map, customer concentration.
- **EX02** Test gaps are high risk for change; old dependencies medium to high (security); single deployer is key-person risk; give ratings and fixes.
- **EX03** Deal-breakers: unlicensed core code, no way to meet required scale. Fixable: missing tests, dependency upgrades. Costs in engineer-months with ranges.
- **EX04** Style rarely drives risk; check change failure history, data protection, recovery capability.
- **EX05** Lead with go with conditions or no-go; top three risks with costs; unknowns and extra access needed.
- **EX06** Stabilize with tests and monitoring, then strangle the riskiest modules behind interfaces; retain the team; stage the investment.

Outcome coverage: all four outcomes are covered by exercises and lab.

**Workplace evidence:** an assessment you produced that informed an acquisition, vendor, or modernization decision.
