# JNR-009 · IoC and DI — Lecture scripts

**Video:** 74 min · **Analogy used throughout:** a restaurant kitchen where a manager hands each cook the tools needed, instead of each cook fetching their own.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## JNR-009-L01 · Wiring by hand: the problem (8 min)
**Goal:** see why creating collaborators inside a class hurts.

**Key points**
- If `OrderService` does `new StripePayment()` itself, it is glued to that class.
- You cannot swap the payment provider or test the service with a fake.
- A dependency is any object a class needs to do its work.
- Hard-wiring spreads: change one constructor and many places break.

**Show**
```java
class OrderService {
    private final PaymentProvider payment = new StripePayment(); // glued
}
```

**Check:** Why is this hard to test? *(The service always uses the real provider; you cannot give it a fake.)*

---

## JNR-009-L02 · Inversion of control (8 min)
**Goal:** explain IoC and dependency injection without Spring.

**Key points**
- Inversion of control (IoC): someone else creates and connects your objects; you stop doing it.
- Dependency injection (DI) is the common form: dependencies are handed in from outside.
- The class declares what it needs; it does not decide which implementation.
- Depend on an interface (`PaymentProvider`), not a concrete class.

**Show**
```java
class OrderService {
    private final PaymentProvider payment;
    OrderService(PaymentProvider payment) { this.payment = payment; }
}
var service = new OrderService(new StripePayment()); // main() acts as the "container"
```

**Check:** Who decides which implementation is used now? *(The caller or container, not the service.)*

---

## JNR-009-L03 · Constructor injection (10 min)
**Goal:** use constructor injection and say why it beats field injection.

**Key points**
- Spring passes beans into the constructor. With one constructor, `@Autowired` is not needed.
- Fields can be `final`: the object is complete and never half-built.
- Dependencies are visible in the signature; tests just call `new`.
- Field injection (`@Autowired` on a field) hides dependencies, needs reflection in tests, and prevents `final`.

**Show**
```java
@Service
public class OrderService {
    private final PaymentProvider payment;
    public OrderService(PaymentProvider payment) { this.payment = payment; }
}
```

**Check:** Why can a constructor-injected field be `final`? *(It is set once, in the constructor.)*

---

## JNR-009-L04 · Multiple implementations (10 min)
**Goal:** resolve ambiguity with `@Primary` and `@Qualifier`.

**Key points**
- Two beans of the same type make Spring unable to choose: `NoUniqueBeanDefinitionException`.
- `@Primary` marks the default choice.
- `@Qualifier("name")` at the injection point picks a specific bean.
- Injecting a `List<PricingStrategy>` collects all implementations.
- Bean names default to the class name with a lowercase first letter.

**Show**
```java
@Component @Primary class StripePayment implements PaymentProvider {}
@Component("paypal") class PayPalPayment implements PaymentProvider {}

OrderService(@Qualifier("paypal") PaymentProvider payment) { ... }
```

**Check:** You want one default and one exception. Which annotations? *(`@Primary` on the default, `@Qualifier` where the exception is used.)*

---

## JNR-009-L05 · Bean lifecycle and callbacks (8 min)
**Goal:** name the four lifecycle stages.

**Key points**
- Stages: instantiation (constructor), injection of dependencies, initialization, destruction at shutdown.
- `@PostConstruct` runs after injection; `@PreDestroy` runs before the bean is removed.
- Use callbacks for light setup and cleanup, not heavy work.
- Never use injected fields inside the constructor body of a field-injected bean: they are not set yet.

**Show:** a timeline: constructor → dependencies set → `@PostConstruct` → bean in use → `@PreDestroy`.

**Check:** Which runs first, `@PostConstruct` or injection? *(Injection.)*

---

## JNR-009-L06 · Circular dependencies and how to avoid them (6 min)
**Goal:** recognize and remove a cycle.

**Key points**
- A needs B and B needs A: with constructors Spring cannot build either, and fails at startup.
- `@Lazy` can hide the cycle but not fix the design.
- A cycle means responsibilities are tangled.
- Fix: extract the shared part into a third class, or move the call to an event or a method parameter.

**Show:** `OrderService ⇄ InventoryService`; extract `StockPolicy` that both use.

**Check:** Why is `@Lazy` a poor fix? *(It hides a design problem instead of removing it.)*

---

## JNR-009-L07 · Demo: wiring Shop Core by hand, then with Spring (12 min)
**Goal:** move Shop Core from manual `new` to Spring beans; prepares JNR-009-LAB1.

**Steps**
1. Show `main` building `PricingService`, `PaymentProvider`, and `OrderService` with `new`.
2. Annotate the services with `@Service` and keep constructor parameters.
3. Delete the `new` calls from `main`; run the Boot app.
4. **Planned mistake:** put `@Autowired` on a field and write a unit test with `new OrderService(...)`; the field is null and the test fails. Fix: switch to constructor injection.
5. Show that the unit test now passes a fake `PaymentProvider`.

---

## JNR-009-L08 · Demo: diagnosing an ambiguous-bean startup failure (12 min)
**Goal:** read the failure message and fix it three ways; prepares the assessment.

**Steps**
1. Add a second `PaymentProvider` implementation and start the app.
2. Read the report: it says `expected single matching bean but found 2` and lists both names.
3. **Planned mistake:** "fix" it by deleting one implementation. Explain why that removes a needed feature.
4. Fix 1: `@Primary` on the default. Fix 2: `@Qualifier("paypal")` at the injection point.
5. Fix 3: inject `Map<String, PaymentProvider>` and choose by key at run time.
6. Run again and confirm the app starts.
