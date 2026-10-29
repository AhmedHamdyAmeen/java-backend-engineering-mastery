# ARC-022 · Cloud architecture frameworks — Exercises and lab

## Lab
### ARC-022-LAB1 · Larkspur review
**Outcomes:** 1–3 · **Time:** ~3 h
1. Collect the infrastructure design artifacts from ARC-011 to ARC-021.
2. Review each pillar with questions and evidence.
3. Record findings and rate them by likelihood and impact.
4. Prioritize, then decide per finding: fix, mitigate, accept, or defer.
5. Write the remediation plan with owners and dates, and the review report.
**Acceptance:** high-risk findings either fixed in the design or accepted by a named owner.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| ARC-022-EX01 | 1 | Write one review question per pillar for Larkspur. |
| ARC-022-EX02 | 1 | Map these concerns to pillars: restore tests, tag enforcement, MFA for admins, autoscaling, energy-efficient regions, runbooks. |
| ARC-022-EX03 | 2 | Describe how you would run the review so findings rest on evidence. |
| ARC-022-EX04 | 2 | Given six findings, rate and order them: no DR test, missing tags on non-prod, payment egress open, unused large instances, logs kept forever, no alerting on checkout errors. |
| ARC-022-EX05 | 3 | Write a remediation entry for the payment egress finding. |
| ARC-022-EX06 | 3 | A sponsor wants to accept the missing DR test risk. Write the acceptance record. |

## Solutions
- **EX01** Operational excellence: how do we deploy and roll back? Security: who can reach payment data? Reliability: what happens if a zone fails? Performance: how does checkout scale at peak? Cost: which costs scale with volume? Sustainability: are idle resources shut down?
- **EX02** Restore tests: reliability; tag enforcement: operational excellence or cost; MFA: security; autoscaling: performance efficiency (and cost); efficient regions: sustainability; runbooks: operational excellence.
- **EX03** Preparation with owners, question lists, requests for evidence (configs, test results, dashboards), walkthrough with the build and operations teams, recorded findings.
- **EX04** High: payment egress open, no DR test, no checkout alerting; medium: unused large instances (cost), logs kept forever (cost and privacy); low: missing tags on non-prod. Order high first.
- **EX05** Finding, risk high; action: restrict egress to the provider endpoints; owner: network lead; due date; success: flow test shows other destinations denied.
- **EX06** Risk statement, impact, reason for acceptance, compensating controls, accepting owner's name, date, and review date; sponsor signs.

**Workplace evidence:** a well-architected review you ran and the improvements it produced.

---
Outcome coverage: all outcomes covered by exercises and the lab.
