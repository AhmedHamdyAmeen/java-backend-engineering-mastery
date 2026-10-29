# SRA-021 · AI strategy and build vs buy — Lecture scripts

**Video:** 88 min · **Running case:** *Commerce 2030* — the group formed by Shop and FulfillCo has 25 engineering teams and plans a third-party seller marketplace, a five-country expansion, and doubled order volume each year for three years, while its earliest services approach end of life; you are the senior technical leader for the commerce product area.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRA-021-L01 · Finding real AI value (12 min)
**Goal:** separate AI uses that create value from those that only add cost and risk.

**Key points**
- Start from a business problem and a measure (conversion, handling time, listing quality), not from a model.
- Good fits: language-heavy tasks, ranking with fuzzy signals, drafting with human review.
- Poor fits: tasks with exact rules, zero error tolerance, or too little data.
- Count the full cost: inference, evaluation, monitoring, review effort, and incident risk.

**Show:** a scoring grid for AI ideas: value, feasibility, data readiness, risk, cost, and a verdict of pursue, pilot, or reject.

**Check:** What should an AI proposal start from? *(A business problem and a measure of value, not a model.)*

---

## SRA-021-L02 · Hosted, open-weight, or managed (12 min)
**Goal:** compare the three ways of obtaining model capability.

**Key points**
- Hosted model APIs: fastest start, pay per use, least control, data goes to the provider under its terms.
- Open-weight self-hosted: more control over data and cost at scale, but you operate GPUs, updates, and safety.
- Managed platforms: a middle path inside your cloud with enterprise controls, at some premium.
- Compare cost, control, latency, data handling, and quality on your own evaluation, not on benchmarks.

**Show:** a decision table with the three options against cost at three volumes, latency, data residency, quality on our test set, and operational burden. Verify current pricing and terms before recording.

**Check:** Why evaluate on your own data instead of public benchmarks? *(Benchmarks may not reflect your task, language, or data.)*

---

## SRA-021-L03 · Prompting, RAG, or fine-tuning (12 min)
**Goal:** pick the lightest technique that meets the quality bar.

**Key points**
- Prompting: instructions and examples; cheapest and fastest to change.
- Retrieval-augmented generation (RAG): fetch relevant documents and give them to the model; good for changing or private knowledge.
- Fine-tuning: adjusts model behavior or style from examples; needs data, evaluation, and maintenance.
- Escalate only when evaluation shows the lighter option is not enough.

**Show:** a flow: start with prompting and an evaluation set; if knowledge is missing add RAG; if style or format is inconsistent after that, consider fine-tuning, with the cost of each step.

**Check:** What is the usual order of escalation? *(Prompting, then retrieval, then fine-tuning, based on evaluation results.)*

---

## SRA-021-L04 · AI total cost of ownership and lock-in (12 min)
**Goal:** build a multi-year cost model and plan the exit.

**Key points**
- Drivers: tokens or GPU hours per request, requests per user, growth, evaluation, human review, and staffing.
- Prices and models change quickly; model scenarios, and verify current rates before use.
- Lock-in sits in prompts, fine-tunes, vector indexes, and provider-specific features.
- Keep an abstraction, an evaluation suite, and a second option to make switching affordable.

**Show:** a three-year cost sheet: usage assumptions, unit costs, caching savings, review effort, staffing, with a price-change sensitivity and an exit plan row.

**Check:** What helps you switch providers later? *(An abstraction layer and an evaluation suite that tests a new model quickly.)*

---

## SRA-021-L05 · Data foundations for AI (10 min)
**Goal:** show that AI quality depends on data ownership, quality, and access.

**Key points**
- RAG and fine-tuning use your data; unclear ownership and poor quality produce poor answers.
- Needs: current catalogs, documented sources, access controls, and freshness guarantees.
- Sensitive data requires classification before it goes near a model.
- Build the data contract and ownership first (SRA-004) and AI second.

**Show:** a readiness checklist per use case: data source, owner, freshness, quality checks, sensitivity class, access path.

**Check:** Why does AI strategy depend on data ownership? *(Without owners and quality, retrieved or training data is stale or wrong, and so are the answers.)*

---

## SRA-021-L06 · Demo: scoring ten AI ideas for the marketplace (15 min)
**Goal:** run a scoring session that prioritizes and rejects ideas; prepares SRA-021-LAB1.

**Steps**
1. Collect ten ideas: seller listing assistant, support assistant, search ranking, fraud explanation, price suggestions, auto-reply to reviews, and so on.
2. Score each on value, feasibility, data readiness, risk, and cost; capture assumptions.
3. Discuss with product, support, and legal; adjust scores openly.
4. Select a short list to pilot and explicitly reject at least one with reasons.
5. **Planned mistake:** rank by excitement and demo quality. Fix: require a business measure and an estimated cost for each idea before scoring.
6. Publish the portfolio with owners and next steps.

---

## SRA-021-L07 · Demo: hosted API vs self-hosted model, three-year cost (15 min)
**Goal:** model the cost trade-off between hosted and self-hosted; prepares SRA-021-LAB1.

**Steps**
1. Choose the use case, such as the support assistant, and define usage: requests per day, tokens per request, and yearly growth.
2. Model the hosted option: price per unit (verify current), caching, and price-change scenarios.
3. Model self-hosting: GPUs, utilization, operations staff, evaluation, upgrades, and redundancy.
4. Find the break-even volume and compare control and data-handling benefits.
5. **Planned mistake:** compare per-token price with GPU rental only. Fix: add engineers, idle capacity, redundancy, and upgrades, which move break-even sharply.
6. Recommend with a trigger for revisiting and an exit plan.
