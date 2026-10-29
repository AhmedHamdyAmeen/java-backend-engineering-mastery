# SRC-021 · Designing reliable AI features — Exercises and lab

## Lab
### SRC-021-LAB1 · AI order support at 10×
**Outcomes:** 1–4 · **Time:** ~3 h
1. Design the order-support assistant for the 10× forecast with p95 latency, cost-per-conversation, and quality targets, allocated across retrieval, model calls, and tools.
2. Implement a fallback path and a model-routing rule.
3. Define SLOs combining availability, latency, and evaluated quality.
4. Inject a provider outage and a latency spike; run a load test; measure quality on the evaluation set before and after routing.
**Acceptance:** checkout and order tracking are unaffected by the outage; budgets met in a load test; quality measured on the evaluation set before and after routing.

## Exercises (design review; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| SRC-021-EX01 | 1 | Allocate a 6 s p95 budget and a cost-per-conversation target across retrieval, model call, and tools for the assistant. |
| SRC-021-EX02 | 1 | Estimate monthly cost at 10x conversations given token counts and a price; state assumptions. |
| SRC-021-EX03 | 2 | Design a fallback ladder with triggers and user messages for model timeout, provider outage, and quota exhaustion. |
| SRC-021-EX04 | 2 | Review a design where the assistant call sits inside the checkout transaction; fix it. |
| SRC-021-EX05 | 3 | Propose a routing rule and a cache for order-status and refund questions; list the risks of each. |
| SRC-021-EX06 | 4 | Write SLOs for the assistant including a quality SLI, and respond to an assessor constraint: cost per answer must be halved. |

## Solutions
- **EX01** For example retrieval 600 ms, prompt assembly 100 ms, model 4 s, tools 600 ms, margin 700 ms; cost split by tokens; include timeouts per stage.
- **EX02** Conversations x turns x (input + output tokens) x price per token; verify current pricing; include retrieval and retries; show a range.
- **EX03** Timeout: retry once then smaller model; outage: circuit opens, cached or FAQ answer, then honest "unavailable"; quota exhaustion: queue with limits, route to cheaper model, shed low-priority traffic.
- **EX04** Move it off the critical path: asynchronous endpoint, separate pool, timeout; checkout must not depend on model availability.
- **EX05** Routing: order-status via data lookup and small model, refunds to the large model; risk of misrouting measured on the evaluation set; cache exact-match answers with short TTL, avoid caching personal data across users.
- **EX06** SLOs: 99.5% of conversations get a response in 6 s p95, 90% of sampled answers meet the rubric, cost under budget. To halve cost: more routing to small model, shorter context, caching, output limits; re-evaluate quality and report the trade-off.

**Workplace evidence:** an AI feature you designed or hardened with explicit latency, cost, and fallback targets.
