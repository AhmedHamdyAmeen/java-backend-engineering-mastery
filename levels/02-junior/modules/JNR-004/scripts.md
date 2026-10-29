# JNR-004 · SOLID principles — Lecture scripts

**Video:** 70 min · **Analogy used throughout:** a kitchen with a power socket: any appliance with the right plug works, and the kitchen does not care which brand.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## JNR-004-L01 · Single Responsibility (12 min)
**Goal:** give each class one reason to change.

**Key points**
- SOLID is five design guidelines for classes. Guidelines, not laws.
- S: a class should have one reason to change.
- "One responsibility" does not mean "one method".
- Smell: a class that changes for tax rules, for email text, and for database changes.
- Fix: extract classes, each with one clear job.

**Show**
```java
class OrderService {
    void place(Order o) { /* calculate tax, save, send email */ }
}
// split: TaxCalculator, OrderRepository, OrderNotifier
```

**Check:** Does SRP mean one method per class? *(No; it means one reason to change.)*

---

## JNR-004-L02 · Open/Closed (10 min)
**Goal:** add behavior without editing working code.

**Key points**
- O: open for extension, closed for modification.
- Smell: an `if/else` or `switch` on type that grows with every new feature.
- Fix: an interface with a new class per case.
- Then a new case means a new class, and old classes stay untouched.
- With a sealed type, the compiler lists what to update; both styles can be fine.

**Show**
```java
interface TaxRule { Money tax(Money net); }
class VatRule implements TaxRule { ... }
// adding a new rule = adding a class
```

**Check:** What does "closed for modification" mean? *(Adding a feature does not require editing existing, tested code.)*

---

## JNR-004-L03 · Liskov Substitution (10 min)
**Goal:** make subtypes safe to use in place of their parent.

**Key points**
- L: code that uses the parent type must work with any subtype.
- Like the socket: any plug that fits must work.
- Violation: a subclass throws `UnsupportedOperationException` for an inherited method.
- Violation: a subclass breaks a promise of the parent, such as "never returns null".
- Fix: change the hierarchy or use composition.

**Show**
```java
class Penguin extends Bird { void fly() { throw new UnsupportedOperationException(); } }
// callers of Bird.fly() break
```

**Check:** Why is throwing `UnsupportedOperationException` in an override a smell? *(Callers of the parent type break.)*

---

## JNR-004-L04 · Interface Segregation (8 min)
**Goal:** keep interfaces small and focused.

**Key points**
- I: do not force a class to implement methods it does not use.
- A large interface makes many empty or throwing methods.
- Split into small interfaces, each for one role.
- Clients depend only on what they use.
- Example: `Readable` and `Writable` instead of one `Storage`.

**Show**
```java
interface PriceReader { Money priceOf(Sku sku); }
interface PriceWriter { void save(Sku sku, Money price); }
```

**Check:** What problem does a fat interface cause? *(Implementers must provide methods they do not need.)*

---

## JNR-004-L05 · Dependency Inversion (12 min)
**Goal:** make high-level code depend on interfaces, not on concrete details.

**Key points**
- D: high-level code and low-level code both depend on an interface.
- Like the socket: the kitchen depends on the socket shape, not the appliance.
- Pass dependencies in through the constructor (dependency injection).
- Benefit: in tests, pass a fake instead of the real thing.
- Spring's dependency injection is built on this idea.

**Show**
```java
interface PaymentProvider { Receipt charge(Money amount); }
class CheckoutService {
    private final PaymentProvider payments;
    CheckoutService(PaymentProvider payments) { this.payments = payments; }
}
```

**Check:** Why does DI make testing easier? *(You can pass a fake in place of the real dependency.)*

---

## JNR-004-L06 · SOLID with judgment (8 min)
**Goal:** know when a principle adds needless complexity.

**Key points**
- Do not make an interface for every class; one implementation and no need to swap means no interface.
- Do not split a class so much that you cannot follow the flow.
- Apply a principle when you feel the pain: a hard-to-change or hard-to-test spot.
- Prefer the simplest design that is easy to change.
- Discuss trade-offs in code review, not rules.

**Show:** two designs for a simple tax calculation: one with six interfaces, one with a small function.

**Check:** When is an interface not needed? *(One implementation, no tests or swapping that need it.)*

---

## JNR-004-L07 · Demo: dependency inversion for a payment provider (10 min)
**Goal:** inject a payment provider through an interface. Prepares JNR-004-LAB1.

**Steps**
1. Show `CheckoutService` calling `new StripeClient()` directly; tests need the network.
2. Extract the `PaymentProvider` interface.
3. Inject it through the constructor.
4. **Planned mistake:** the interface exposes Stripe-specific types, so the core still depends on Stripe. Fix: use Shop's own types (`Money`, `Receipt`) in the interface.
5. Write a fake provider for tests; run them without a network.
6. Add a second provider without touching `CheckoutService`.

**Check:** Where should the interface live? *(In the core, not in the provider's code.)*
