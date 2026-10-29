# SRC-021 · Designing reliable AI features — Quiz

Outcomes: O1 latency, cost, quality budgets · O2 fallbacks · O3 routing, caching, streaming · O4 SLOs for non-deterministic features.

**Q01 (O1)** A checkout team proposes calling the model inside the checkout request. Best response? A. Approve B. Raise the timeout C. Keep model calls off the critical path D. Cache the checkout
**Q02 (O1)** Every model call should have: A. No limits B. A timeout, token limit, and retry or fallback policy C. Unlimited retries D. A bigger prompt
**Q03 (O1)** Cost per conversation depends mainly on: A. Tokens in and out and call count B. Screen size C. Number of engineers D. Log level
**Q04 (O2)** The provider is down. The assistant should: A. Fabricate an answer B. Block checkout C. Retry forever D. Fall back to cached, non-AI, or an honest unavailable state
**Q05 (O2)** To prevent model slowness from exhausting threads you use: A. Larger shared pool B. Isolation with a separate pool and circuit breaker C. No timeouts D. More retries
**Q06 (O3)** Streaming mainly improves: A. Perceived latency B. Total cost C. Quality D. Security
**Q07 (O3)** After routing easy questions to a smaller model you must: A. Only check cost B. Skip evaluation C. Evaluate quality on the evaluation set D. Remove the larger model
**Q08 (O3)** A risk of semantic caching is: A. Serving stale or another user's data B. Lower latency C. Lower cost D. Simpler code
**Q09 (O4)** An AI feature's SLO should include: A. Availability only B. Latency only C. Cost only D. Availability, latency, and evaluated quality
**Q10 (O4)** A quality SLI is typically: A. Server CPU B. Share of sampled answers meeting a rubric C. Number of tokens D. Request count

## Answers
Q01 C · Q02 B · Q03 A · Q04 D · Q05 B · Q06 A · Q07 C · Q08 A · Q09 D · Q10 B

## Practical part
Six design exercises `SRC-021-EX01` to `EX06` plus the lab with an injected provider outage and latency spike. Pass: quiz at least 8/10, at least five exercises correct, and a design review that holds up under an assessor-injected constraint (cost halved or quota cut).
