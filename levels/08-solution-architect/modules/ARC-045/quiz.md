# ARC-045 · AI solution architecture — Quiz

Outcomes: O1 reference architectures · O2 integrating with enterprise systems · O3 deployment options · O4 cost, latency, and fallbacks.

**Q01 (O1)** A customer asks questions answered by the current returns policy documents. The best fit is: A. Retrieval over enterprise content B. A model with no context C. An agent with refund rights D. A nightly batch
**Q02 (O1)** What is the main added risk when moving from retrieval to an agent with tools? A. Longer documents B. The system can take actions on enterprise data C. Smaller prompts D. No logs
**Q03 (O2)** How should the assistant read order data? A. Direct database account B. Copy of the ERP in the model prompt C. Through a user-scoped governed API D. Shared admin password
**Q04 (O2)** Who runs a tool the model requests? A. The model itself B. The provider C. The customer D. Your platform code
**Q05 (O2)** For a write action such as a refund, the safest design is: A. The model executes it freely B. Confirmation or human approval before execution C. No logging D. Open to all prompts
**Q06 (O3)** Which deployment option places a provider model inside your cloud network boundary? A. Public hosted API B. Self-hosted on laptops C. Private endpoint D. Browser plugin
**Q07 (O3)** Self-hosting mainly shifts to you: A. The provider's terms B. Operations, capacity, and update work C. Prompt writing only D. Nothing
**Q08 (O4)** The cost of the assistant should be estimated: A. Per request only B. Per conversation including all turns and growing history C. Per developer D. Per server only
**Q09 (O4)** When the model provider is down, a good fallback is: A. Show errors B. Route to the human queue or a static help page C. Retry forever D. Guess answers
**Q10 (O1)** Which is a common mistake listed for AI solution design? A. Human handover designed early B. Tool calls logged C. Cost estimated with volumes D. Letting the model query core systems directly

## Answers
Q01 A · Q02 B · Q03 C · Q04 D · Q05 B · Q06 C · Q07 B · Q08 B · Q09 B · Q10 D

## Practical part
Architecture defense for the Larkspur assistant: C4 container view, data flows, deployment choice, cost per conversation, and human handover. Pass: quiz at least 8/10, at least five of six exercises correct, and a defense in which no path lets the model reach core systems directly.
