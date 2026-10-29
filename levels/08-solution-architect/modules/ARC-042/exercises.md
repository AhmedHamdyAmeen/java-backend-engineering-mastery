# ARC-042 · Architecture assurance — Exercises and lab

## Lab
### ARC-042-LAB1 · Larkspur assurance plan
**Outcomes:** 1–4 · **Time:** ~3 h
1. Define assurance checkpoints across Larkspur delivery with focus, participants, and outputs.
2. Create a drift log template and complete it for a provided design-versus-build comparison.
3. For each Larkspur NFR, specify the test, the target, and the required evidence.
4. Write an operational acceptance checklist (monitoring, alerting, runbooks, backup and restore, support, vendor escalation) with how each item is verified.
5. Assess the provided set of test results and write a go, conditional go, or no-go recommendation.
**Acceptance:** go/no-go recommendation traceable to evidence.

## Exercises (case-based; five exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| ARC-042-EX01 | 1 | Phase one runs for five months. Propose four assurance checkpoints and what each reviews. |
| ARC-042-EX02 | 1 | A team has added a cache of customer addresses that is not in the HLD. Classify it, state the options, and write the drift log entry. |
| ARC-042-EX03 | 2 | NFR: "checkout p95 under 2 s at peak". The team provides a load test run at 20% of peak volume with synthetic data. Is the evidence sufficient? State what you would require. |
| ARC-042-EX04 | 3 | Write five operational acceptance checks for the Larkspur platform and how each is verified in practice. |
| ARC-042-EX05 | 4 | Test results: functional pass, performance met, penetration test has one open high finding, restore test not done, rollback not rehearsed. Make a recommendation. |

## Solutions
- **EX01** After the first slice (structure and integration style), before ERP and payment integration go live (contracts and failure handling), before pilot (NFR evidence, security findings), before go-live (readiness).
- **EX02** Drift, not necessarily bad; options: remove it, or accept via ADR with controls (data classification, retention, access, deletion); log entry with impact on privacy, owner, decision date.
- **EX03** Not sufficient: 20% of peak with synthetic data does not show peak behaviour; require peak (or above) volume, realistic data and mix, ERP latency included, p95 reported, tied to the requirement ID.
- **EX04** Examples: restore a backup and time it against RTO; trigger an alert and confirm the on-call receives it; run an incident drill with the vendor contact; confirm runbooks followed by someone who did not write them; verify access and permissions for support staff.
- **EX05** No-go for now or conditional go only if the high finding is fixed and retested, restore test completed, and rollback rehearsed by named dates; list each against evidence; residual risk accepted by the business owner.

All four outcomes are also covered by the lab acceptance and the quiz.

**Workplace evidence:** an assurance review or go-live decision you led.
