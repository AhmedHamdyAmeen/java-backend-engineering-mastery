# Level 2 — Junior Backend Engineer: Interview Preparation

The questions most often asked in junior Java backend interviews, how to answer them, and exactly where in this course you learned and practiced each one.

**How to use this guide**
1. Read the question and answer it **out loud** before reading the answer. Interviews test explanation, not recognition.
2. If you struggle, go back to the module in **Learned in** and redo the lab in **Practiced in**.
3. Prepare the **Show it** line for every question: at this level interviewers expect you to point at code you wrote in the Shop API.

> **About "How often":** frequencies reflect commonly reported interview patterns for junior Java/Spring backend roles, not measured statistics. Check them against current job posts in your target market (the method from `BEG-004-LAB1`) and update this guide when the market moves.

---

## 1. What the market asks for — and where you proved it

Typical junior backend job posts list the skills below. The right-hand columns show where this course taught each one and which artifact proves it.

| Skill employers list | Learned in | Proven by |
| --- | --- | --- |
| Modern Java (records, streams, Optional) | JNR-001, BEG-036 | `JNR-001-LAB1` Shop Core v1 |
| Spring / Spring Boot | JNR-008 … JNR-016 | `JNR-013-LAB1` products feature, `JNR-CAP` |
| REST API design | JNR-017 … JNR-021 | `JNR-019-LAB1` catalog CRUD, `JNR-021-LAB1` OpenAPI |
| SQL, JPA / Hibernate | JNR-025 … JNR-034 | `JNR-029-LAB1`, `JNR-032-LAB1` N+1 fix |
| Transactions | JNR-031 | `JNR-031-LAB1` atomic checkout |
| Spring Security, JWT, OAuth 2.0 | JNR-035 … JNR-040 | `JNR-036-LAB1`, `JNR-039-LAB1` Keycloak |
| Secure coding (OWASP) | JNR-041, JNR-042 | `JNR-041-LAB1` vulnerable Shop |
| Unit and integration testing | JNR-016, JNR-043 … JNR-047 | `JNR-045-LAB1` Testcontainers suite |
| Docker | JNR-049, JNR-050 | `JNR-050-LAB1` one-command stack |
| CI/CD and deployment | JNR-051, JNR-052 | `JNR-051-LAB1` pipeline, `JNR-052-LAB1` live Shop |
| Git workflow and code review | JNR-053 | `JNR-053-LAB1` team sprint |
| Troubleshooting | JNR-054 | `JNR-054-LAB1` break the Shop |
| AI-assisted development | JNR-055 | `JNR-055-LAB1`, `AI-USE.md` in `JNR-CAP` |
| Integrating LLM APIs (Spring AI) | JNR-056, JNR-057 | `JNR-056-LAB1` AI helper in Shop API, `JNR-057-LAB1` |

**Your portfolio at the end of Level 2:** the deployed Shop API (`JNR-CAP`) with OpenAPI docs, a green CI pipeline, Testcontainers tests, `docker compose up`, and a `SECURITY.md`. Put the live URL and the repository on your CV.

## 2. How junior backend interviews usually run

| Round | What happens | What they check | Prepare with |
| --- | --- | --- | --- |
| Recruiter / phone screen | 20–30 min | Motivation, stack fit, communication | Q21, Q22 |
| Online test or take-home | Coding problems or a small Spring API | Working, tested, readable code | Q20, `JNR-019-LAB1` |
| Technical interview | Java, Spring, JPA, SQL, REST, security questions | Depth and correct vocabulary | Q1–Q19 |
| Live coding / pairing | Build or fix an endpoint, write a test | How you think and test | Q20, Q15 |
| Project / behavioral | Walk through your project, teamwork stories | Ownership, collaboration | Q21, Q22 |

---

## 3. Spring and Spring Boot

### Q1 · What are IoC and dependency injection, and why prefer constructor injection?
**How often:** Very common · **Round:** Technical

**How to answer:**
- **Inversion of Control:** objects do not create their collaborators; a container creates and wires them.
- **Dependency injection** is how Spring does it: dependencies are passed in, so classes depend on interfaces, not concrete implementations.
- **Constructor injection** makes dependencies explicit and `final`, guarantees a fully initialized object, works in plain unit tests without Spring, and exposes classes with too many dependencies.

```java
@Service
class OrderService {
    private final OrderRepository orders;
    private final PaymentGateway payments;

    OrderService(OrderRepository orders, PaymentGateway payments) { // no @Autowired needed
        this.orders = orders;
        this.payments = payments;
    }
}
```

**Common trap:** field injection with `@Autowired` — hides dependencies and forces Spring into every test.

**Learned in:** JNR-004, JNR-009
**Practiced in:** `JNR-009-LAB1`
**Show it:** Shop Core services wired by constructor, with the payment provider chosen by qualifier.

---

### Q2 · What bean scopes exist, and what is the risk of state in a singleton?
**How often:** Very common · **Round:** Technical

**How to answer:**
- Default scope is **singleton**: one instance per application context. Others: **prototype** (new instance per injection) and web scopes (**request**, **session**).
- Singletons are shared by all request threads, so **mutable fields are a race condition**. Keep services stateless; put per-request data in method parameters or local variables.
- Bonus: injecting a prototype into a singleton gives you one instance only, unless you use `ObjectProvider`.

**Learned in:** JNR-010
**Practiced in:** `JNR-010-LAB1`

---

### Q3 · How does Spring Boot auto-configuration work?
**How often:** Common · **Round:** Technical

**How to answer:**
- Starters bring dependencies; auto-configuration classes (listed in the `AutoConfiguration.imports` file of each module) create beans **conditionally** with annotations such as `@ConditionalOnClass`, `@ConditionalOnMissingBean`, and `@ConditionalOnProperty`.
- Your own bean of the same type wins because of `@ConditionalOnMissingBean`.
- To see what happened, run with `--debug` and read the conditions evaluation report.

**Learned in:** JNR-011
**Practiced in:** `JNR-011-LAB1`
**Show it:** "I overrode Boot's default JSON date format and could explain from the report why my bean replaced the default."

---

### Q4 · How do you handle validation and errors consistently in a REST API?
**How often:** Very common · **Round:** Technical

**How to answer:**
- Validate request DTOs at the edge with Jakarta Bean Validation (`@NotBlank`, `@Positive`, `@Valid` on the controller parameter); keep business rules in the domain.
- Map exceptions centrally with `@RestControllerAdvice`, returning one error shape — RFC 9457 **Problem Details** (`ProblemDetail`) — with the right status.
- Log the stack trace server-side; never send internal details to the client.

```java
@RestControllerAdvice
class ApiErrors {
    @ExceptionHandler(ProductNotFoundException.class)
    ProblemDetail notFound(ProductNotFoundException e) {
        return ProblemDetail.forStatusAndDetail(HttpStatus.NOT_FOUND, e.getMessage());
    }
}
```

**Learned in:** JNR-014, JNR-015
**Practiced in:** `JNR-014-LAB1`, `JNR-015-LAB1`

---

## 4. REST API design

### Q5 · Design the endpoints for a product catalog and cart. Which status codes do you return?
**How often:** Very common · **Round:** Technical, design

**How to answer:** resources and nouns, standard methods, precise status codes.
- `GET /products?category=…&page=0&size=20&sort=price,asc` → 200
- `GET /products/{id}` → 200 or 404
- `POST /products` → **201 Created** with a `Location` header; 400 on validation; 409 on duplicate SKU
- `PUT /products/{id}` (full replace) / `PATCH /products/{id}` (partial) → 200 or 204
- `DELETE /products/{id}` → 204
- Actions that aren't CRUD become resources or sub-resources: `POST /carts/{id}/checkout` → 201 with the created order.
- 401 = not authenticated; 403 = authenticated but not allowed.

**Common trap:** verbs in URLs (`/getProducts`) and unbounded list endpoints without pagination.

**Learned in:** JNR-018, JNR-019, JNR-020
**Practiced in:** `JNR-018-LAB1`, `JNR-019-LAB1`
**Show it:** your Shop API design table and the OpenAPI document.

---

### Q6 · What does idempotent mean? Which HTTP methods are idempotent, and how do you make a POST safe to retry?
**How often:** Very common · **Round:** Technical

**How to answer:**
- **Idempotent:** repeating the request has the same effect as sending it once. GET, PUT, DELETE (and HEAD, OPTIONS) are idempotent; POST is not; PATCH is not guaranteed.
- **Safe** methods (GET, HEAD) do not change state.
- It matters because clients and proxies retry after timeouts. To make `POST /orders` retry-safe, accept an **idempotency key** header, store it with the result, and return the stored result on a repeat.

**Learned in:** JNR-017
**Practiced in:** `JNR-017-LAB1`

---

### Q7 · Why use DTOs instead of returning JPA entities from controllers?
**How often:** Common · **Round:** Technical

**How to answer:**
- Entities expose your database structure as your API contract, so any schema change breaks clients.
- Serializing entities triggers lazy loading (N+1, `LazyInitializationException`) and can leak fields like password hashes.
- Binding request bodies to entities enables **mass assignment** (a client sets `role` or `price`).
- DTOs (often records) give a stable contract, per-use-case shapes, and validation in one place.

**Learned in:** JNR-013, JNR-020, JNR-041
**Practiced in:** `JNR-013-LAB1`, `JNR-020-LAB1`

---

## 5. Persistence: JPA, transactions, and SQL

### Q8 · Explain the JPA entity lifecycle and dirty checking.
**How often:** Common · **Round:** Technical

**How to answer:**
- States: **transient** (new, unknown to JPA) → **managed** (in the persistence context after `persist`/load) → **detached** (context closed) → **removed**.
- Managed entities are **dirty-checked**: at flush (usually commit), Hibernate compares them with their loaded snapshot and issues `UPDATE`s automatically — no `save()` needed inside a transaction.
- The persistence context is also a first-level cache: loading the same ID twice in one transaction returns the same object.

**Learned in:** JNR-027, JNR-028
**Practiced in:** `JNR-028-LAB1`
**Show it:** "I logged the SQL and explained every statement in a create-update-read sequence."

---

### Q9 · What is the N+1 query problem and how do you fix it?
**How often:** Very common · **Round:** Technical

**How to answer:**
- Loading N parents and then touching a lazy association on each issues 1 + N queries.
- Detect it from SQL logs or a query-count assertion in a test.
- Fix it per use case: **fetch join** (`JOIN FETCH`), **`@EntityGraph`**, a **DTO projection**, or batch fetching.

```java
@Query("select o from Order o join fetch o.lines where o.customer.id = :customerId")
List<Order> findWithLines(Long customerId);
```

**Common trap:** switching associations to `EAGER` — it moves the problem everywhere. And beware fetch-joining collections with pagination (Hibernate paginates in memory).

**Learned in:** JNR-032
**Practiced in:** `JNR-032-LAB1`
**Show it:** the order-history fix from 101 queries to 2, with the test that proves it.

---

### Q10 · Lazy vs eager loading — and why do you get `LazyInitializationException`?
**How often:** Very common · **Round:** Technical

**How to answer:**
- **Lazy** associations load on first access; **eager** load immediately. Defaults: `@ManyToOne`/`@OneToOne` eager, collections lazy — set `@ManyToOne(fetch = LAZY)` explicitly.
- The exception happens when a lazy association is touched **after the persistence context is closed** (e.g., in the controller or JSON serialization).
- Fix by loading what the use case needs inside the transaction (fetch join, entity graph, projection) and mapping to DTOs there — not by enabling Open Session in View.

**Learned in:** JNR-030, JNR-032
**Practiced in:** `JNR-032-LAB1`

---

### Q11 · How does `@Transactional` work? Explain rollback rules, propagation, and the self-invocation problem.
**How often:** Very common · **Round:** Technical

**How to answer:**
- Spring wraps the bean in a **proxy** that starts a transaction before the method and commits or rolls back after it.
- **Rollback rules:** by default it rolls back on **unchecked** exceptions and errors, *not* on checked exceptions — use `rollbackFor` if needed.
- **Propagation:** `REQUIRED` (default) joins an existing transaction or starts one; `REQUIRES_NEW` suspends it and starts an independent one.
- **Self-invocation:** calling a `@Transactional` method from another method **in the same class** bypasses the proxy, so no transaction starts. Move the method to another bean.
- Put transactions on service methods; keep them short; no remote calls (payment APIs) inside.

**Common trap:** catching an exception inside the transactional method and not rethrowing — nothing rolls back.

**Learned in:** JNR-031
**Practiced in:** `JNR-031-LAB1`
**Show it:** atomic checkout (stock + order) and the self-invocation bug you fixed.

---

### Q12 · How do you guarantee unique emails or SKUs when two requests arrive at the same time?
**How often:** Common · **Round:** Technical

**How to answer:**
- "Check, then insert" in Java is a race: both requests pass the check.
- Put a **unique constraint** in the database (the only place that sees both), catch the violation (`DataIntegrityViolationException`), and return **409 Conflict**.
- Add indexes for foreign keys and frequent lookups; verify with `EXPLAIN`.

**Learned in:** JNR-034
**Practiced in:** `JNR-034-LAB1`

---

### Q13 · How do you evolve a database schema in a team? Why not `ddl-auto=update`?
**How often:** Common · **Round:** Technical

**How to answer:**
- Use versioned migrations (**Flyway** or Liquibase) committed with the code and applied on startup or in the pipeline.
- Never edit an applied migration; add a new one.
- `ddl-auto=update` cannot rename, cannot backfill data, behaves differently per environment, and leaves no history. Use `ddl-auto=validate` so mappings are checked against the migrated schema.

**Learned in:** JNR-033
**Practiced in:** `JNR-033-LAB1`

---

## 6. Security

### Q14 · How does Spring Security work, and what is the difference between 401 and 403?
**How often:** Very common · **Round:** Technical

**How to answer:**
- Spring Security is a chain of servlet **filters** in front of your controllers. You configure it with a `SecurityFilterChain` bean: authentication mechanism (session, JWT resource server) plus authorization rules per request matcher, and `@PreAuthorize` for method-level rules.
- **401 Unauthorized:** not authenticated (missing or invalid credentials). **403 Forbidden:** authenticated but not allowed.

```java
@Bean
SecurityFilterChain api(HttpSecurity http) throws Exception {
    return http
        .authorizeHttpRequests(auth -> auth
            .requestMatchers(HttpMethod.GET, "/products/**").permitAll()
            .requestMatchers("/admin/**").hasRole("ADMIN")
            .anyRequest().authenticated())
        .oauth2ResourceServer(rs -> rs.jwt(Customizer.withDefaults()))
        .build();
}
```

**Learned in:** JNR-036, JNR-040
**Practiced in:** `JNR-036-LAB1`
**Show it:** your access-matrix tests for anonymous, customer, and admin.

---

### Q15 · What is a JWT, and how should a server validate it? Sessions or tokens?
**How often:** Very common · **Round:** Technical

**How to answer:**
- A JWT is `header.payload.signature`, Base64URL-encoded. The payload (claims) is **readable by anyone** — it is signed, not encrypted.
- Validate: signature with the expected key and **algorithm** (never accept `none`), `exp`/`nbf`, `iss`, and `aud`. Then map claims to authorities.
- Sessions: server-side state, easy revocation, cookie-based (needs CSRF protection). Tokens: stateless and easy across services, but hard to revoke — keep access tokens short-lived and use refresh tokens.

**Common trap:** putting personal data or secrets in claims.

**Learned in:** JNR-038
**Practiced in:** `JNR-038-LAB1`

---

### Q16 · Explain OAuth 2.0 and OIDC. Which flow would you use for a web app, and which for service-to-service?
**How often:** Common · **Round:** Technical

**How to answer:**
- **OAuth 2.0** delegates API access: roles are resource owner, client, authorization server, resource server.
- **OIDC** adds login on top: an **ID token** says who the user is.
- Web or mobile app with a user: **authorization code flow with PKCE**. Service-to-service with no user: **client credentials**. Implicit and password grants are deprecated.
- Your API is a **resource server**: it only validates access tokens issued by the authorization server.

**Learned in:** JNR-039
**Practiced in:** `JNR-039-LAB1`

---

### Q17 · How do you store passwords, and what is an IDOR vulnerability?
**How often:** Very common · **Round:** Technical

**How to answer:**
- Passwords: hash with a slow, salted, adaptive algorithm — **bcrypt** or **Argon2** via `PasswordEncoder`. Never encrypt (reversible) or use fast general-purpose hashes (MD5, the SHA family). Throttle failed logins.
- **IDOR / broken object-level authorization:** the API returns an object just because the client knows its ID (`GET /orders/1043`). Fix: check **ownership** on every access, ideally in the query itself (`findByIdAndCustomerId`), and return 404 to avoid leaking existence.
- Broken access control is the top OWASP risk — name it.

**Learned in:** JNR-037, JNR-040, JNR-041
**Practiced in:** `JNR-037-LAB1`, `JNR-040-LAB1`, `JNR-041-LAB1`
**Show it:** the test where customer A cannot read customer B's order.

---

## 7. Testing and delivery

### Q18 · Unit vs integration tests in a Spring app — what do you mock, and why Testcontainers?
**How often:** Very common · **Round:** Technical, live coding

**How to answer:**
- **Unit tests:** a class in isolation, plain JUnit, collaborators mocked or faked with **Mockito**. Fast; most of your tests.
- **Slice tests:** `@WebMvcTest` (controller + MockMvc) or `@DataJpaTest` (repositories).
- **Integration tests:** `@SpringBootTest` against real infrastructure. **Testcontainers** runs real PostgreSQL in Docker, so you test the same SQL, constraints, and migrations as production — H2 behaves differently.
- Mock what you own at boundaries (payment gateway); don't mock value objects or the class under test.

```java
@Test
void declinedPaymentCancelsOrder() {
    when(payments.authorize(any())).thenReturn(PaymentResult.declined());
    var order = service.placeOrder(cartWithOneItem());
    assertThat(order.status()).isEqualTo(OrderStatus.CANCELLED);
    verify(inventory).release(order.id());
}
```

**Learned in:** JNR-016, JNR-043, JNR-044, JNR-045
**Practiced in:** `JNR-044-LAB1`, `JNR-045-LAB1`, `JNR-046-LAB1`
**Show it:** the checkout journey matrix and a suite that runs green on a clean machine with only Docker.

---

### Q19 · How would you containerize a Spring Boot app and set up CI/CD for it?
**How often:** Very common · **Round:** Technical

**How to answer:**
- **Dockerfile:** multi-stage build (JDK to build, JRE to run), non-root user, pinned base image tag, no secrets baked in; configuration through environment variables.
- **Local:** `docker compose` with the app and PostgreSQL, health checks for startup order.
- **CI (e.g., GitHub Actions):** on every PR, build and run all tests (including Testcontainers); block merge on failure. On merge to `main`, build and push a version-tagged image.
- **CD:** deploy the image, check readiness, and be able to roll back to the previous tag.

```dockerfile
FROM eclipse-temurin:25-jdk AS build
WORKDIR /app
COPY . .
RUN ./mvnw -q package -DskipTests

FROM eclipse-temurin:25-jre
RUN useradd --system app
USER app
COPY --from=build /app/target/shop-api.jar /app.jar
ENTRYPOINT ["java", "-jar", "/app.jar"]
```

(Use your project's baseline LTS version tag.)

**Learned in:** JNR-049, JNR-050, JNR-051, JNR-052
**Practiced in:** `JNR-049-LAB1`, `JNR-051-LAB1`, `JNR-052-LAB1`
**Show it:** the PR that could not merge because a test failed, and your documented rollback.

---

## 8. Live coding

### Q20 · Live coding: build `POST /products` with validation, a 201 response, and a test.
**How often:** Very common · **Round:** Live coding, take-home

**How to answer:** narrate the layers and test as you go.
1. Request DTO as a record with validation annotations.
2. Controller delegates to the service and returns **201 + Location**.
3. Service checks business rules (duplicate SKU → 409 via a custom exception mapped in the advice).
4. A `@WebMvcTest` for success and validation failure.

```java
record CreateProduct(@NotBlank String name, @NotBlank String sku, @Positive BigDecimal price) {}

@PostMapping("/products")
ResponseEntity<ProductResponse> create(@Valid @RequestBody CreateProduct request) {
    ProductResponse created = products.create(request);
    return ResponseEntity.created(URI.create("/products/" + created.id())).body(created);
}

@Test
void rejectsBlankName() throws Exception {
    mvc.perform(post("/products").contentType(APPLICATION_JSON)
            .content("""
                {"name": "", "sku": "A-1", "price": 9.99}"""))
       .andExpect(status().isBadRequest());
}
```

**Common trap:** coding silently. Say what you are doing, what you are skipping because of time, and how you would test it.

**Learned in:** JNR-014, JNR-016, JNR-019
**Practiced in:** `JNR-019-LAB1`, `JNR-016-LAB1`

---

## 9. Your project and behavior

### Q21 · Walk me through your Shop API. What would you do differently?
**How often:** Asked in almost every interview · **Round:** Screen, project

**How to answer (4–5 minutes):**
1. **What it does:** catalog, cart, orders, payments behind an interface, roles.
2. **Architecture:** modular monolith packaged by feature; controller → service → repository; DTOs at the edge. Show the diagram.
3. **Key decisions:** checkout in one transaction with stock that can never go negative (constraint + test); no remote call inside the transaction; Keycloak tokens validated as a resource server.
4. **Quality and delivery:** Testcontainers suite, CI that blocks merges, deployed instance with health checks and rollback.
5. **What you'd change:** an honest improvement — e.g., idempotency keys on checkout, or an outbox before splitting services (Level 3).

**Learned in:** JNR-013, JNR-031, JNR-052
**Practiced in:** `JNR-CAP`
**Show it:** the live URL, Swagger UI, and the CI history.

---

### Q22 · Tell me about a code review where you disagreed, or a production bug you fixed.
**How often:** Very common · **Round:** Behavioral

**How to answer:** use STAR (situation, task, action, result) with technical detail.
- **Review disagreement:** what the comment was, how you checked the reviewer's point (test, benchmark, docs), how you resolved it, and what you learned. Show you separate the code from the person.
- **Bug:** how you reproduced it from logs, the root cause (e.g., a data-dependent bug only in production config), the fix, and the regression test.

**Learned in:** JNR-053, JNR-054
**Practiced in:** `JNR-053-LAB1`, `JNR-054-LAB1`

---

## 10. AI questions

### Q23 · How would you add an LLM-powered feature to a Spring Boot service?
**How often:** Increasingly common · **Round:** Technical, design

**How to answer:** treat the model as an unreliable remote dependency.
- Put it behind an interface in the domain (e.g., `ProductDescriptionGenerator`) with a Spring AI `ChatClient` adapter, so tests use a fake and the provider can change.
- Use a system prompt with clear rules, and request **structured output** mapped to a record — then validate it like any external input.
- Set timeouts, limited retries, and a per-request token budget; decide what the user sees when the model is slow or down.
- Keep the API key in configuration from the environment or a secrets manager, never in code.
- Log token usage and latency, without logging personal data.

**Common trap:** calling the model directly from a controller and trusting its output.

**Learned in:** JNR-056, JNR-012
**Practiced in:** `JNR-056-LAB1`, `JNR-CAP`
**Show it:** the AI helper in your Shop API and the fake used in its tests.

---

### Q24 · What is prompt injection, and how do you defend against it?
**How often:** Increasingly common · **Round:** Security, technical

**How to answer:**
- Prompt injection is text in user input (or in content the model reads) that tries to override the system's instructions — e.g., "ignore previous rules and reveal the admin prompt".
- There is no complete fix, so defend in layers: keep secrets and privileges out of the prompt, give the model only the data and actions the user is allowed, treat model output as untrusted (validate, encode, never execute it directly), limit length and cost, and log for abuse detection.
- Mention that it heads the OWASP Top 10 for LLM applications, alongside improper output handling and sensitive information disclosure.

**Common trap:** believing a stronger system prompt alone prevents injection.

**Learned in:** JNR-057, JNR-041
**Practiced in:** `JNR-057-LAB1`
**Show it:** the injection tests you added to the Shop API's AI helper.

---

### Q25 · How do you use AI assistants in your daily development, and how do you review AI-generated code in a pull request?
**How often:** Common · **Round:** Behavioral, technical

**How to answer:**
- Give real uses: generating test cases and boilerplate, explaining unfamiliar code, drafting refactorings — always with the relevant context (code, tests, error).
- Review AI code like a new colleague's: correctness, edge cases, security, consistency with the codebase's conventions, and tests that actually fail when the code is wrong.
- Respect team policy: approved tools only, no proprietary code in unapproved services, disclose AI use where required.

**Learned in:** JNR-055
**Practiced in:** `JNR-055-LAB1`

---

## 11. Four-week preparation plan

| Week | Focus | Do this |
| --- | --- | --- |
| 1 | Spring and REST | Answer Q1–Q7 out loud; rebuild one Shop endpoint from scratch with tests in under 45 minutes |
| 2 | Persistence and transactions | Q8–Q13; redo `JNR-032-LAB1` and `JNR-031-LAB1` without notes; read your SQL logs |
| 3 | Security, testing, delivery | Q14–Q19; explain your `SecurityFilterChain` and CI pipeline line by line |
| 4 | Live coding and project | Q20 timed twice; rehearse Q21–Q22; two mock interviews using the Level 2 interview simulation |

**Ready when:** you can answer every question here without notes, build a validated and tested endpoint live in under 45 minutes while talking, and explain every design decision in your Shop API — including the ones you would change.
