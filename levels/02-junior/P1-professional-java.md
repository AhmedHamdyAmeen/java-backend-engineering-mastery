# JNR-P1 — Professional Java Development

**Phase goal:** the learner writes modern, idiomatic Java that a team can maintain: current language features, reproducible builds, clean design, and the logging and configuration habits every backend service needs.

**Running project:** *Shop Core* — a plain-Java domain library (products, prices, carts, discounts) built here and reused as the domain layer of the Junior capstone (`JNR-CAP`).

**Phase total:** ~7.9 h video · ~21 h practice

---

### JNR-001 · Modern Java
`n: 55` · **Video:** 80 min · **Practice:** 4 h · `version:` current LTS

**Prerequisites:** BEG-012, BEG-024, BEG-026

**Learning outcomes** — the learner can:
1. Explain Java's six-month release cadence, what LTS means, and how to choose a version for production.
2. Replace boilerplate data classes with records, including compact constructors that validate.
3. Model closed hierarchies with sealed interfaces and handle them exhaustively with pattern-matching `switch`.
4. Use text blocks, `instanceof` patterns, and record patterns where they improve readability.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-001-L01 | Java's release model and LTS versions | 8 |
| JNR-001-L02 | Records | 12 |
| JNR-001-L03 | Sealed classes and interfaces | 10 |
| JNR-001-L04 | Switch expressions and pattern matching | 15 |
| JNR-001-L05 | Record patterns | 10 |
| JNR-001-L06 | Text blocks and other small wins | 7 |
| JNR-001-L07 | What changed since the last LTS (updated per release) | 8 |
| JNR-001-L08 | Demo: modernizing a legacy Java class step by step | 10 |

**Lab** — `JNR-001-LAB1` *Shop Core v1:* model `Product`, `Money`, and `CartLine` as records with validation; model `Discount` as a sealed hierarchy (percentage, fixed amount, buy-X-get-Y) priced by an exhaustive `switch`. Acceptance: no setters; adding a new discount type causes a compile error until handled.

**Common mistakes:** records with mutable components (lists not copied); `default` branches that defeat exhaustiveness; using preview features in production code.

**Assessment:** refactor a legacy POJO-heavy module to modern Java and justify each change.

**Career relevance:** modern codebases and interviews expect these features; sealed types reappear in event modeling (SRB-002).

---

### JNR-002 · Maven in depth
`n: 56` · **Video:** 70 min · **Practice:** 3 h

**Prerequisites:** BEG-054

**Learning outcomes** — the learner can:
1. Choose the correct dependency scope (`compile`, `provided`, `runtime`, `test`) for a dependency.
2. Inspect the dependency tree, explain transitive dependencies, and resolve a version conflict.
3. Import a BOM to align versions and explain why Spring Boot uses one.
4. Configure common plugins (compiler, surefire, failsafe) and split a project into a multi-module build.
5. Explain what makes a build reproducible and use the Maven Wrapper.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-002-L01 | Dependency scopes | 8 |
| JNR-002-L02 | Transitive dependencies and `dependency:tree` | 10 |
| JNR-002-L03 | Version conflicts and dependency management | 10 |
| JNR-002-L04 | BOMs | 7 |
| JNR-002-L05 | Plugins and the build lifecycle revisited | 10 |
| JNR-002-L06 | Multi-module projects | 10 |
| JNR-002-L07 | Reproducible builds and the Maven Wrapper | 5 |
| JNR-002-L08 | Demo: untangling a dependency conflict with `dependency:tree` | 10 |

**Lab** — `JNR-002-LAB1` *Shop multi-module:* split into `shop-core` and `shop-cli` modules with a parent POM, dependency management, and the wrapper; diagnose a planted version conflict. Acceptance: `./mvnw verify` passes on a clean clone.

**Common mistakes:** hard-coded versions in every module; `compile` scope for test libraries; ignoring dependency convergence.

**Assessment:** fix a broken multi-module build and explain the cause.

**Career relevance:** every Spring Boot project; dependency security (MID-053).

---

### JNR-003 · Code quality
`n: 57` · **Video:** 65 min · **Practice:** 3 h

**Prerequisites:** BEG-028

**Learning outcomes** — the learner can:
1. Rename variables, methods, and classes so code reads as intent.
2. Assess cohesion and coupling in a class and reduce coupling between classes.
3. Apply DRY, KISS, and YAGNI and recognize when they conflict.
4. Identify common code smells (long method, large class, feature envy, primitive obsession, duplicated logic) and apply the matching refactoring safely with IDE support.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-003-L01 | Code is read more than written | 6 |
| JNR-003-L02 | Naming | 10 |
| JNR-003-L03 | Cohesion and coupling | 10 |
| JNR-003-L04 | DRY, KISS, YAGNI — and their limits | 9 |
| JNR-003-L05 | A catalog of code smells | 12 |
| JNR-003-L06 | Safe refactoring with the IDE | 8 |
| JNR-003-L07 | Demo: refactoring a long method under green tests | 10 |

**Lab** — `JNR-003-LAB1` *Clean the checkout:* refactor a provided 300-line `CheckoutService` with tests in place. Acceptance: tests stay green throughout; each commit is one named refactoring.

**Common mistakes:** refactoring without tests; abstracting after one occurrence; cosmetic-only changes.

**Assessment:** smell-spotting review of an unseen class, with proposed refactorings.

**Career relevance:** code reviews (JNR-053) and technical debt (SRC-017).

---

### JNR-004 · SOLID principles
`n: 58` · **Video:** 70 min · **Practice:** 3 h

**Prerequisites:** BEG-024, JNR-003

**Learning outcomes** — the learner can:
1. State each SOLID principle and identify a violation in Java code.
2. Refactor a violation using composition, interfaces, or class extraction.
3. Explain how dependency inversion enables testing and is the foundation of Spring's DI.
4. Recognize when applying a principle would add needless complexity.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-004-L01 | Single Responsibility | 12 |
| JNR-004-L02 | Open/Closed | 10 |
| JNR-004-L03 | Liskov Substitution | 10 |
| JNR-004-L04 | Interface Segregation | 8 |
| JNR-004-L05 | Dependency Inversion | 12 |
| JNR-004-L06 | SOLID with judgment | 8 |
| JNR-004-L07 | Demo: dependency inversion for a payment provider | 10 |

**Lab** — `JNR-004-LAB1` *Pluggable pricing:* refactor Shop Core so tax rules and payment providers are injected through interfaces; add a new tax rule without modifying existing classes. Acceptance: core has no dependency on concrete providers.

**Common mistakes:** an interface for every class; "SRP" meaning one method per class; LSP violations via throwing `UnsupportedOperationException`.

**Assessment:** design quiz with code snippets plus the lab.

**Career relevance:** design discussions at every level; architecture styles (MID-059).

---

### JNR-005 · Design patterns introduction
`n: 59` · **Video:** 85 min · **Practice:** 4 h

**Prerequisites:** JNR-004

**Learning outcomes** — the learner can:
1. Implement Factory, Builder, Strategy, Adapter, Decorator, Observer, and Repository in Java.
2. Describe the problem each pattern solves and choose one for a given scenario.
3. Recognize these patterns in the JDK and Spring.
4. Avoid applying a pattern where a simple function or class suffices.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-005-L01 | What patterns are (and are not) | 6 |
| JNR-005-L02 | Factory | 9 |
| JNR-005-L03 | Builder | 9 |
| JNR-005-L04 | Strategy | 10 |
| JNR-005-L05 | Adapter | 9 |
| JNR-005-L06 | Decorator | 10 |
| JNR-005-L07 | Observer | 10 |
| JNR-005-L08 | Repository | 7 |
| JNR-005-L09 | Spotting patterns in Spring | 5 |
| JNR-005-L10 | Demo: replacing a type switch with Strategy | 10 |

**Lab** — `JNR-005-LAB1` *Patterns in Shop Core:* Strategy for shipping, Adapter for a third-party currency API, Decorator for logging/caching a price lookup, Observer for "order placed" notifications. Acceptance: each pattern justified in the README.

**Common mistakes:** pattern-driven design; Builder for two-field objects; Observer with hidden ordering assumptions.

**Assessment:** scenario quiz (which pattern, and why) plus the lab.

**Career relevance:** shared vocabulary for design reviews; Observer grows into event-driven design (MID-026).

---

### JNR-006 · Logging
`n: 60` · **Video:** 55 min · **Practice:** 2 h

**Prerequisites:** BEG-029, JNR-002

**Learning outcomes** — the learner can:
1. Log through SLF4J with parameterized messages and choose the correct level.
2. Configure Logback appenders, patterns, and per-package levels.
3. Log exceptions with their stack traces exactly once.
4. Identify and remove sensitive data (passwords, tokens, personal data) from logs.
5. Explain structured (JSON) logging and why machines read logs too.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-006-L01 | Why `System.out` is not logging | 6 |
| JNR-006-L02 | SLF4J and Logback | 10 |
| JNR-006-L03 | Choosing log levels | 8 |
| JNR-006-L04 | Logging exceptions well | 7 |
| JNR-006-L05 | Sensitive data in logs | 7 |
| JNR-006-L06 | Structured logging | 7 |
| JNR-006-L07 | Demo: from `println` to structured JSON logs | 10 |

**Lab** — `JNR-006-LAB1` *Observable Shop:* add logging to Shop Core and CLI; switch to JSON output by configuration; demonstrate a masked card number. Acceptance: no secrets in logs; no duplicate stack traces.

**Common mistakes:** string concatenation in log calls; log-and-rethrow; `ERROR` for expected situations.

**Assessment:** review a log file and a logging config for problems.

**Career relevance:** troubleshooting (JNR-054) and observability (MID-047).

---

### JNR-007 · Configuration
`n: 61` · **Video:** 50 min · **Practice:** 2 h

**Prerequisites:** BEG-006, BEG-034

**Learning outcomes** — the learner can:
1. Externalize configuration with properties files, YAML, and environment variables.
2. Apply the twelve-factor principle of separating config from code.
3. Explain configuration precedence and per-environment profiles.
4. Keep secrets out of source control.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-007-L01 | Why externalize configuration | 7 |
| JNR-007-L02 | Properties and YAML | 10 |
| JNR-007-L03 | Environment variables and system properties | 8 |
| JNR-007-L04 | Profiles and precedence | 8 |
| JNR-007-L05 | Secrets do not belong in Git | 7 |
| JNR-007-L06 | Demo: one JAR, three environments | 10 |

**Lab** — `JNR-007-LAB1` *Configurable CLI:* currency, tax rate, and API key read from a file, overridable by environment variable; a `.env.example` committed instead of real values. Acceptance: same JAR behaves differently per environment.

**Common mistakes:** committing `.env`; environment-specific `if` statements in code.

**Assessment:** quiz on precedence plus lab check.

**Career relevance:** Spring configuration (JNR-012) and secure configuration (JNR-042).
