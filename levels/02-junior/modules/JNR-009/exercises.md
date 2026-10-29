# JNR-009 · IoC and DI — Exercises and lab

## Lab
### JNR-009-LAB1 · Inject Shop Core
**Outcomes:** 1–4 · **Time:** ~2 h
1. Take Shop Core's services (pricing, orders, payments) and the pricing strategies (for example `RegularPricing`, `DiscountPricing`).
2. Register them as beans and inject through constructors.
3. Add two `PaymentProvider` implementations; choose the one for orders with `@Qualifier`.
4. Add a `@PostConstruct` log line to one bean and watch the order in the startup log.
**Acceptance:** no `new` for collaborators inside services; no field injection; the app starts with two payment providers present.

## Exercises (assessment: explain a DI wiring diagram and fix an ambiguous-bean failure)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-009-EX01 | 1 | Without Spring, refactor a class that does `new EmailSender()` so the sender is passed in; write a test using a fake. |
| JNR-009-EX02 | 1 | Explain IoC and DI in your own words and name who creates objects in each style. |
| JNR-009-EX03 | 2 | Convert a field-injected service to constructor injection; list two benefits. |
| JNR-009-EX04 | 3 | Given two beans of one interface and a startup failure, fix it with `@Primary`, then with `@Qualifier`. |
| JNR-009-EX05 | 4 | Add `@PostConstruct` and `@PreDestroy` logs to a bean and predict the order relative to the constructor. |
| JNR-009-EX06 | 2 | Break a circular dependency between two services by extracting a third class. |
| JNR-009-EX07 | 1 | Draw the wiring diagram for `OrderController → OrderService → PaymentProvider, PricingStrategy`, and mark who creates each. |

## Solutions
- **EX01** `class Notifier { private final EmailSender sender; Notifier(EmailSender s){this.sender=s;} }` with `new Notifier(new FakeEmailSender())` in the test.
- **EX02** IoC: the framework, not your class, creates and connects objects. DI: dependencies are passed in (constructor). By hand, `main` or the class creates; with Spring, the container.
- **EX03** Benefits: `final` fields and complete objects; easy `new` in tests; dependencies visible in the signature.
- **EX04** `@Primary` on the default implementation. Or `@Qualifier("paypal")` on the constructor parameter.
- **EX05** Constructor, injection, `@PostConstruct`, (use), `@PreDestroy` on shutdown.
- **EX06** Move the shared logic into `StockPolicy`; both services depend on it; no cycle.
- **EX07** Spring creates all four beans; the controller gets the service, the service gets the provider and strategy. The wiring-diagram part of the assessment is covered by this exercise and the lab acceptance.
