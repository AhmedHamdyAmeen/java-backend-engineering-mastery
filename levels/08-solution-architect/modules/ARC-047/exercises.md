# ARC-047 · AI vendor and model evaluation — Exercises and lab

## Lab
### ARC-047-LAB1 · AI vendor choice
**Outcomes:** 1–4 · **Time:** ~3.5 h
1. Define gates, criteria, and weights for the Larkspur assistant with role-played stakeholders.
2. Build a task-specific evaluation set (at least 50 questions including hard cases) and a scoring rubric.
3. Run it against two hosted providers and one self-hosted open-weight model; record quality, latency, and cost per conversation. Verify model versions and prices before recording.
4. Review each provider's terms (residency, retention, training use, exit) against Larkspur policy.
5. Build a three-year cost model with usage growth scenarios and a switching reserve.
6. Write a recommendation with evaluation scores, three-year cost, conditions, and an exit plan.
**Acceptance:** recommendation with evaluation scores, three-year cost, and exit plan.

## Exercises (case-based; five exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| ARC-047-EX01 | 1 | List the criteria for choosing the Larkspur assistant's model provider, mark which are gates, and assign draft weights to the rest. |
| ARC-047-EX02 | 2 | The CIO proposes choosing the model that tops a public leaderboard. Write a short reply and describe what you would do instead. |
| ARC-047-EX03 | 2 | Design ten evaluation items from tickets, covering at least four categories and three hard cases. Show the fields recorded for each. |
| ARC-047-EX04 | 3 | Write a four-week PoC charter for the assistant with success criteria, tests, and decision owner. |
| ARC-047-EX05 | 4 | Larkspur expects 40,000 conversations a month in year one, growing 50% per year. Outline the three-year cost model structure for a hosted and a self-hosted option, including exit. Do not use real prices; mark them to verify. |

## Solutions
- **EX01** Gates: data terms (no training on company data, retention and region acceptable), security controls. Weighted example: quality on own tasks 35%, cost 20%, latency 15%, support and roadmap 10%, exit and portability 10%, operating effort 10%; weights agreed with stakeholders before scoring.
- **EX02** Leaderboards measure general public tasks; they do not reflect Larkspur's questions, documents, tone, latency, or cost. Build the evaluation set from tickets, run candidates, and decide on measured results with gates applied.
- **EX03** Fields: id, question, category, source document, expected answer or rubric, difficulty, pass criteria. Categories such as order status, returns, delivery, loyalty; hard cases: out-of-scope, conflicting policy, injection attempt.
- **EX04** Questions: accuracy grounded in documents, injection resistance, latency at expected load, cost per conversation; thresholds set in advance; real masked data; failure-mode tests; decision owner (e.g. head of customer service with security sign-off); exit if thresholds are not met.
- **EX05** Conversations per month x cost per conversation (tokens in and out) per year with growth; hosted: usage cost, integration, evaluation, monitoring, people; self-hosted: hardware, operations staff, upgrades, plus usage; switching reserve and re-evaluation yearly; exit: portable prompts and evaluation set, abstraction layer, data return and deletion terms; prices to verify before recording.

All four outcomes are also covered by the lab acceptance and the quiz.

**Workplace evidence:** an AI vendor or model evaluation you ran and its outcome.
