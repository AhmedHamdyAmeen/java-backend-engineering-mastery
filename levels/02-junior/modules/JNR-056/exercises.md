# JNR-056 · Calling LLMs from Spring — Exercises and lab

## Lab
### JNR-056-LAB1 · AI helper for Shop
**Outcomes:** 1–5 · **Time:** ~3 h
Add a `ProductDescriptionAssistant` (or a natural-language product search) to Shop API behind an interface. The Spring AI implementation returns a validated record; a fake implementation is used in tests.

**Acceptance:**
- provider and model are set only in configuration
- the API key comes from the environment
- timeout and max-token limit are configured
- invalid model output is handled with a clear error or a fallback
- controller and service tests pass without network access

## Exercises (assessment: extend the helper with a new field and keep all tests deterministic)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-056-EX01 | 1 | Given a request with 400 input tokens and 150 output tokens, explain what is billed and how a lower `max_tokens` changes cost. |
| JNR-056-EX02 | 2 | Call a model with `ChatClient` using a system message and a templated user message; show where the provider is configured. |
| JNR-056-EX03 | 3 | Return a `Description` record with `.entity(...)` and reject results that fail Bean Validation. |
| JNR-056-EX04 | 4 | Add a streaming endpoint that returns pieces as server-sent events. |
| JNR-056-EX05 | 4 | Configure a timeout, a retry policy for transient errors, and a max-token limit; list which errors you retry. |
| JNR-056-EX06 | 5 | Extract an interface, write a fake, and test both the valid and the invalid-output path with no network. |

## Solutions
- **EX01** You pay for 400 input plus up to 150 output tokens; lowering the limit caps the output share of the cost (and may cut the reply short).
- **EX02** `chatClient.prompt().system("...").user(u -> u.text("... {name}").param("name", n)).call().content()`; provider and model in `application.yml` (property names per the Spring AI reference) and the starter dependency.
- **EX03** `.entity(Description.class)` then `validator.validate(d)`; if the set is not empty, throw an exception mapped to a clear error response.
- **EX04** `produces = TEXT_EVENT_STREAM_VALUE` returning `chatClient.prompt()...stream().content()`.
- **EX05** Retry timeouts, `429`, `5xx`; do not retry `400` or authentication errors.
- **EX06** `ProductDescriptionAssistant` interface; a fake returns fixed values or an invalid record; `@WebMvcTest` registers the fake as a test bean (verify the current mock/bean annotation for your Spring Boot version).

**Outcome 1** is also checked by quiz Q01 to Q03. Add a new field (for example `keywords`) to the record, validation, fake, and tests for the assessment.
