# SRA-021 · AI strategy and build vs buy — Exercises and lab

## Lab
### SRA-021-LAB1 · Commerce 2030 AI strategy
**Outcomes:** 1–4 · **Time:** ~2 h
1. Define a portfolio of AI use cases for the marketplace, including a seller listing assistant, a support assistant, and search.
2. Score each by value, feasibility, data readiness, risk, and cost; reject at least one with reasons.
3. For the shortlisted cases choose hosted, open-weight, or managed, and prompting, RAG, or fine-tuning, with justification.
4. Build a three-year cost model with explicit usage assumptions, price-change scenarios, and exit options.
5. Check data foundations: owners, quality, sensitivity.
6. Defend the strategy to a role-played CTO and CFO.
**Acceptance:** at least one idea rejected with reasons; costs traceable to usage assumptions.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| SRA-021-EX01 | 1 | Score six AI ideas for the marketplace and reject two; write the reasons in terms of value, risk, and cost. |
| SRA-021-EX02 | 2 | Compare a hosted API, an open-weight self-hosted model, and a managed platform for the support assistant on cost, control, latency, and data handling. |
| SRA-021-EX03 | 2 | Design an evaluation set and procedure that lets you compare two models fairly on your own task. |
| SRA-021-EX04 | 3 | For three use cases choose prompting, RAG, or fine-tuning, and state the evidence that would make you escalate. |
| SRA-021-EX05 | 4 | Build a three-year cost model for the listing assistant with usage, price change, and review effort; compute the break-even against self-hosting. |
| SRA-021-EX06 | 4 | Write the exit plan for a single-provider dependency and a data-readiness checklist for a RAG use case. |

## Solutions
- **EX01** Example rejects: a fully automated price-setting assistant (high risk, unclear value) and an AI feature that duplicates a rules engine. Keep ideas with a measurable outcome, adequate data, and acceptable risk.
- **EX02** Hosted: low start cost, scales with use, data leaves under provider terms; self-hosted: control and residency, GPU and staffing burden; managed: in-cloud controls at a premium. Check latency and terms by verification.
- **EX03** Representative inputs with expected outputs, scoring rubric (human and automatic), blind comparison, cost and latency recorded, rerun for each candidate model.
- **EX04** Support assistant over changing documentation: prompting plus RAG. Listing assistant with a consistent house style: prompting first; fine-tune only if evaluation shows style failures persist. Product search: ranking signals and retrieval first. Escalate on measured quality gaps.
- **EX05** Multiply requests by tokens by unit price, add review time, evaluation and staffing; self-hosting adds GPUs, utilization, redundancy, and engineers; break-even is the volume where totals cross; show sensitivity to price drops.
- **EX06** Exit plan: abstraction layer, portable prompts and evaluation suite, second provider tested, data export. Checklist: owner, freshness, quality checks, sensitivity class, access control, deletion path.

Outcomes 1 and 4 are also covered by the lab defense and the quiz.

**Workplace evidence:** an AI investment decision you shaped with a cost and value case.
