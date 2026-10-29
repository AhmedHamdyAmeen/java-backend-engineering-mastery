# MID-060 · DDD introduction — Lecture scripts

**Video:** 70 min · **Analogy used throughout:** a shared dictionary and a set of sealed packages: the dictionary fixes the words, each package keeps its contents consistent.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-060-L01 · Why domain-driven design (8 min)
**Goal:** say when DDD pays off and what it is.

**Key points**
- DDD models the business domain in code, with developers and domain experts working together.
- Strategic DDD: language, bounded contexts, context maps. Tactical DDD: entities, value objects, aggregates, repositories, events.
- It pays off where rules are complex and change often; it is overkill for plain CRUD.
- Symptom it fixes: an anemic model, where entities are data bags and services hold all the rules.
- Shop's `Order` has rules (status flow, cancellation) but only getters and setters.

**Show:** `order.setStatus("SHIPPED")` in a service versus `order.ship()` in the model.

**Check:** When is DDD overkill? *(For simple CRUD with few business rules.)*

---

## MID-060-L02 · Ubiquitous language (8 min)
**Goal:** use one shared vocabulary in talk and code.

**Key points**
- The ubiquitous language is the vocabulary agreed with domain experts, used in meetings, docs, and class names.
- If the expert says "place an order" and the code says `createRecord`, translation errors follow.
- Build it with glossary sessions and by asking "what do you call this?".
- The same word can mean different things in different contexts (see MID-025).
- When the language changes, refactor the code names.

**Show:** a glossary table: `Order`, `Place`, `Cancel`, `Reserve stock`, with a column for the class or method name.

**Check:** What do you do when the business renames a concept? *(Rename it in the code too.)*

---

## MID-060-L03 · Entities and value objects (10 min)
**Goal:** model identity versus value in Java.

**Key points**
- An entity has an identity that persists as its attributes change: `Order` with `OrderId`.
- A value object has no identity; equal values are interchangeable: `Money`, `Address`. It is immutable.
- Java records fit value objects well and validate in the compact constructor.
- Entity equality is by ID; value equality is by all fields.
- Prefer value objects over primitives (`Money` instead of `BigDecimal` plus a currency string).

**Show**
```java
public record Money(BigDecimal amount, Currency currency) {
    public Money {
        if (amount.signum() < 0) throw new IllegalArgumentException("negative");
    }
    public Money plus(Money o) { /* same currency check */ return new Money(amount.add(o.amount), currency); }
}
```

**Check:** Which one is `Money`, entity or value object? *(Value object.)*

---

## MID-060-L04 · Aggregates and invariants (14 min)
**Goal:** design aggregates around the rules they protect.

**Key points**
- An invariant is a rule that must always hold, such as "order total equals the sum of its lines".
- An aggregate is a cluster of objects changed as one unit, with a root (`Order`) as the only entry point.
- Keep aggregates small; one transaction changes one aggregate.
- Reference other aggregates by ID, not by object reference (`CustomerId`, not `Customer`).
- Design around invariants, not around tables. Rules across aggregates are eventually consistent (MID-030).

**Show**
```java
public class Order {            // aggregate root
    private final OrderId id;
    private final CustomerId customerId;   // by ID
    private final List<OrderLine> lines = new ArrayList<>();
    private Status status = Status.NEW;

    public void addLine(ProductId p, int qty, Money price) {
        if (status != Status.NEW) throw new IllegalStateException("order not editable");
        lines.add(new OrderLine(p, qty, price));
    }
}
```

**Check:** How should `Order` refer to its customer? *(By `CustomerId`.)*

---

## MID-060-L05 · Repositories and domain services (8 min)
**Goal:** place persistence and cross-aggregate logic correctly.

**Key points**
- One repository per aggregate root, with collection-like methods: `findById`, `save`.
- The repository interface lives in the domain; JPA implements it (MID-059).
- A domain service holds domain logic that fits no single aggregate, such as pricing across order and discount rules.
- Do not confuse it with an application service, which orchestrates use cases and transactions.
- No repository for inner objects like `OrderLine`.

**Show:** `interface OrderRepository { Optional<Order> findById(OrderId id); void save(Order o); }`

**Check:** Is there a repository for `OrderLine`? *(No, only for the aggregate root.)*

---

## MID-060-L06 · Domain events (8 min)
**Goal:** record that something happened in the domain.

**Key points**
- A domain event is a fact in the past tense: `OrderPlaced`, `OrderCancelled`.
- The aggregate raises events as part of a state change; other code reacts.
- Events are immutable and carry the aggregate ID and time.
- Within a service they decouple side effects; to leave the service they become integration events (MID-026, MID-029).
- Do not publish before the state change is saved.

**Show:** `Order.place()` adds `new OrderPlaced(id, Instant.now())` to an internal list that the application service publishes after saving.

**Check:** Why past tense? *(An event states a fact that already happened.)*

---

## MID-060-L07 · Demo: redesigning the Order aggregate (14 min)
**Goal:** refactor an anemic `Order` into an aggregate. Prepares `MID-060-LAB1`.

**Steps**
1. Start from the setter-based `Order` and a service with `if (status == ...)` checks.
2. Introduce `OrderId`, `Money`, and `OrderLine` value types; remove setters.
3. Move rules into methods: `addLine`, `place`, `cancel`, with status transitions.
4. Raise `OrderPlaced` and `OrderCancelled` events and publish them from the application service after `save`.
5. **Planned mistake:** hold a full `Customer` object inside `Order`. Replace it with `CustomerId` and explain why loading and locking grew.
6. Write one unit test per invariant, with no Spring context.

---
