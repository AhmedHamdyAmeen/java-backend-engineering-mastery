# JNR-045 · Integration testing — Lecture scripts

**Video:** 74 min · **Analogy used throughout:** a test drive on a real road, after the parts were checked on the bench.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## JNR-045-L01 · What integration tests prove (8 min)
**Goal:** know what unit tests cannot show and integration tests can.

**Key points**
- Unit tests check logic in isolation; integration tests check that parts work together with real infrastructure.
- They catch wrong SQL, missing migrations, mapping errors, and wrong configuration.
- They are slower, so write fewer and aim them at boundaries: database, web layer, messaging.
- Use the same database as production; an in-memory stand-in hides differences.
- Docker must be running for the tests in this module.

**Show:** a diagram: unit test (class + fakes) versus integration test (class + Spring + real PostgreSQL).

**Check:** Name a bug a unit test with a fake repository cannot find. *(A wrong SQL query or missing column.)*

---

## JNR-045-L02 · Testcontainers (12 min)
**Goal:** start a real PostgreSQL for tests from code.

**Key points**
- Testcontainers starts Docker containers from JUnit tests and removes them afterwards.
- `@Testcontainers` with `@Container` manages the lifecycle.
- Spring Boot's `@ServiceConnection` (Boot 3.1 or later; verify version before recording) configures the datasource from the container, with no URL copying.
- Older style: `@DynamicPropertySource` sets properties from the container.
- Make the container `static` so one container serves all tests in the class.
- Share one container across classes (singleton or reuse) to save startup time.

**Show**
```java
@Testcontainers
@SpringBootTest
class OrderIT {
    @Container @ServiceConnection
    static PostgreSQLContainer<?> db = new PostgreSQLContainer<>("postgres:16");
}
```

**Check:** What does `@ServiceConnection` replace? *(Manually copying the container URL and credentials into properties.)*

---

## JNR-045-L03 · Repository tests with `@DataJpaTest` (10 min)
**Goal:** test custom queries against a real database quickly.

**Key points**
- `@DataJpaTest` loads only JPA parts (entities, repositories), not the whole app.
- By default it replaces the datasource with an embedded database; add `@AutoConfigureTestDatabase(replace = NONE)` to keep your Testcontainers database.
- Each test runs in a transaction that rolls back at the end.
- Test every custom query: derived queries with tricky conditions, `@Query`, paging.
- Flush and clear the persistence context if you want to see what the database really returns.

**Show**
```java
@DataJpaTest
@AutoConfigureTestDatabase(replace = AutoConfigureTestDatabase.Replace.NONE)
@Testcontainers
class ProductRepositoryTest {
    @Container @ServiceConnection static PostgreSQLContainer<?> db = new PostgreSQLContainer<>("postgres:16");
    @Autowired ProductRepository repo;
}
```

**Check:** Why add `replace = NONE`? *(To stop Spring swapping in an embedded database.)*

---

## JNR-045-L04 · Full-application tests (10 min)
**Goal:** run the whole application and test it end to end.

**Key points**
- `@SpringBootTest` starts the full context; with `webEnvironment = RANDOM_PORT` it also starts the web server.
- Flyway or Liquibase migrations run on the container database, so you test the real schema.
- Use `TestRestTemplate` or `WebTestClient`; the next module adds REST Assured.
- Keep the number of these tests small; each costs startup time.
- Cache the Spring context by keeping test configurations identical.

**Show:** a test that posts an order, then reads it back through the repository, with Flyway having created the tables.

**Check:** What does `RANDOM_PORT` avoid? *(Port clashes when tests run in parallel or on a busy machine.)*

---

## JNR-045-L05 · Test data isolation (10 min)
**Goal:** keep tests independent of each other.

**Key points**
- Shared mutable data makes tests pass or fail depending on order.
- Options: roll back each test's transaction (`@Transactional`), clean tables in `@BeforeEach`, or use unique data per test.
- `@Transactional` on tests does not roll back when the code runs in another thread or via real HTTP.
- Prefer unique values (random email) so tests cannot collide.
- Never rely on rows left behind by other tests.

**Show:** a `@BeforeEach` that truncates tables, and a helper `uniqueEmail()` returning `user-<uuid>@test.com`.

**Check:** Does `@Transactional` rollback work for a test using real HTTP calls? *(No; the server runs in another thread and commits separately.)*

---

## JNR-045-L06 · Demo: Testcontainers integration tests for Shop (12 min)
**Goal:** add real-database tests for Shop. Prepares `JNR-045-LAB1`.

**Steps**
1. Add Testcontainers and the PostgreSQL module dependencies (verify versions).
2. Create a shared base configuration with a `static` container and `@ServiceConnection`.
3. Write a `@DataJpaTest` for a custom product search query.
4. Write a `@SpringBootTest` that creates an order and reads it back with migrations applied.
5. **Planned mistake:** an H2 test passes but the same query fails on PostgreSQL because of a function difference; move it to the Testcontainers test.
6. Run the suite with Docker only, on a clean checkout.

---

## JNR-045-L07 · Demo: fixing leaking test data (12 min)
**Goal:** find and fix tests that depend on each other. Prepares `JNR-045-LAB1`.

**Steps**
1. Show two tests that pass alone but one fails when run together.
2. Find the cause: both insert the same email, or one counts all rows.
3. Run in random order (JUnit method order setting) to reproduce.
4. Fix with unique data per test and a cleanup in `@BeforeEach`.
5. **Planned mistake:** adding `@Transactional` to a test that uses real HTTP and seeing the leak remain; explain why and use cleanup instead.
6. Run the suite ten times to confirm.
