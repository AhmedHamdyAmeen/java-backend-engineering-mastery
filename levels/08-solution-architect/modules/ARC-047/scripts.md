# ARC-047 · AI vendor and model evaluation — Lecture scripts

**Video:** 70 min · **Running case:** *Larkspur Retail* — a mid-size retailer with 120 stores and a dated on-premises web shop; you are the solution architect for a new platform integrated with the existing ERP and CRM, now choosing how to power its AI assistant.
Format: **Goal** · **Key points** · **Show** · **Check**.

Note: model names, versions, and prices change quickly; verify before recording any specific figure.

---

## ARC-047-L01 · Evaluating AI vendors and models (12 min)
**Goal:** define the criteria for choosing an AI vendor or model and weight them with stakeholders.

**Key points**
- Core criteria: quality on your own tasks, latency, cost, data terms (residency, retention, training use), security, support and roadmap, and exit.
- Separate vendor questions (terms, support, stability, sub-processors) from model questions (quality, speed, context size, tool use).
- Agree weights with stakeholders before scoring; security and data terms may be pass/fail gates, not weighted points.
- Include operating effort: a self-hosted open-weight model needs GPUs, patching, and skilled people.
- Reuse the vendor-evaluation method from ARC-040; the AI-specific part is how quality is measured.

**Show:** a criteria table for Larkspur: criterion, gate or weighted, weight, how measured, evidence source; two hosted providers and one self-hosted open-weight model as columns.

**Check:** Which criteria might be gates instead of weighted points? *(Data terms and security requirements, which must be met regardless of score.)*

---

## ARC-047-L02 · Benchmarks vs your own evaluations (12 min)
**Goal:** explain why public benchmarks are not enough and describe a task-specific evaluation set.

**Key points**
- Public benchmarks test general skills on public tasks; your tasks, data, language, and tone differ, and models may have seen benchmark content.
- Rank on a leaderboard does not predict your result on your questions or your cost and latency.
- Build an evaluation set from real cases: questions, expected answers or criteria, and tricky cases (edge, out-of-scope, adversarial).
- Score with a rubric: correct, grounded in sources, safe, appropriate tone; use human review and, where trusted, a model as judge, spot-checked by humans.
- Version the set, keep it private, and rerun it when models or prompts change.

**Show:** an evaluation record: id, question, source documents, expected answer or rubric, category (order status, returns policy, out-of-scope), difficulty, pass criteria.

**Check:** Why is a leaderboard rank not enough? *(It measures general public tasks, not your questions, data, cost, or latency.)*

---

## ARC-047-L03 · AI proofs of concept (10 min)
**Goal:** run a time-boxed proof of concept (PoC) that answers the riskiest questions.

**Key points**
- Start from the riskiest assumptions: can it answer from our documents accurately, resist injection, meet latency, stay within cost?
- Time-box (for example 3-4 weeks), define success criteria beforehand, and name who decides at the end.
- Use real data (with approval and masking) and real question styles, not toy examples.
- Test failure modes: out-of-scope questions, conflicting sources, attacks, provider outage.
- Output: results against criteria, cost per conversation measured, risks, and a recommendation, not a demo reel.

**Show:** a PoC charter: questions to answer, success thresholds, data used, tests, timeline, decision owner, and exit if thresholds are missed.

**Check:** What makes a PoC useful for a decision? *(Pre-agreed success criteria on the riskiest questions, using realistic data.)*

---

## ARC-047-L04 · Multi-year AI cost and exit planning (10 min)
**Goal:** compare total cost over several years including usage growth and switching.

**Key points**
- Usage-based pricing grows with adoption: model cost as conversations times tokens, with growth scenarios and peaks; verify prices before recording.
- Add the other costs: retrieval, evaluation, monitoring, integration, people, support, and for self-hosting, hardware and operations.
- Price changes and model deprecations happen: include a switching cost and a periodic re-evaluation.
- Exit plan: keep prompts, evaluation sets, and retrieved data portable; use an abstraction layer; know how data is returned or deleted.
- Show best, expected, and worst scenarios so finance sees the range.

**Show:** a three-year table for Larkspur: year, conversations per month, cost per conversation, platform and people cost, switching reserve, for each of the three approaches under expected growth.

**Check:** Why include switching cost in the model? *(Models and prices change, so leaving a vendor must be affordable and planned.)*

---

## ARC-047-L05 · Demo: scoring three AI vendors for Larkspur (14 min)
**Goal:** score two hosted providers and one self-hosted open-weight model for the Larkspur assistant. This prepares ARC-047-LAB1.

**Steps**
1. Agree gates and weights with the role-played security officer and head of customer service: data terms and security as gates; quality, cost, latency, exit as weighted.
2. Apply the gates from the terms review: one hosted provider needs a configuration change for retention; record it as a condition.
3. **Planned mistake:** pick the provider with the top public leaderboard rank for the quality score. Fix: use the results from the evaluation set run on all three approaches.
4. Fill the scoring matrix with measured quality, latency, estimated cost per conversation, and the operating effort for the self-hosted option.
5. Run a weight sensitivity check: if cost is weighted higher, does the ranking change?
6. Write the recommendation with conditions and the exit plan; verify prices and model versions before recording.

**Check:** What was the planned mistake? *(Using public leaderboard rank instead of results on the task-specific evaluation set.)*

---

## ARC-047-L06 · Demo: building a 50-question evaluation set from support tickets (12 min)
**Goal:** build a first 50-question evaluation set from Larkspur support tickets. This prepares ARC-047-LAB1.

**Steps**
1. Sample recent tickets across categories (order status, returns, delivery, store opening hours, loyalty), with privacy approval.
2. Remove personal data (names, addresses, card digits) and rewrite each into a clean question with the information the assistant would have.
3. **Planned mistake:** write all 50 questions that the knowledge base answers easily. Fix: add about a fifth as hard cases: out-of-scope, ambiguous, conflicting policy, a prompt-injection attempt, and a request needing a human.
4. For each question record the expected answer or rubric and the source document.
5. Have two reviewers check a sample for agreement; resolve disagreements and fix unclear rubrics.
6. Store the set versioned and private, run the baseline, and record the results for use in the lab.

**Check:** What was the planned mistake? *(Including only easy questions and no hard or out-of-scope cases.)*
