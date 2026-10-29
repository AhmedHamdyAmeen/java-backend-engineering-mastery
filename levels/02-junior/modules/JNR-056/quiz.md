# JNR-056 · Calling LLMs from Spring — Quiz

Outcomes: O1 how a call works · O2 ChatClient · O3 structured output · O4 streaming, timeouts, budgets · O5 interface and fake.

**Q01 (O1)** A system message is used to: A. Hold the API key B. Pay for tokens C. Set the model's role and rules D. Stream output
**Q02 (O1)** Cost of a call mainly depends on: A. Tokens in and out B. The URL length C. The JSON field order D. The HTTP method
**Q03 (O1)** Same input twice to a model can give: A. Always identical text B. A compile error C. Only `404` D. Different text
**Q04 (O2)** Spring AI's `ChatClient` is used to: A. Call a model through a fluent API B. Create tables C. Run unit tests only D. Encrypt keys
**Q05 (O2)** Where should the provider and model be chosen? A. In configuration B. In every controller C. In the HTTP request from the user D. In the DTO
**Q06 (O3)** Why use structured output? A. It is cheaper by definition B. It removes the need for tokens C. It avoids fragile free-text parsing D. It disables timeouts
**Q07 (O3)** After mapping to a record, you should: A. Trust it fully B. Validate it before use C. Ignore it D. Store the raw text only
**Q08 (O4)** Streaming helps because: A. The total time shrinks to zero B. Tokens become free C. Output is always valid D. Users see the first words sooner
**Q09 (O4)** Which failure is reasonable to retry? A. Wrong API key B. Invalid request body C. A timeout or `429` D. A validation error in your code
**Q10 (O5)** Tests for the AI feature should: A. Call the real model every run B. Use a fake implementation behind the interface C. Be skipped D. Use production keys

## Answers
Q01 C · Q02 A · Q03 D · Q04 A · Q05 A · Q06 C · Q07 B · Q08 D · Q09 C · Q10 B

## Practical part
Six exercises `JNR-056-EX01` to `EX06` plus the AI-helper lab. Pass: at least five exercises and a lab meeting every acceptance item; the assessment extension (a new field) must keep all tests offline and deterministic.
