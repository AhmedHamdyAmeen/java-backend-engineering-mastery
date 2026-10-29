# SRC-021 · Designing reliable AI features — Lecture scripts

**Video:** 88 min · **Running case:** *Order Processing at 10×* — Shop Platform's order subsystem must handle a 10× growth forecast, a 99.95% availability commitment, and a 15-minute recovery objective.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRC-021-L01 · What makes AI features different to operate (10 min)
**Goal:** list how model-backed features differ from ordinary services.

**Key points**
- Outputs are non-deterministic and quality is a spectrum, not pass or fail.
- Latency is long and variable; cost scales with tokens, per call.
- The provider is an external dependency with quotas, rate limits, outages, and model changes.
- Quality can degrade silently when prompts, models, or data change.

**Show:** a comparison table of a normal REST dependency and an LLM call: latency, cost, determinism, failure modes.

**Check:** Why is "up" not enough for an AI feature? *(Answers can be wrong or slow while the service is technically up.)*

---

## SRC-021-L02 · Latency and cost budgets for model calls (12 min)
**Goal:** budget latency, cost, and quality across retrieval, model, and tools.

**Key points**
- Budget end to end: retrieval, prompt assembly, model time to first token and total, tool calls, post-processing.
- Cost per conversation: tokens in and out times price, plus retrieval and tool costs (verify current pricing before recording).
- Set a quality target measured on an evaluation set; budgets trade against quality.
- Every model call gets a timeout, a token limit, and a retry policy.

**Show:** a budget table: p95 latency, cost per conversation, and quality score per stage of the order-support assistant.

**Check:** What must every model call have? *(A timeout, a token limit, and a retry or fallback policy.)*

---

## SRC-021-L03 · Fallbacks and graceful degradation for AI (12 min)
**Goal:** keep the core journey alive when the model is not.

**Key points**
- Ladder: smaller model, cached answer, non-AI path (search or FAQ), honest "unavailable" state.
- Keep model calls off the critical path of checkout and order tracking.
- Use circuit breakers and bulkheads so model slowness cannot exhaust shared threads.
- Never fabricate an answer to hide failure; say what is unavailable.

**Show:** a fallback ladder diagram with trigger and user message per step.

**Check:** Where must a model call not sit? *(On the critical checkout path.)*

---

## SRC-021-L04 · Model routing, caching, and streaming (12 min)
**Goal:** use routing, caching, streaming, and request shaping to hit targets.

**Key points**
- Routing: send easy requests to a smaller, cheaper model and hard ones to a larger one; measure quality per route.
- Caching: exact-match and semantic caches for repeated questions; mind freshness and privacy.
- Streaming: improves perceived latency by showing partial output early.
- Request shaping: shorter prompts, limited context, output limits, batching, and rate-limit-aware queues.

**Show:** a routing rule: order-status questions go to the small model with a data lookup; refund disputes go to the larger model.

**Check:** What must you measure when you route to a cheaper model? *(Quality on the evaluation set, not just cost.)*

---

## SRC-021-L05 · SLOs for non-deterministic features (12 min)
**Goal:** write SLOs that include quality.

**Key points**
- Combine availability (usable response), latency (p95 time to first and last token), and evaluated quality.
- Quality SLI: share of sampled answers meeting a rubric or evaluation score; define sampling and judges explicitly.
- Add cost per conversation as an operational budget.
- Error budgets cover degraded modes too; decide what counts.

**Show:** an SLO sheet: 99.5% responses within 6 s, 90% rated acceptable on the sampled set, cost under budget.

**Check:** What extra SLI do AI features need beyond availability and latency? *(An evaluated quality measure.)*

---

## SRC-021-L06 · Demo: an order-support assistant surviving a provider outage (15 min)
**Goal:** design and test fallbacks; prepares SRC-021-LAB1.

**Steps**
1. Map the assistant's dependencies: model provider, retrieval, order API.
2. Define the fallback ladder and the timeouts.
3. **Planned mistake:** the assistant shares the checkout service's thread pool. Fix: isolate it with a separate pool and a circuit breaker.
4. Inject a provider outage in staging.
5. Verify checkout and tracking are unaffected and users see an honest message.
6. Record the failure behavior and alert.

---

## SRC-021-L07 · Demo: cutting cost per answer by routing easy questions to a smaller model (15 min)
**Goal:** reduce cost while holding quality; prepares SRC-021-LAB1.

**Steps**
1. Classify a sample of questions by difficulty and measure the baseline cost and quality.
2. Define a routing rule (simple classifier or rules).
3. **Planned mistake:** judge success by cost alone. Fix: run the evaluation set before and after; one category degraded.
4. Adjust the rule and add a fallback to the larger model on low confidence.
5. Re-measure cost per conversation and quality.
6. Document the rule, the evaluation results, and a review trigger.
