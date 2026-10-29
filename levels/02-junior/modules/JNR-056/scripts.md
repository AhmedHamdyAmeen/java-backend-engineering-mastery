# JNR-056 · Calling LLMs from Spring — Lecture scripts

**Video:** 74 min · **Analogy used throughout:** ordering from an expert by letter: you send a letter (messages) to a clerk (the model) who bills by the word (tokens), may reply slowly, and sometimes writes back something you did not ask for, so you check the reply before acting.
Format: **Goal** · **Key points** · **Show** · **Check**.

Version note: Spring AI's APIs evolve. Verify every class, method, and property name against the current Spring AI reference before recording.

---

## JNR-056-L01 · What happens in an LLM API call (10 min)
**Goal:** understand what your code sends and receives.

**Key points**
- An LLM API is an HTTP call: you send a list of **messages**, you get a reply message back.
- A **system** message sets the rules and role. **User** messages carry the request. Earlier assistant messages are context.
- **Model parameters** such as temperature (randomness) and a maximum output length shape the reply.
- Text is counted in **tokens** (word pieces). Cost and limits depend on input plus output tokens.
- Output is probabilistic: the same input can give different text, so never assume the format.

**Show**
```json
{ "model": "<configured>",
  "messages": [
    {"role":"system","content":"You write short product descriptions."},
    {"role":"user","content":"Wireless mouse, 2.4 GHz, black"} ],
  "max_tokens": 150 }
```

**Check:** What do you pay for? *(Tokens sent and tokens received.)*

---

## JNR-056-L02 · Spring AI concepts: ChatClient, prompts, advisors (12 min)
**Goal:** call a model through Spring AI.

**Key points**
- **Spring AI** is a Spring project that gives one API for several model providers.
- `ChatClient` has a fluent API: `prompt()`, `system(...)`, `user(...)`, `call()`.
- A **prompt template** fills placeholders, so prompts are not built by string concatenation.
- **Advisors** wrap calls to add behavior such as logging or memory; here we only name the idea.
- The provider and model come from configuration and the starter you add, not from your code.

**Show**
```java
String text = chatClient.prompt()
    .system("You write short product descriptions.")
    .user(u -> u.text("Describe: {name}, {features}").param("name", name).param("features", features))
    .call()
    .content();
```

**Check:** Where is the provider chosen? *(In configuration and dependencies, not in business code.)*

---

## JNR-056-L03 · Structured output to records, and validating it (12 min)
**Goal:** get typed data instead of free text.

**Key points**
- Parsing free text with string tricks breaks easily. Ask for structured output instead.
- Spring AI can map the reply into a Java record with `.entity(MyRecord.class)`; it adds format instructions to the prompt.
- The model may still return wrong or missing values. Treat the result as untrusted input.
- Validate with Bean Validation (`@NotBlank`, `@Size`) before use.
- On failure, return a clear error or a safe fallback; never pass bad output further.

**Show**
```java
record Description(@NotBlank String title, @Size(max = 300) String text) {}
Description d = chatClient.prompt().user(...).call().entity(Description.class);
validator.validate(d); // reject if violations
```

**Check:** Why validate model output? *(It is not guaranteed to follow your format or rules.)*

---

## JNR-056-L04 · Streaming responses (10 min)
**Goal:** send text to the client as it is produced.

**Key points**
- A long reply can take seconds. **Streaming** sends pieces as they are generated.
- Spring AI offers `.stream().content()`, which returns a reactive `Flux<String>` (one piece at a time).
- A Spring MVC endpoint can return it as server-sent events (`text/event-stream`); verify the exact setup before recording.
- Users see the first words sooner, though total time is the same.
- Structured output is awkward while streaming; stream plain text, validate whole results.

**Show**
```java
@GetMapping(value = "/describe/stream", produces = MediaType.TEXT_EVENT_STREAM_VALUE)
Flux<String> stream(@RequestParam String name) {
    return chatClient.prompt().user("Describe " + name).stream().content();
}
```

**Check:** What type carries the pieces? *(A `Flux<String>`.)*

---

## JNR-056-L05 · Timeouts, retries, and token budgets (10 min)
**Goal:** keep model calls from hurting your service or your bill.

**Key points**
- Model calls are slow and can fail. Set a connect and read **timeout**.
- **Retry** only transient failures (timeouts, `429`, `5xx`), a small number of times, with a growing delay.
- Set a **max output tokens** limit per request and limit input size too; this is your token budget.
- Cap user-provided text length before it reaches the prompt.
- Log token usage so cost can be watched; do not log secrets or private data.

**Show**
```yaml
# property names: verify for the chosen provider
app.ai.timeout: 10s
app.ai.max-tokens: 300
```

**Check:** Which failures deserve a retry? *(Transient ones: timeouts, `429`, `5xx`.)*

---

## JNR-056-L06 · Keys, configuration, and testing with a fake model (8 min)
**Goal:** keep secrets safe and tests deterministic.

**Key points**
- API keys come from environment variables, never from `application.yml` committed to Git.
- Reference the key as `${AI_API_KEY}` in configuration.
- Define an interface (`ProductDescriptionAssistant`); the Spring AI class implements it.
- In tests use a **fake** implementation that returns a fixed record. No network, no cost, same result every run.
- Test the invalid-output path with a fake that returns bad data.

**Show**
```java
interface ProductDescriptionAssistant { Description describe(ProductInfo info); }
class FakeAssistant implements ProductDescriptionAssistant {
    public Description describe(ProductInfo i) { return new Description("Test", "Fixed text"); }
}
```

**Check:** Why a fake in tests? *(Fast, free, offline, and deterministic.)*

---

## JNR-056-L07 · Demo: an AI product-description helper for Shop API (12 min)
**Goal:** build the helper end to end. Prepares JNR-056-LAB1.

**Steps**
1. Define `ProductDescriptionAssistant` and the `Description` record with validation annotations.
2. Add the Spring AI starter and set provider and model in configuration; the key comes from an environment variable.
3. Implement it with `ChatClient`, `.entity(Description.class)`, a timeout, and a max-token limit.
4. **Planned mistake:** the first version asks for plain text and splits it by newline; the model adds extra lines and parsing breaks. Fix: request structured output and validate it.
5. Add `POST /products/{id}/description-suggestion` that returns the record, or a Problem Details error for invalid output.
6. Write controller and service tests with the fake; confirm they pass offline.
