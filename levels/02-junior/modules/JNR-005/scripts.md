# JNR-005 · Design patterns introduction — Lecture scripts

**Video:** 85 min · **Analogy used throughout:** recipes in a cookbook: named, proven ways to solve a common kitchen problem, which you adapt and do not follow blindly.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## JNR-005-L01 · What patterns are (and are not) (6 min)
**Goal:** understand what a design pattern is.

**Key points**
- A pattern is a named, reusable solution to a common design problem.
- It gives the team a shared vocabulary: "use a Strategy here".
- It is a recipe, not code to copy; you adapt it.
- Patterns are not goals. Do not use one when a simple function or class is enough.
- Many patterns are already in the JDK and Spring.

**Show:** a list of the seven patterns in this module with one problem line each.

**Check:** Is a pattern a library you add? *(No, it is an idea for structuring code.)*

---

## JNR-005-L02 · Factory (9 min)
**Goal:** hide how objects are created.

**Key points**
- Problem: callers should not know which class to create.
- A factory method returns the right object.
- Use it when creation has rules or choices.
- Return an interface or sealed type, not the concrete class.
- JDK examples: `List.of`, `Optional.of`, `Calendar.getInstance`.

**Show**
```java
static Discount discountFor(String code) {
    return switch (code) {
        case "SUMMER10" -> new Percentage(10);
        case "WELCOME5" -> new FixedAmount(Money.eur(500));
        default -> throw new IllegalArgumentException(code);
    };
}
```

**Check:** What does a factory hide? *(Which concrete class is created and how.)*

---

## JNR-005-L03 · Builder (9 min)
**Goal:** build objects with many optional parts clearly.

**Key points**
- Problem: a constructor with many parameters is hard to read.
- A builder sets parts by name, then calls `build()`.
- `build()` validates and returns an immutable object.
- Do not use a builder for an object with two fields; a constructor is enough.
- JDK example: `StringBuilder`, `HttpRequest.newBuilder()`.

**Show**
```java
Order order = Order.builder()
    .customer(customerId)
    .line(sku, 2)
    .coupon("SUMMER10")
    .build();
```

**Check:** When is a builder too much? *(For small objects with two or three fields.)*

---

## JNR-005-L04 · Strategy (10 min)
**Goal:** swap an algorithm without changing the caller.

**Key points**
- Problem: many `if/else` branches choose between ways of doing one thing.
- Define an interface; each way is a class (or a lambda).
- The caller holds the interface and does not care which one.
- Example: shipping cost: standard, express, pickup.
- JDK example: `Comparator` passed to `sort`.

**Show**
```java
interface ShippingStrategy { Money cost(Order o); }
class Express implements ShippingStrategy { ... }
Money total = strategy.cost(order);
```

**Check:** What does Strategy replace? *(A chain of if/else or a switch choosing an algorithm.)*

---

## JNR-005-L05 · Adapter (9 min)
**Goal:** make a foreign interface fit yours.

**Key points**
- Problem: a third-party API has a different shape from what your code expects.
- Like a travel plug adapter: it changes the shape, not the power.
- Your code depends on your interface; the adapter translates the calls.
- It protects your core from outside changes.
- JDK example: `Arrays.asList`, `InputStreamReader`.

**Show**
```java
interface CurrencyRates { Money convert(Money m, String to); }
class VendorRatesAdapter implements CurrencyRates {
    private final VendorApi api;
    ...
}
```

**Check:** What does an Adapter change? *(The shape of an interface, not what it does.)*

---

## JNR-005-L06 · Decorator (10 min)
**Goal:** add behavior by wrapping an object.

**Key points**
- Problem: add logging or caching without changing the original class.
- A decorator implements the same interface and holds another one inside.
- It adds its work, then calls the inner one.
- Decorators can be stacked.
- JDK example: `BufferedReader` wrapping a `Reader`.

**Show**
```java
class CachedPriceLookup implements PriceLookup {
    private final PriceLookup inner;
    private final Map<Sku, Money> cache = new HashMap<>();
    public Money priceOf(Sku s) { return cache.computeIfAbsent(s, inner::priceOf); }
}
```

**Check:** What must a decorator share with the object it wraps? *(The same interface.)*

---

## JNR-005-L07 · Observer (10 min)
**Goal:** notify interested parts when something happens.

**Key points**
- Problem: when an order is placed, email, stock, and analytics all need to know.
- The subject keeps a list of listeners and calls each one.
- The subject does not know what listeners do.
- Do not rely on the order of listeners; that is a hidden trap.
- Grows into event-driven design later.

**Show**
```java
interface OrderListener { void onPlaced(Order o); }
listeners.forEach(l -> l.onPlaced(order));
```

**Check:** Should the subject know what listeners do? *(No; that is the point of the pattern.)*

---

## JNR-005-L08 · Repository (7 min)
**Goal:** hide storage behind a collection-like interface.

**Key points**
- Problem: domain code should not know about SQL or files.
- A repository offers `findById`, `save`, `findAll`.
- Domain code uses the interface; storage code implements it.
- In tests, use an in-memory version.
- Spring Data uses this idea.

**Show**
```java
interface ProductRepository {
    Optional<Product> findBySku(Sku sku);
    void save(Product p);
}
```

**Check:** What does a repository hide? *(How and where data is stored.)*

---

## JNR-005-L09 · Spotting patterns in Spring (5 min)
**Goal:** recognize patterns in Spring and the JDK.

**Key points**
- Spring beans are created by factories (`BeanFactory`).
- `JdbcTemplate` and `RestTemplate` accept callbacks: close to Strategy.
- Spring Data repositories follow the Repository pattern.
- Spring events work like Observer.
- Proxies (for transactions and security) wrap beans, like Decorator.

**Show:** a table: pattern / JDK example / Spring example.

**Check:** Which pattern do Spring Data repositories follow? *(Repository.)*

---

## JNR-005-L10 · Demo: replacing a type switch with Strategy (10 min)
**Goal:** turn a growing switch on shipping type into Strategy. Prepares JNR-005-LAB1.

**Steps**
1. Show a `switch (shippingType)` in `ShippingCalculator` with three cases; tests pass.
2. Extract the `ShippingStrategy` interface and one class per case.
3. Choose the strategy through a small factory.
4. **Planned mistake:** create a strategy for a case with one line of code and a new file for each trivial detail; the design is heavier than the switch. Fix: use lambdas for tiny strategies, and keep only the meaningful classes.
5. Run the tests; add a fourth shipping type with no edit to old classes.
6. Say in one line why Strategy was justified here.

**Check:** When is a lambda enough for a strategy? *(When the behavior is tiny and has no state.)*
