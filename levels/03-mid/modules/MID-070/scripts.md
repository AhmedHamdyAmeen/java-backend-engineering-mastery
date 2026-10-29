# MID-070 · LLM evaluation and observability — Lecture scripts

**Video:** 67 min · **Analogy used throughout:** an exam for a new employee, with a marking scheme, graded the same way every time, plus a timesheet showing what each task cost. Running project: Shop.
Format: **Goal** · **Key points** · **Show** · **Check**.
Version note: tracing conventions for LLM calls (OpenTelemetry GenAI attributes) and evaluation tools evolve; verify version before recording.

---

## MID-070-L01 · Why LLM features need evaluations (8 min)
**Goal:** explain why normal tests are not enough.

**Key points**
- LLM output is variable and open-ended; an exact-match assertion rarely fits.
- A prompt, model, or retrieval change can silently make answers worse; nobody notices until customers complain.
- An evaluation (eval) is a repeatable test set with scoring that turns "seems fine" into numbers.
- Evals gate releases, like unit tests and contract tests.

**Show:** two runs of the order-support assistant on the same questions: groundedness 92% versus 71% after a prompt tweak.

**Check:** What problem do evals solve? *(Silent quality drops after prompt, model, or retrieval changes.)*

---

## MID-070-L02 · Building an evaluation set (10 min)
**Goal:** assemble a realistic, useful question set.

**Key points**
- Collect real questions (support tickets, logs, with personal data removed), not five hand-picked ones; start with about 50 and grow.
- Cover categories: normal questions, edge cases, questions that must be refused, adversarial ones.
- For each: the question, the expected source documents, and acceptance criteria (must mention X; must not claim Y).
- Version the set in Git and review it like code.
- Keep a held-out part you do not tune against.

**Show:** a row: `{id: q17, question: "Can I return opened shoes?", sources: ["returns-policy#2"], must: ["30 days"], mustNot: ["free shipping"]}`.

**Check:** Name three kinds of questions in a set. *(Normal, edge or adversarial, and must-refuse.)*

---

## MID-070-L03 · Metrics: recall, groundedness, refusals (10 min)
**Goal:** measure the parts of a retrieval-based assistant.

**Key points**
- Retrieval recall: did the retrieved passages include the expected source? (Measure before blaming the model.)
- Groundedness (faithfulness): is every claim in the answer supported by the retrieved sources?
- Refusal correctness: refuses when the sources do not answer, answers when they do.
- Also track format validity and latency per step.
- Report per category so a weak area is visible.

**Show:** table: metric | how measured | threshold (for example recall at least 0.9, groundedness at least 0.9, refusal correctness at least 0.95).

**Check:** If recall is low, where do you look first? *(Retrieval: chunking, embeddings, search settings.)*

---

## MID-070-L04 · LLM-as-judge and its caveats (8 min)
**Goal:** use a model as a grader responsibly.

**Key points**
- A judge model scores answers against a rubric, scaling beyond what humans can read.
- Calibrate: have humans label a sample (for example 50), compare agreement with the judge, and adjust the rubric.
- Known biases: favors longer answers, favors its own style, can be inconsistent; use clear rubrics and fixed settings.
- Prefer deterministic checks where possible (citation present, source id matches).
- Re-calibrate when the judge model changes.

**Show:** agreement table: human label versus judge label on 50 samples, with the agreement rate.

**Check:** Why calibrate a judge? *(To know how far its scores match human judgment.)*

---

## MID-070-L05 · Evaluations in CI (8 min)
**Goal:** make quality a pipeline gate.

**Key points**
- Run the evaluation set on every change to prompts, model version, retrieval config, or tools.
- Fail the pipeline when a metric falls below its threshold or drops more than an allowed margin from the baseline.
- Control cost and flakiness: cache retrieval results, fix the temperature, run a fast subset on every PR and the full set nightly.
- Store results with the prompt and model version for comparison.

**Show:** pipeline stage: `eval` job → report artifact → threshold check → pass or fail.

**Check:** What triggers an evaluation run? *(A change to prompt, model, retrieval, or tools.)*

---

## MID-070-L06 · Tracing tokens, latency, and cost (10 min)
**Goal:** make every request observable and its cost visible.

**Key points**
- One trace per conversation turn, with spans for retrieval, each model call, and each tool call.
- Attributes: model name and version, prompt version, input and output tokens, latency, computed cost, outcome.
- Do not store raw personal data in traces without a policy.
- Dashboards: cost per conversation per day, p95 latency per step, error and refusal rates.
- Alerts on cost spikes so the bill is not the first signal.

**Show:** span tree: `assistant.turn` → `retrieval` (40 ms) → `llm.call` (1.8 s, 1,200 in / 300 out tokens, 0.004 USD) → `tool.get_order_status`.

**Check:** Why record the prompt version on spans? *(To tell which change caused a quality or cost change.)*

---

## MID-070-L07 · Demo: an evaluation run catching a prompt regression (13 min)
**Goal:** watch the pipeline block a worse prompt. Prepares `MID-070-LAB1`.

**Steps**
1. Run the 50-question set on the current prompt: baseline recorded.
2. Open the report: recall, groundedness, and refusal correctness per category.
3. **Planned mistake:** shorten the prompt to save tokens (dropping the "answer only from sources" rule).
4. Run the pipeline: groundedness falls below the threshold; the build fails and lists the failing questions.
5. Restore the rule, keep the shorter wording elsewhere, and rerun: pass.
6. Open the dashboard: cost per conversation fell slightly, which would have hidden the regression.
