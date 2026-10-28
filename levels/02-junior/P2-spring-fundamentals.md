# JNR-P2 — Spring Framework Fundamentals

**Phase goal:** the learner understands what Spring does for them — dependency injection, the container, and Boot's auto-configuration — and builds a correctly layered, validated, tested Spring Boot application.

**Running project:** *Shop API* — the Spring Boot application that becomes the Junior capstone. This phase creates its skeleton with an in-memory repository; persistence arrives in JNR-P4.

**Phase total:** ~9.1 h video · ~21 h practice · `version:` current Spring Boot major

---

### JNR-008 · Spring ecosystem
`n: 62` · **Video:** 40 min · **Practice:** 1 h

**Prerequisites:** JNR-002

**Learning outcomes** — the learner can:
1. Distinguish Spring Framework, Spring Boot, Spring Data, and Spring Security and state what each adds.
2. Explain what problem Spring solves compared with wiring objects by hand.
3. Generate a project with Spring Initializr and identify its parts.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-008-L01 | Why frameworks exist | 7 |
| JNR-008-L02 | The Spring family | 10 |
| JNR-008-L03 | Spring Initializr walkthrough | 8 |
| JNR-008-L04 | Reading Spring's documentation | 5 |
| JNR-008-L05 | Demo: first Spring Boot app from Initializr to running endpoint | 10 |

**Lab** — `JNR-008-LAB1` *Shop API skeleton:* generate the project with Web, Validation, and Actuator; run it; hit `/actuator/health`. Acceptance: runs from the terminal with `./mvnw spring-boot:run`.

**Common mistakes:** adding every starter "just in case".

**Assessment:** quiz.

**Career relevance:** orientation for the rest of the level.

---

### JNR-009 · IoC and DI
`n: 63` · **Video:** 74 min · **Practice:** 3 h

**Prerequisites:** JNR-004, JNR-008

**Learning outcomes** — the learner can:
1. Explain inversion of control and dependency injection, first without Spring.
2. Use constructor injection and explain why it beats field injection.
3. Resolve ambiguity between multiple implementations with `@Primary` and `@Qualifier`.
4. Describe the bean lifecycle (instantiation, injection, initialization, destruction).

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-009-L01 | Wiring by hand: the problem | 8 |
| JNR-009-L02 | Inversion of control | 8 |
| JNR-009-L03 | Constructor injection | 10 |
| JNR-009-L04 | Multiple implementations | 10 |
| JNR-009-L05 | Bean lifecycle and callbacks | 8 |
| JNR-009-L06 | Circular dependencies and how to avoid them | 6 |
| JNR-009-L07 | Demo: wiring Shop Core by hand, then with Spring | 12 |
| JNR-009-L08 | Demo: diagnosing an ambiguous-bean startup failure | 12 |

**Lab** — `JNR-009-LAB1` *Inject Shop Core:* register Shop Core's services and the pricing strategies as beans; select the payment provider by qualifier. Acceptance: no `new` for collaborators inside services; no field injection.

**Common mistakes:** `@Autowired` on fields; services that look up beans from the context; circular dependencies "fixed" with `@Lazy`.

**Assessment:** explain a DI wiring diagram and fix an ambiguous-bean failure.

**Career relevance:** the core of every Spring application; enables mocking (JNR-044).

---

### JNR-010 · Spring container
`n: 64` · **Video:** 55 min · **Practice:** 2 h

**Prerequisites:** JNR-009

**Learning outcomes** — the learner can:
1. Explain the `ApplicationContext` and how beans are discovered by component scanning.
2. Choose between `@Component`, `@Service`, `@Repository`, `@Controller`, and `@Bean` methods in `@Configuration` classes.
3. Choose singleton or prototype scope and explain the thread-safety implication of singletons.
4. Diagnose a bean that was not found because of package layout.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-010-L01 | The ApplicationContext | 8 |
| JNR-010-L02 | Component scanning and stereotypes | 10 |
| JNR-010-L03 | `@Configuration` and `@Bean` | 10 |
| JNR-010-L04 | Bean scopes | 8 |
| JNR-010-L05 | Stateless singletons and thread safety | 9 |
| JNR-010-L06 | Demo: injecting a `Clock` to test time-dependent logic | 10 |

**Lab** — `JNR-010-LAB1` *Third-party beans:* register a third-party `Clock` and currency client with `@Bean`; inject `Clock` to make time-dependent logic testable. Acceptance: no static `now()` calls in services.

**Common mistakes:** mutable state in singleton services; main class in the wrong package.

**Assessment:** "why is this bean missing?" debugging exercise.

**Career relevance:** concurrency awareness (MID-004) starts with stateless singletons.

---

### JNR-011 · Spring Boot
`n: 65` · **Video:** 74 min · **Practice:** 2 h

**Prerequisites:** JNR-010

**Learning outcomes** — the learner can:
1. Explain starters and how auto-configuration decides what to create (conditions).
2. Read the conditions evaluation report to see why something was or was not configured.
3. Override an auto-configured bean.
4. Describe the embedded server and build an executable JAR.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-011-L01 | What Boot adds to Spring | 8 |
| JNR-011-L02 | Starters | 7 |
| JNR-011-L03 | Auto-configuration and conditions | 12 |
| JNR-011-L04 | Overriding defaults | 8 |
| JNR-011-L05 | Embedded servers and executable JARs | 8 |
| JNR-011-L06 | Project structure conventions | 7 |
| JNR-011-L07 | Demo: reading the conditions evaluation report | 12 |
| JNR-011-L08 | Demo: overriding Jackson's auto-configuration | 12 |

**Lab** — `JNR-011-LAB1` *Under the hood:* run with `--debug`, find three auto-configurations that applied and one that did not, and explain why; override the default JSON date format. Acceptance: written explanation matches the report.

**Common mistakes:** treating auto-configuration as magic; excluding auto-configurations blindly.

**Assessment:** explain the startup sequence of the Shop API.

**Career relevance:** troubleshooting configuration issues in real services.

---

### JNR-012 · Configuration management
`n: 66` · **Video:** 50 min · **Practice:** 2 h

**Prerequisites:** JNR-007, JNR-011

**Learning outcomes** — the learner can:
1. Configure the application with `application.yml` and profile-specific files.
2. Bind configuration to typed, immutable `@ConfigurationProperties` records.
3. Validate configuration at startup so the app fails fast on bad values.
4. Explain Spring's property-source precedence.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-012-L01 | `application.yml` and profiles | 10 |
| JNR-012-L02 | Typed configuration with `@ConfigurationProperties` | 12 |
| JNR-012-L03 | Validating configuration | 8 |
| JNR-012-L04 | Property-source precedence | 10 |
| JNR-012-L05 | Demo: typed, validated `ShopProperties` that fail fast | 10 |

**Lab** — `JNR-012-LAB1` *Shop settings:* `ShopProperties` record (currency, tax rate, page-size limits) validated at startup; `dev` and `prod` profiles. Acceptance: invalid config prevents startup with a clear message.

**Common mistakes:** `@Value` scattered everywhere; secrets in `application.yml`.

**Assessment:** lab check plus precedence quiz.

**Career relevance:** deployment configuration (JNR-052).

---

### JNR-013 · Layered architecture
`n: 67` · **Video:** 79 min · **Practice:** 4 h

**Prerequisites:** BEG-027, JNR-011

**Learning outcomes** — the learner can:
1. Assign responsibilities to controller, service, repository, and domain layers.
2. Separate API DTOs from domain/entity models and map between them.
3. Organize code by feature with layers inside each feature.
4. Write a minimal `@RestController` that delegates to a service.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-013-L01 | Why layers | 8 |
| JNR-013-L02 | Controllers: the HTTP edge | 10 |
| JNR-013-L03 | Services: business logic and orchestration | 10 |
| JNR-013-L04 | Repositories: data access behind an interface | 8 |
| JNR-013-L05 | DTOs vs domain models | 12 |
| JNR-013-L06 | Package by feature, layer within | 7 |
| JNR-013-L07 | Demo: building the products feature layer by layer | 12 |
| JNR-013-L08 | Demo: separating DTOs from domain models | 12 |

**Lab** — `JNR-013-LAB1` *Products feature:* `GET /products` and `GET /products/{id}` through controller → service → in-memory repository, returning DTOs. Acceptance: controller contains no business logic; domain objects never serialized directly.

**Common mistakes:** fat controllers; services that return `ResponseEntity`; one DTO reused for everything.

**Assessment:** layering review of a provided feature.

**Career relevance:** the "established architecture" the Junior gate asks the learner to work within; hexagonal architecture (MID-059).

---

### JNR-014 · Validation
`n: 68` · **Video:** 50 min · **Practice:** 2 h

**Prerequisites:** JNR-013

**Learning outcomes** — the learner can:
1. Validate request DTOs with Jakarta Bean Validation annotations and `@Valid`.
2. Write a custom constraint annotation and validator.
3. Use validation groups or separate DTOs for create vs update.
4. Distinguish input validation (at the edge) from business-rule validation (in the domain).

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-014-L01 | Validating at the edge | 8 |
| JNR-014-L02 | Built-in constraints | 10 |
| JNR-014-L03 | Custom constraints | 10 |
| JNR-014-L04 | Input validation vs business rules | 7 |
| JNR-014-L05 | Sanitization and why validation is not escaping | 5 |
| JNR-014-L06 | Demo: writing a custom `@ValidSku` constraint | 10 |

**Lab** — `JNR-014-LAB1` *Validated product creation:* `POST /products` with constraints and a custom `@ValidSku`. Acceptance: invalid requests never reach the service.

**Common mistakes:** validating only in the frontend; business rules as annotations.

**Assessment:** 4 exercises.

**Career relevance:** input-related vulnerabilities (JNR-041).

---

### JNR-015 · Error handling
`n: 69` · **Video:** 50 min · **Practice:** 2 h

**Prerequisites:** BEG-029, JNR-013

**Learning outcomes** — the learner can:
1. Design a small exception hierarchy for an application (not found, conflict, business rule).
2. Map exceptions to HTTP responses centrally with `@RestControllerAdvice`.
3. Return consistent error bodies using RFC 9457 Problem Details (`ProblemDetail`).
4. Avoid leaking stack traces or internals to clients while logging them server-side.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-015-L01 | Errors are part of the API | 7 |
| JNR-015-L02 | Application exception hierarchy | 8 |
| JNR-015-L03 | `@RestControllerAdvice` | 10 |
| JNR-015-L04 | Problem Details | 8 |
| JNR-015-L05 | What not to tell the client | 7 |
| JNR-015-L06 | Demo: centralized Problem Details error handling | 10 |

**Lab** — `JNR-015-LAB1` *Consistent errors:* 400 (validation, with field errors), 404, 409, and 500 return Problem Details. Acceptance: every error matches one documented shape.

**Common mistakes:** try/catch in every controller; 200 with `"error": true`; exposing exception messages from the database.

**Assessment:** error-contract review.

**Career relevance:** API conventions (JNR-020) and incident diagnosis.

---

### JNR-016 · Spring testing basics
`n: 70` · **Video:** 74 min · **Practice:** 3 h

**Prerequisites:** BEG-045, JNR-013

**Learning outcomes** — the learner can:
1. Unit-test a service without Spring by passing collaborators to its constructor.
2. Test a controller with `@WebMvcTest` and MockMvc, including validation and error responses.
3. Use a basic Mockito mock for the service under a controller test.
4. Explain the cost of `@SpringBootTest` and when a slice is enough.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-016-L01 | Testing pyramid for Spring apps | 8 |
| JNR-016-L02 | Plain unit tests for services | 8 |
| JNR-016-L03 | Mockito in five minutes | 7 |
| JNR-016-L04 | `@WebMvcTest` and MockMvc | 15 |
| JNR-016-L05 | `@SpringBootTest` and context caching | 12 |
| JNR-016-L06 | Demo: test-driving a controller with `@WebMvcTest` | 12 |
| JNR-016-L07 | Demo: slice vs full-context tests, timed | 12 |

**Lab** — `JNR-016-LAB1` *Test the products feature:* service unit tests plus controller slice tests for success, validation failure, and not found. Acceptance: tests run in seconds; no full context in controller tests.

**Common mistakes:** `@SpringBootTest` for everything; asserting only the status code.

**Assessment:** write the missing tests for a provided controller.

**Career relevance:** deepened in JNR-043 to JNR-047.

> **Teaching note:** this module introduces just enough Mockito to isolate a controller. JNR-044 covers mocking properly.
