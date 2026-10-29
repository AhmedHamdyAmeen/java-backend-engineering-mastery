# MID-059 · Architectural styles — Lecture scripts

**Video:** 64 min · **Analogy used throughout:** a building's floor plan: walls and doors decide what can change without knocking down the rest.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-059-L01 · What architecture is for (8 min)
**Goal:** explain architecture as the set of decisions that are expensive to change.

**Key points**
- Architecture is structure plus the rules about who may depend on whom.
- Its job is to keep change cheap: swap a database, a payment provider, or a framework without a rewrite.
- Drivers: team size, domain complexity, change rate, and quality needs (latency, availability).
- No style is best; each protects something and costs something.
- Shop's pain today: business rules call JPA directly, so every change touches everything.

**Show:** a dependency arrow diagram of Shop: controller → service → repository → entity, with JPA annotations everywhere.

**Check:** What is architecture mostly about? *(Decisions that are costly to change, and the dependency rules that keep change cheap.)*

---

## MID-059-L02 · Layered architecture and its limits (8 min)
**Goal:** recognize what layering gives and where it breaks.

**Key points**
- Layers: web → service → persistence; each layer calls the one below.
- Strength: simple, familiar, fast to start.
- Weakness: the database sits at the bottom, so the domain ends up shaped by tables and the ORM.
- Services become "transaction scripts" over anemic entities; business rules scatter.
- Tests need a database because the logic cannot be reached without it.

**Show:** a three-box stack with the arrow pointing down to `JpaRepository`, and a note "domain depends on infrastructure".

**Check:** Which way do dependencies point in a classic layered app? *(Downward, ending at the database.)*

---

## MID-059-L03 · Hexagonal architecture (14 min)
**Goal:** place the domain at the centre and push frameworks to the edge.

**Key points**
- Ports are interfaces owned by the domain; adapters implement them for a technology.
- Driving (inbound) side: REST controller calls an inbound port (use case).
- Driven (outbound) side: the domain calls an outbound port (`PaymentGateway`); an adapter talks to the real provider.
- The dependency rule: adapters depend on the domain, never the reverse.
- Payoff: unit-test the domain without Spring, swap adapters freely.
- Do not add an interface where no boundary exists.

**Show**
```java
// domain: no Spring, no JPA imports
public interface PaymentGateway { PaymentResult charge(OrderId id, Money amount); }

// adapter (infrastructure)
@Component class StripePaymentAdapter implements PaymentGateway { ... }
```

**Check:** Who owns the `PaymentGateway` interface, the domain or the adapter? *(The domain.)*

---

## MID-059-L04 · Clean architecture (8 min)
**Goal:** compare clean architecture with hexagonal.

**Key points**
- Concentric rings: entities → use cases → interface adapters → frameworks and drivers.
- Same dependency rule as hexagonal: source code points inward only.
- Adds an explicit use-case ring and the idea of boundary data structures (DTOs crossing rings).
- Onion architecture is a close cousin. In practice the three share one idea: protect the domain.
- Pick one vocabulary per team; do not argue over names.

**Show:** a ring diagram with arrows pointing to the centre.

**Check:** What do all three styles protect? *(The domain logic from framework and infrastructure details.)*

---

## MID-059-L05 · The modular monolith (12 min)
**Goal:** structure one deployable into modules with real boundaries.

**Key points**
- One deployment, several modules (`catalog`, `orders`, `inventory`, `payments`), each with its own domain and data.
- Each module exposes a small public API (package or interface); everything else is internal.
- Enforce boundaries by tooling: Java modules, separate Gradle/Maven modules, or ArchUnit tests, not by good intentions.
- Modules do not share tables freely; each owns its schema or tables and others call its API.
- Spring Modulith is one option to verify structure and publish events between modules (verify version before recording).
- Cheaper than microservices and the natural step before splitting.

**Show:** a package layout `orders/api`, `orders/internal`, plus an ArchUnit rule forbidding `inventory` from importing `orders.internal`.

**Check:** What makes a module boundary real? *(A tool or build rule that fails when it is crossed.)*

---

## MID-059-L06 · Demo: turning Shop into ports and adapters (14 min)
**Goal:** refactor Shop live. Prepares `MID-059-LAB1`.

**Steps**
1. Start from the layered Shop: `OrderService` imports `JpaOrderRepository` and a Stripe client.
2. Create the `orders` domain package; move `Order` as a plain class without JPA annotations.
3. Define outbound ports `OrderRepository` and `PaymentGateway` in the domain; add the inbound port `PlaceOrderUseCase`.
4. Write adapters: a JPA adapter with a separate `OrderEntity` and mapper, and a payment adapter.
5. **Planned mistake:** put `@Entity` back on the domain `Order` "to save a mapper". Add an ArchUnit test that fails on `jakarta.persistence` imports in the domain; remove the annotation and keep the mapper.
6. Swap in a fake payment adapter; the domain tests still pass untouched.

---
