# JNR-047 · Testing practices — Lecture scripts

**Video:** 50 min · **Analogy used throughout:** a well-run kitchen: clear recipes, prepared ingredients, and a clean station.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## JNR-047-L01 · Arrange-Act-Assert and naming (8 min)
**Goal:** structure each test so it reads in seconds.

**Key points**
- Arrange: set up data and collaborators. Act: call the thing under test once. Assert: check the outcome.
- Separate the three parts with blank lines or comments.
- Name tests by behavior: `rejectsOrderWhenStockIsZero`, not `test1` or `placeOrderTest`.
- One reason to fail per test; a name with "and" often means two tests.
- Assert on outcomes, not on how the code got there.

**Show**
```java
@Test
void rejectsOrderWhenStockIsZero() {
    var product = aProduct().withStock(0).build();       // arrange
    var result = service.place(orderOf(product));         // act
    assertThat(result.status()).isEqualTo(REJECTED);      // assert
}
```

**Check:** What does the "Act" step do? *(Calls the code under test, once.)*

---

## JNR-047-L02 · Test data builders (10 min)
**Goal:** create test objects without copy-paste.

**Key points**
- Long constructors repeated in every test hide what matters.
- A builder has sensible defaults; the test overrides only the relevant fields: `aProduct().withStock(0).build()`.
- An object mother is a class of named factories: `Products.outOfStock()`.
- Defaults must be valid so tests start from a good state.
- Keep builders in test code, not production.

**Show**
```java
class ProductBuilder {
    private String name = "Pen"; private int stock = 10; private BigDecimal price = new BigDecimal("2.50");
    static ProductBuilder aProduct() { return new ProductBuilder(); }
    ProductBuilder withStock(int s) { this.stock = s; return this; }
    Product build() { return new Product(name, price, stock); }
}
```

**Check:** What should a builder's defaults be? *(Valid, so tests set only what they care about.)*

---

## JNR-047-L03 · Flaky and brittle tests (12 min)
**Goal:** spot and fix tests that fail without a real bug.

**Key points**
- A flaky test passes and fails on the same code. Causes: time, test order, randomness, shared data, real network, async timing.
- Control time with an injected `Clock` instead of `LocalDate.now()`.
- Avoid `Thread.sleep`; wait for a condition (Awaitility) or make the code synchronous in tests.
- Seed or fix randomness.
- A brittle test breaks when you refactor without changing behavior: usually over-specified (too many verifies, exact strings).

**Show**
```java
Clock fixed = Clock.fixed(Instant.parse("2025-01-15T10:00:00Z"), ZoneOffset.UTC);
var service = new CouponService(fixed);
```

**Check:** Why is `Thread.sleep(2000)` a bad wait? *(Too slow when fast, too short when the machine is busy; it is a guess.)*

---

## JNR-047-L04 · Shaping a healthy suite (10 min)
**Goal:** balance fast tests and confidence.

**Key points**
- Many unit tests (fast), a moderate number of slice tests, few full integration tests.
- Fast feedback matters: unit tests in seconds, the whole suite in minutes.
- Do not test the same thing at every level.
- Track runtime and flaky tests; fix or delete tests nobody trusts.
- A failing test should point to the cause quickly.

**Show:** a pyramid with counts and times, for example unit 300 (10 s), slice 60 (40 s), integration 20 (3 min).

**Check:** Which level should have the most tests? *(Unit tests.)*

---

## JNR-047-L05 · Demo: hunting a flaky test (10 min)
**Goal:** find the cause of a flaky test and fix it. Prepares `JNR-047-LAB1`.

**Steps**
1. Run the suite ten times and note which test fails sometimes.
2. Run that test alone, then in random order, to see whether it depends on order.
3. Spot the cause: it uses `LocalDate.now()` near midnight, or leftover data.
4. Inject a fixed `Clock` and use unique data.
5. **Planned mistake:** add `Thread.sleep` and see it still flake; replace with a deterministic clock.
6. Run ten times again and record the runtime.
