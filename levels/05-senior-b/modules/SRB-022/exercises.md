# SRB-022 · AI tools across teams — Exercises and lab

## Lab
### SRB-022-LAB1 · Assistant rollout at FulfillCo
**Outcomes:** 1–4 · **Time:** ~3.5 h
1. Write a pilot plan for an AI coding assistant across the four teams, with a control group, training, support, and a review gate.
2. Write the usage policy (confidentiality, secrets, licensing, review) and run the tool security review with a role-played security lead.
3. Write a measurement plan using DORA and quality metrics, with a baseline, a defect-rate check, and a review-load measure.
**Acceptance:** policy approved by a role-played security lead; measurement plan includes a baseline and a defect-rate check.

## Exercises (assessment: rollout plan defense)
| ID | Outcome | Task |
| --- | --- | --- |
| SRB-022-EX01 | 1 | Case: two of four teams already use assistants personally. Write the rollout plan outline with pilot, control, training, and gate. |
| SRB-022-EX02 | 1 | List three risks of rolling out widely without a pilot and how the pilot mitigates each. |
| SRB-022-EX03 | 2 | Draft a one-page usage policy and name its owner and review date. |
| SRB-022-EX04 | 2 | A developer pasted a production config with credentials into an assistant. Write the incident steps and a policy change. |
| SRB-022-EX05 | 3 | Fill a security review questionnaire for a candidate tool: data handling, retention, access, admin controls, with evidence sources. |
| SRB-022-EX06 | 4 | Case: pilot teams show 25% more pull requests and higher defect rate. Write the honest reading and next step. |
| SRB-022-EX07 | 4 | Design a measurement plan with baseline, control, three metric families, and a decision rule. |
| SRB-022-EX08 | 1 | Defend your rollout plan in five minutes against three role-played objections (cost, quality, juniors). |

## Solutions
- **EX01** Pilot with two teams (including a skeptic) and two controls; training on verification and data limits; support channel; gate at week 9 requiring policy and security approval.
- **EX02** Unmeasured quality drift, data leakage, inconsistent practice; the pilot limits exposure and produces a baseline and evidence.
- **EX03** Sections: scope, approved tools, allowed and forbidden data, secrets, licensing note (legal), review rule, incident path, exception route, owner, review date.
- **EX04** Rotate the credentials immediately, report the incident, check vendor retention and deletion, add secret scanning on prompts or IDE where possible, and update training.
- **EX05** Example rows: data sent and training use; retention and deletion; SSO and roles; audit logs; repository exclusions. Answers must cite contract or documentation; mark unknowns as open risks.
- **EX06** The result is mixed: throughput up, quality and review load worse, possible novelty and selection effects. Extend the pilot, fix review capacity, and compare with control.
- **EX07** Questions with metrics: lead time and frequency (delivery), change failure and defect rate (quality), survey and toil time (experience), review time per PR (load). Rule: widen only if quality is no worse and at least one delivery or experience measure improves relative to control.
- **EX08** Evidence is the plan's baseline, policy, and gate; answer cost with measured time saved versus license, quality with defect check, juniors with training and review rules.
- Outcome 3 is also covered by the lab security review.

**Workplace evidence:** an AI tool rollout or policy you led and what the data showed.
