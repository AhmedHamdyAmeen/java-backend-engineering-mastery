# MID-070 · LLM evaluation and observability — Quiz

Outcomes: O1 evaluation sets · O2 metrics · O3 LLM-as-judge · O4 evaluations in CI · O5 tracing tokens and cost.

**Q01 (O1)** Why use an evaluation set? A. To make answers longer B. To detect silent quality changes after edits C. To avoid unit tests D. To train the model
**Q02 (O1)** A good evaluation set includes: A. Five favorite questions B. Only easy questions C. Real, varied questions with expected sources and criteria D. Only random text
**Q03 (O2)** Retrieval recall measures whether: A. The answer is polite B. Tokens were counted C. The model refused D. The expected source was retrieved
**Q04 (O2)** Groundedness means: A. Answer claims are supported by the sources B. The answer is short C. The model is local D. The answer is fast
**Q05 (O2)** Refusal correctness means the assistant: A. Always refuses B. Refuses when sources do not answer and answers when they do C. Never refuses D. Refuses long questions
**Q06 (O3)** Before trusting a judge model you should: A. Calibrate it against human-labeled samples B. Use a higher temperature C. Make it longer D. Hide its rubric
**Q07 (O3)** A known bias of judge models: A. They are too slow B. They never agree C. They may favor longer answers D. They need no rubric
**Q08 (O4)** In CI the evaluation should fail the build when: A. The pipeline is green B. A metric falls below its threshold C. The prompt file exists D. Tokens are counted
**Q09 (O5)** Which belongs on a model-call span? A. The customer's password B. Nothing C. The whole database D. Model version, prompt version, tokens, and cost
**Q10 (O5)** Cost problems are best caught by: A. The monthly invoice B. Customer complaints C. A cost-per-conversation dashboard with alerts D. Guessing

## Answers
Q01 B · Q02 C · Q03 D · Q04 A · Q05 B · Q06 A · Q07 C · Q08 B · Q09 D · Q10 C

## Practical part
Seven exercises `MID-070-EX01` to `EX07` (EX07 is the evaluation plan for a new AI feature) plus the measured-assistant lab. Pass: at least five exercises including EX07, and a lab where a worse prompt fails the pipeline and cost per conversation is visible per day.
