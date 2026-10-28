# JNR-P6 — Testing and Delivery

**Phase goal:** the learner proves their code works with a balanced automated test suite, packages it in containers, delivers it through a CI pipeline to a running environment, and works the way professional teams do — including diagnosing problems once it runs.

**Running project:** *Shop API* reaches capstone shape: full test suite, Docker Compose, CI pipeline, and a deployed instance.

**Phase total:** ~12.1 h video · ~32 h practice

> **Ordering change (v1.1):** Linux, Docker, and Docker Compose (JNR-048 to JNR-050) are taught before integration testing (JNR-045), because Testcontainers requires a working Docker environment. IDs are unchanged; see the catalog for teaching order.

---

### JNR-043 · Unit testing
`n: 97` · **Video:** 60 min · **Practice:** 3 h · `version:` current JUnit Jupiter

**Prerequisites:** BEG-045

**Learning outcomes** — the learner can:
1. Use the JUnit Jupiter lifecycle (`@BeforeEach`, `@AfterEach`, `@Nested`, `@DisplayName`).
2. Write parameterized tests with value, CSV, and method sources.
3. Write expressive assertions with AssertJ, including collections and exceptions.
4. Measure coverage and explain why coverage is not quality.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-043-L01 | What a unit is | 7 |
| JNR-043-L02 | Lifecycle and structure | 10 |
| JNR-043-L03 | Parameterized tests | 12 |
| JNR-043-L04 | AssertJ | 12 |
| JNR-043-L05 | Coverage and its limits | 9 |
| JNR-043-L06 | Demo: turning copy-pasted tests into a parameterized table | 10 |

**Lab** — `JNR-043-LAB1` *Pricing rules suite:* parameterized tests for every discount and tax combination in Shop Core. Acceptance: one table-driven test replaces ≥ 10 copy-pasted ones; a planted bug is caught.

**Common mistakes:** one test asserting ten things; testing private methods.

**Assessment:** write tests for an unseen class; graded by mutation survivors.

**Career relevance:** daily practice.

---

### JNR-044 · Mocking
`n: 98` · **Video:** 55 min · **Practice:** 2.5 h

**Prerequisites:** JNR-009, JNR-043

**Learning outcomes** — the learner can:
1. Distinguish stubs, mocks, spies, and fakes, and pick one.
2. Stub return values and exceptions, and verify interactions with Mockito.
3. Capture arguments and assert on them.
4. Recognize over-mocking and prefer fakes or real objects where cheap.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-044-L01 | Test doubles taxonomy | 8 |
| JNR-044-L02 | Stubbing with Mockito | 10 |
| JNR-044-L03 | Verifying interactions | 8 |
| JNR-044-L04 | Argument captors | 7 |
| JNR-044-L05 | When not to mock | 12 |
| JNR-044-L06 | Demo: mocking the payment gateway's three outcomes | 10 |

**Lab** — `JNR-044-LAB1` *Order service tests:* test `OrderService` with a mocked payment gateway (success, decline, timeout) and an in-memory fake repository. Acceptance: tests survive an internal refactor of the service.

**Common mistakes:** mocking types you do not own; verifying every call; mocks returning mocks.

**Assessment:** refactor an over-mocked test suite.

**Career relevance:** contract testing (MID-045).

---

### JNR-048 · Linux basics
`n: 102` · **Video:** 65 min · **Practice:** 3 h

**Prerequisites:** BEG-006

**Learning outcomes** — the learner can:
1. Inspect processes, memory, and disk (`ps`, `top`, `free`, `df`), and stop a process.
2. Read and change file permissions and ownership.
3. Connect to a server over SSH with key-based authentication.
4. Find which process listens on a port (`ss`, `lsof`).
5. Read service logs with `journalctl` and `tail -f`, and manage a service with `systemctl`.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-048-L01 | Linux for backend engineers | 7 |
| JNR-048-L02 | Processes and resources | 10 |
| JNR-048-L03 | Users, permissions, ownership | 10 |
| JNR-048-L04 | SSH and keys | 10 |
| JNR-048-L05 | Ports and networking tools | 8 |
| JNR-048-L06 | Logs and services | 10 |
| JNR-048-L07 | Demo: running Shop as a systemd service | 10 |

**Lab** — `JNR-048-LAB1` *Run Shop on Linux:* on a Linux VM or WSL, run the Shop JAR as a `systemd` service, read its logs, and find its port. Acceptance: service restarts automatically after a kill.

**Common mistakes:** `chmod 777`; running services as root; password SSH logins.

**Assessment:** timed troubleshooting tasks on a Linux box.

**Career relevance:** containers and production servers are Linux.

---

### JNR-049 · Docker fundamentals
`n: 103` · **Video:** 84 min · **Practice:** 3 h

**Prerequisites:** JNR-011, JNR-048

**Learning outcomes** — the learner can:
1. Explain images, containers, layers, and registries, and how containers differ from VMs.
2. Write a multi-stage Dockerfile for a Spring Boot app that runs as a non-root user.
3. Use volumes for persistent data and port mapping for access.
4. Connect containers on a user-defined network.
5. Inspect running containers (`logs`, `exec`, `inspect`).

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-049-L01 | Why containers | 8 |
| JNR-049-L02 | Images, layers, registries | 10 |
| JNR-049-L03 | Running containers | 10 |
| JNR-049-L04 | Writing a Dockerfile for Spring Boot | 14 |
| JNR-049-L05 | Volumes and networks | 10 |
| JNR-049-L06 | Debugging containers | 8 |
| JNR-049-L07 | Demo: writing a multi-stage Dockerfile for Shop | 12 |
| JNR-049-L08 | Demo: debugging a crashing container | 12 |

**Lab** — `JNR-049-LAB1` *Containerize Shop:* multi-stage image, non-root, under 300 MB; run PostgreSQL in a container with a volume. Acceptance: data survives container removal.

**Common mistakes:** building inside the final image; `latest` tags; secrets baked into images.

**Assessment:** review and improve a poor Dockerfile.

**Career relevance:** Kubernetes (MID-057).

---

### JNR-050 · Docker Compose
`n: 104` · **Video:** 45 min · **Practice:** 2 h

**Prerequisites:** BEG-051, JNR-049

**Learning outcomes** — the learner can:
1. Define a multi-service local environment (app, PostgreSQL, Keycloak) in `compose.yaml`.
2. Use health checks and dependency conditions so services start in a usable order.
3. Supply configuration through environment files without committing secrets.
4. Use Spring Boot's Docker Compose support for development.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-050-L01 | Compose files | 10 |
| JNR-050-L02 | Health checks and startup order | 8 |
| JNR-050-L03 | Environment and secrets | 7 |
| JNR-050-L04 | Spring Boot's Compose integration | 10 |
| JNR-050-L05 | Demo: one-command Shop stack | 10 |

**Lab** — `JNR-050-LAB1` *One-command Shop:* `docker compose up` starts the whole stack with seeded data. Acceptance: a new teammate runs the stack in under 10 minutes using only the README.

**Common mistakes:** `depends_on` without health checks; committed `.env` files.

**Assessment:** lab check.

**Career relevance:** the capstone's local environment requirement.

---

### JNR-045 · Integration testing
`n: 99` · **Video:** 74 min · **Practice:** 3 h

**Prerequisites:** JNR-016, JNR-029, JNR-050

**Learning outcomes** — the learner can:
1. Write `@SpringBootTest` and `@DataJpaTest` tests against a real PostgreSQL using Testcontainers.
2. Use service connections so tests configure themselves from containers.
3. Isolate test data between tests (transactions, cleanup, unique data).
4. Explain why H2 is not a substitute for the production database.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-045-L01 | What integration tests prove | 8 |
| JNR-045-L02 | Testcontainers | 12 |
| JNR-045-L03 | Repository tests with `@DataJpaTest` | 10 |
| JNR-045-L04 | Full-application tests | 10 |
| JNR-045-L05 | Test data isolation | 10 |
| JNR-045-L06 | Demo: Testcontainers integration tests for Shop | 12 |
| JNR-045-L07 | Demo: fixing leaking test data | 12 |

**Lab** — `JNR-045-LAB1` *Real-database tests:* repository tests for every custom query and an end-to-end order test with migrations applied. Acceptance: suite passes from a clean machine with only Docker installed.

**Common mistakes:** shared mutable data across tests; one container per test class without reuse.

**Assessment:** add integration tests for an untested repository.

**Career relevance:** the foundation of a trustworthy CI pipeline.

---

### JNR-046 · API testing
`n: 100` · **Video:** 50 min · **Practice:** 2.5 h

**Prerequisites:** JNR-019, JNR-045

**Learning outcomes** — the learner can:
1. Test endpoints end-to-end with REST Assured against a running application.
2. Choose between MockMvc slice tests and full HTTP tests.
3. Cover success, validation, authentication, authorization, and not-found scenarios systematically.
4. Assert on response bodies and headers, not just status codes.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-046-L01 | MockMvc vs real HTTP | 8 |
| JNR-046-L02 | REST Assured | 12 |
| JNR-046-L03 | A scenario matrix for every endpoint | 10 |
| JNR-046-L04 | Testing secured endpoints | 10 |
| JNR-046-L05 | Demo: the checkout journey with REST Assured | 10 |

**Lab** — `JNR-046-LAB1` *Checkout journey:* register → login → add to cart → checkout → view order, plus the failure scenario for each step. Acceptance: matrix documented; all scenarios automated.

**Common mistakes:** only happy paths; brittle assertions on entire JSON strings.

**Assessment:** scenario matrix for an unseen endpoint.

**Career relevance:** contract and performance testing (MID-045, MID-046).

---

### JNR-047 · Testing practices
`n: 101` · **Video:** 50 min · **Practice:** 2 h

**Prerequisites:** JNR-045

**Learning outcomes** — the learner can:
1. Structure tests with Arrange-Act-Assert and name them by behavior.
2. Build test data with builders or object mothers instead of copy-paste.
3. Identify brittle tests (time, order, randomness, over-specification) and fix them.
4. Balance the test suite across unit, slice, and integration levels for speed and confidence.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-047-L01 | Arrange-Act-Assert and naming | 8 |
| JNR-047-L02 | Test data builders | 10 |
| JNR-047-L03 | Flaky and brittle tests | 12 |
| JNR-047-L04 | Shaping a healthy suite | 10 |
| JNR-047-L05 | Demo: hunting a flaky test | 10 |

**Lab** — `JNR-047-LAB1` *Suite cleanup:* refactor the Shop test suite: builders, deterministic clocks, no order dependence; record runtime before and after. Acceptance: 10 consecutive runs green.

**Common mistakes:** `Thread.sleep` in tests; tests coupled to implementation details.

**Assessment:** test-quality review.

**Career relevance:** test strategy at Senior and Staff levels.

---

### JNR-051 · CI/CD introduction
`n: 105` · **Video:** 69 min · **Practice:** 3 h

**Prerequisites:** BEG-047, JNR-045, JNR-049

**Learning outcomes** — the learner can:
1. Explain continuous integration, delivery, and deployment.
2. Write a GitHub Actions workflow that builds, runs all tests (including Testcontainers), and caches dependencies.
3. Publish build artifacts (JAR, container image) to a registry with version tags.
4. Protect `main` with required checks.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-051-L01 | CI, CD, and CD | 8 |
| JNR-051-L02 | GitHub Actions anatomy | 12 |
| JNR-051-L03 | Build and test pipeline | 10 |
| JNR-051-L04 | Artifacts and image publishing | 10 |
| JNR-051-L05 | Branch protection | 5 |
| JNR-051-L06 | Demo: building the Shop pipeline in GitHub Actions | 12 |
| JNR-051-L07 | Demo: publishing a tagged image on merge | 12 |

**Lab** — `JNR-051-LAB1` *Shop pipeline:* every PR runs the full suite; merges to `main` publish a tagged image. Acceptance: a PR with a failing test cannot be merged.

**Common mistakes:** secrets printed in logs; pipelines that pass with zero tests run.

**Assessment:** fix a broken workflow.

**Career relevance:** CI/CD advanced (MID-055).

---

### JNR-052 · Deployment basics
`n: 106` · **Video:** 69 min · **Practice:** 3 h

**Prerequisites:** JNR-012, JNR-051

**Learning outcomes** — the learner can:
1. Deploy the containerized app and a managed PostgreSQL to a hosting platform or VM.
2. Configure the deployment entirely through environment variables.
3. Expose liveness and readiness health checks and explain the difference.
4. Perform graceful shutdown and roll back to the previous image.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-052-L01 | From artifact to running service | 8 |
| JNR-052-L02 | Deployment targets compared | 10 |
| JNR-052-L03 | Configuration in deployed environments | 8 |
| JNR-052-L04 | Health checks: liveness vs readiness | 10 |
| JNR-052-L05 | Graceful shutdown and rollback | 9 |
| JNR-052-L06 | Demo: deploying Shop and its database | 12 |
| JNR-052-L07 | Demo: rolling back a bad release | 12 |

**Lab** — `JNR-052-LAB1` *Shop goes live:* deploy from the pipeline to a public URL with a managed database; perform and document a rollback. Acceptance: deployed instance reachable; rollback under 5 minutes.

**Common mistakes:** database credentials in the image; health checks that call the database for liveness.

**Assessment:** deployment walkthrough.

**Career relevance:** Kubernetes (MID-057) and production readiness (SRC-011).

---

### JNR-053 · Team workflows
`n: 107` · **Video:** 50 min · **Practice:** 2 h

**Prerequisites:** BEG-047

**Learning outcomes** — the learner can:
1. Follow trunk-based development or a short-lived branch workflow.
2. Write PR descriptions that a reviewer can act on, and keep PRs small.
3. Give and receive code-review feedback constructively.
4. Break work into issues, estimate roughly, and participate in agile ceremonies.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-053-L01 | Branching strategies | 8 |
| JNR-053-L02 | Good pull requests | 8 |
| JNR-053-L03 | Code review as reviewer and author | 12 |
| JNR-053-L04 | Issues, boards, and agile basics | 12 |
| JNR-053-L05 | Demo: a pull request from issue to merge | 10 |

**Lab** — `JNR-053-LAB1` *Team sprint:* in groups of three, deliver two Shop features in a one-week mini-sprint with issues, PRs, and reviews. Acceptance: every change merged through a reviewed PR; retro notes written.

**Common mistakes:** 2,000-line PRs; reviews that only nitpick style.

**Assessment:** PR and review quality (COM dimension).

**Career relevance:** the graduation gate requires a reviewable PR; collaboration (MID-066).

---

### JNR-054 · Troubleshooting
`n: 108` · **Video:** 55 min · **Practice:** 3 h

**Prerequisites:** BEG-018, JNR-006, JNR-052

**Learning outcomes** — the learner can:
1. Reproduce a reported bug reliably, locally or in a test.
2. Read logs and stack traces from a deployed service to localize a failure.
3. Identify environment differences (config, data, versions) that explain "works on my machine".
4. Write a short bug report with root cause, fix, and a regression test.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-054-L01 | A troubleshooting method | 8 |
| JNR-054-L02 | Logs and stack traces in production | 12 |
| JNR-054-L03 | Environment differences | 10 |
| JNR-054-L04 | From bug to regression test | 8 |
| JNR-054-L05 | Asking for help well | 7 |
| JNR-054-L06 | Demo: diagnosing a production fault from logs | 10 |

**Lab** — `JNR-054-LAB1` *Break the Shop:* the instructor injects three faults into a deployed Shop (bad config, data-dependent bug, dependency change); diagnose each with only logs and the codebase. Acceptance: root cause, fix, and regression test for each.

**Common mistakes:** fixing without reproducing; changing several things at once.

**Assessment:** live troubleshooting session.

**Career relevance:** incident handling (MID-050) and advanced troubleshooting (SRC-015).

---

## Junior capstone — E-Commerce Backend API (`JNR-CAP`)

Full brief, acceptance criteria, and graduation gate: [`projects/ladder.md`](../../projects/ladder.md#02--e-commerce-rest-api-jnr-cap).
