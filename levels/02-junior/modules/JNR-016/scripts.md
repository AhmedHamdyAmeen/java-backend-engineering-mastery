# JNR-016 · Spring testing basics — Lecture scripts

**Video:** 74 min · **Analogy used throughout:** checking a car: test one part on the bench, the steering with a small rig, and only sometimes the whole car on the road.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## JNR-016-L01 · Testing pyramid for Spring apps (8 min)
**Goal:** know which kind of test to write.

**Key points**
- Many fast unit tests, fewer slice tests, few full-context tests.
- Unit: a class with plain Java, no Spring.
- Slice: part of the app (web layer) with Spring's help.
- Full: the whole app in a test; slowest.
- Fast tests are run often; slow ones get skipped.

**Show:** a pyramid with three levels and a rough cost label (milliseconds, a second or two, several seconds).

**Check:** Which level should have the most tests? *(Unit tests.)*

---

## JNR-016-L02 · Plain unit tests for services (8 min)
**Goal:** test a service without Spring.

**Key points**
- Constructor injection means you can call `new` with fakes.
- No annotations, no context: runs in milliseconds.
- Test one rule per test; name it by behavior.
- Use JUnit 5 and AssertJ assertions.

**Show**
```java
@Test
void unknownProductThrowsNotFound() {
    var service = new ProductService(new InMemoryProductRepository());
    assertThatThrownBy(() -> service.get(999)).isInstanceOf(NotFoundException.class);
}
```

**Check:** Why does a test need no Spring here? *(The class takes dependencies via its constructor.)*

---

## JNR-016-L03 · Mockito in five minutes (7 min)
**Goal:** use a mock to isolate a class.

**Key points**
- A mock is a fake object you program: "when asked X, answer Y".
- `when(mock.method()).thenReturn(value)` sets the answer; `verify(mock).method()` checks it was called.
- Mock the collaborators, never the class under test.
- This is only the basics; JNR-044 covers mocking properly.

**Show**
```java
var repo = mock(ProductRepository.class);
when(repo.findById(1L)).thenReturn(Optional.of(new Product(1L, "Pen")));
```

**Check:** What does `thenReturn` do? *(Defines what the mock answers.)*

---

## JNR-016-L04 · `@WebMvcTest` and MockMvc (15 min)
**Goal:** test a controller through HTTP without starting a server.

**Key points**
- `@WebMvcTest(ProductController.class)` loads only the web layer (controller, advice, JSON), not services or repositories.
- Provide the service as a mock bean (`@MockitoBean` in recent Spring, `@MockBean` in older; verify version before recording).
- `MockMvc` sends fake requests and checks status, JSON, and headers.
- Test success, validation failure (400), and not found (404), and check the body, not only the status.

**Show**
```java
@WebMvcTest(ProductController.class)
class ProductControllerTest {
    @Autowired MockMvc mvc;
    @MockitoBean ProductService service;

    @Test void notFound() throws Exception {
        when(service.get(9)).thenThrow(new NotFoundException("Product", 9));
        mvc.perform(get("/products/9"))
           .andExpect(status().isNotFound())
           .andExpect(jsonPath("$.detail").value("Product 9 not found"));
    }
}
```

**Check:** What does `@WebMvcTest` not load? *(Services, repositories, and the rest of the app.)*

---

## JNR-016-L05 · `@SpringBootTest` and context caching (12 min)
**Goal:** explain the cost of full-context tests.

**Key points**
- `@SpringBootTest` starts the entire application context.
- Spring caches contexts between tests with the same configuration; different configs mean a new context.
- Mock beans and different properties create new contexts, so use them sparingly.
- Use it for a few end-to-end checks; use slices for most.

**Show:** a timeline: first test starts the context (seconds); next tests with the same configuration reuse it; a test with a new mock bean starts another.

**Check:** Why can adding a `@MockitoBean` slow the suite? *(It changes the configuration, so Spring builds another context.)*

---

## JNR-016-L06 · Demo: test-driving a controller with `@WebMvcTest` (12 min)
**Goal:** write tests first for `GET /products/{id}`; prepares JNR-016-LAB1.

**Steps**
1. Write a failing test for the success case; mock the service; assert status and JSON fields.
2. Make it pass (the controller from JNR-013).
3. Add a validation test: `POST /products` with a blank name returns 400 and a field error.
4. **Planned mistake:** assert only `status().isOk()`, and a bug in the JSON passes. Fix: add `jsonPath` assertions.
5. Add the not-found test and check the Problem Details body.

---

## JNR-016-L07 · Demo: slice vs full-context tests, timed (12 min)
**Goal:** measure the difference; prepares JNR-016-LAB1.

**Steps**
1. Run the controller slice tests and note the time.
2. Write the same check as a `@SpringBootTest` with `@AutoConfigureMockMvc`; run and note the time.
3. Run both classes together; show the cached context being reused.
4. **Planned mistake:** convert every controller test to `@SpringBootTest` "to be safe"; the suite becomes several times slower. Fix: keep slices; keep one full-context smoke test.
5. Summarize the rule: slice for one layer, full context for wiring and end-to-end.
