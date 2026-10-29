# JNR-021 · OpenAPI — Lecture scripts

**Video:** 50 min · **Analogy used throughout:** a restaurant menu: it lists every dish, what goes in it, and what you get, so customers can order without asking the chef.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## JNR-021-L01 · The OpenAPI specification (10 min)
**Goal:** read an OpenAPI document.

**Key points**
- **OpenAPI** is a standard, machine-readable description of an HTTP API, written in YAML or JSON.
- `info` names the API and its version. `servers` lists base URLs.
- `paths` lists URLs; each path has **operations** (`get`, `post`, ...).
- An operation lists parameters, a request body, and `responses` by status code.
- Reusable shapes live in `components/schemas` and are referenced with `$ref`.

**Show**
```yaml
openapi: 3.0.3
info: { title: Shop API, version: 1.0.0 }
paths:
  /products/{id}:
    get:
      parameters:
        - { name: id, in: path, required: true, schema: { type: integer } }
      responses:
        "200": { description: OK }
        "404": { description: Not found }
```

**Check:** Where do reusable schemas live? *(Under `components/schemas`.)*

---

## JNR-021-L02 · Generating docs from Spring (springdoc) (10 min)
**Goal:** get a spec and Swagger UI from existing code.

**Key points**
- **springdoc-openapi** reads your controllers and DTOs and builds the spec at run time. Verify the artifact name and version for your Spring Boot version before recording.
- The spec is served as JSON (commonly at `/v3/api-docs`).
- **Swagger UI** is a web page (commonly `/swagger-ui.html`) where you read and try endpoints.
- Annotations such as `@Operation` and `@Schema` add detail where the code alone is not enough.
- In production, decide whether the docs endpoints should be public.

**Show:** add the starter dependency, run the app, open the UI, and call `GET /products` with "Try it out".

**Check:** What is Swagger UI for? *(Reading and trying the API in a browser.)*

---

## JNR-021-L03 · Examples and error responses (10 min)
**Goal:** make the docs useful, not just generated.

**Key points**
- Add a short `description` to each operation and field.
- Add realistic **examples** for requests and responses so newcomers can copy them.
- Document the error responses (`400`, `404`, `409`) with the Problem Details shape.
- Undocumented errors force clients to guess.
- Use `@ApiResponse` on operations, or a shared configuration for common errors.

**Show**
```java
@Operation(summary = "Get a product")
@ApiResponse(responseCode = "404", description = "Product not found")
@GetMapping("/{id}")
ProductResponse get(@PathVariable long id) { ... }
```

**Check:** Why document `404`? *(Clients need to know what can go wrong and what it looks like.)*

---

## JNR-021-L04 · Code-first vs contract-first (10 min)
**Goal:** compare the two ways of producing a spec.

**Key points**
- **Code-first:** write controllers, generate the spec. Fast and always matches the code; the design can become an afterthought.
- **Contract-first:** write the spec first, then generate or hand-write code to match. Good for reviews and parallel work with client teams; needs discipline to keep code in sync.
- The main risk of both is docs drifting from behavior; check the spec in tests or in CI.
- Commit the spec to the repository so changes show up in code review.
- Many teams use code-first for internal APIs and contract-first for public or partner APIs.

**Show**
| Approach | Strength | Risk |
| --- | --- | --- |
| Code-first | Quick, matches code | Weak design review |
| Contract-first | Design agreed early | Code can drift |

**Check:** What is the shared risk of both? *(Docs drifting from actual behavior.)*

---

## JNR-021-L05 · Demo: from bare springdoc output to a usable API reference (10 min)
**Goal:** improve generated docs until a newcomer can use them. Prepares JNR-021-LAB1.

**Steps**
1. Open the bare Swagger UI: no descriptions, no examples, no errors.
2. Add `@Operation` summaries and `@Schema` descriptions with examples on the DTOs.
3. Document `400`, `404`, and `409` using the Problem Details shape.
4. **Planned mistake:** the docs say `200` but the code returns `201` on create. Fix: correct the annotation and add a test that checks the status.
5. Export the spec and commit it to the repository.
6. Ask a colleague to call every endpoint using only Swagger UI.
