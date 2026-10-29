# JNR-045 · Integration testing — Exercises and lab

## Lab
### JNR-045-LAB1 · Real-database tests
**Outcomes:** 1–4 · **Time:** ~3 h
Write repository tests for every custom query and an end-to-end order test with migrations applied, all against PostgreSQL via Testcontainers.
**Acceptance:** suite passes from a clean machine with only Docker installed.

## Exercises (assessment: add integration tests for an untested repository)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-045-EX01 | 1 | Write a `@DataJpaTest` with a Testcontainers PostgreSQL for `findByCategoryOrderByPrice`. |
| JNR-045-EX02 | 1 | Write a `@SpringBootTest` (random port) that places an order and checks it is stored. |
| JNR-045-EX03 | 2 | Replace a `@DynamicPropertySource` setup with `@ServiceConnection`. |
| JNR-045-EX04 | 3 | Two tests insert the same unique email. Fix with unique data and cleanup. |
| JNR-045-EX05 | 3 | Explain why `@Transactional` on a test does not clean up data created through real HTTP. |
| JNR-045-EX06 | 4 | List three differences between H2 and PostgreSQL that can hide bugs. |
| JNR-045-EX07 | 1 | Make one container serve all test classes and time the suite before and after. |

## Solutions
- **EX01** `@DataJpaTest @AutoConfigureTestDatabase(replace = NONE) @Testcontainers` with a `static @Container @ServiceConnection` field; save products and assert order.
- **EX02** `@SpringBootTest(webEnvironment = RANDOM_PORT)`, post through `TestRestTemplate`, then assert with the repository.
- **EX03** Remove the `@DynamicPropertySource` method and annotate the container field with `@ServiceConnection`.
- **EX04** Generate `user-<uuid>@test.com` per test; add `repo.deleteAll()` in `@BeforeEach` where needed.
- **EX05** The server handles the request on another thread with its own transaction, which commits; the test transaction does not cover it.
- **EX06** Examples: SQL dialect and functions, JSON/array/enum types, constraint and locking behavior, case sensitivity, migration scripts that only run on PostgreSQL.
- **EX07** A shared `static` container in an abstract base class or the singleton pattern; record before and after runtimes.
- Outcome 4 is also covered by quiz Q09–Q10.
