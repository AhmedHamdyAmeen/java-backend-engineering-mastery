# MID-070 · LLM evaluation and observability — Exercises and lab

## Lab
### MID-070-LAB1 · Measured assistant
**Outcomes:** 1–5 · **Time:** ~3 h
Create a 50-question evaluation set for the order-support assistant and run it in CI with pass thresholds. Add OpenTelemetry spans for retrieval, model call, and tools with token and cost attributes. Build a Grafana dashboard for cost per conversation and p95 latency.
**Acceptance:** a deliberately worse prompt fails the pipeline; cost per conversation is visible per day.

## Exercises (assessment: evaluation plan for a new AI feature)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-070-EX01 | 1 | Write 20 evaluation rows (question, expected sources, must and must-not criteria) covering normal, edge, adversarial, and must-refuse cases. |
| MID-070-EX02 | 2 | Compute retrieval recall for the set by checking whether the expected source is in the top-k results. |
| MID-070-EX03 | 2 | Write a rule-based check for refusal correctness and one for citation presence. |
| MID-070-EX04 | 3 | Label 30 answers by hand, run a judge model with a rubric, and compute agreement; list two judge failures. |
| MID-070-EX05 | 4 | Add a CI stage that fails when groundedness drops below 0.9 or falls more than 3 points from baseline. |
| MID-070-EX06 | 5 | Add spans with model version, prompt version, tokens, and cost; verify them in the trace backend. |
| MID-070-EX07 | 1–5 | Design an evaluation plan for a new "product description generator": data, metrics, thresholds, what blocks a release, and the dashboards and alerts. |

## Solutions
- **EX01** Include rows such as a policy question, an ambiguous one, a prompt-injection attempt, and one whose answer is not in the sources (expected: refusal).
- **EX02** `recall = rows where expected source in top-k / total rows`.
- **EX03** Refusal: the answer matches a refusal pattern exactly when no source supports it; citation: the answer cites a retrieved source id.
- **EX04** Agreement = matching labels / 30; typical failures: rewards verbose answers, misses subtle unsupported claims.
- **EX05** Compare the run's metrics with the stored baseline; non-zero exit when below threshold or margin.
- **EX06** Span attributes for model, prompt version, token counts, and computed cost; check them in Jaeger or Tempo.
- **EX07** Include a held-out set, human review sample, calibrated judge, thresholds (for example groundedness at least 0.9), release blockers (any threshold miss, any safety failure), and cost and latency alerts.

**Outcome 1** is also checked by quiz Q01-Q02; outcome 3 by the quiz and EX04.
