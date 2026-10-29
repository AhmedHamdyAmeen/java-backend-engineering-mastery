# JNR-005 · Design patterns introduction — Exercises and lab

## Lab
### JNR-005-LAB1 · Patterns in Shop Core
**Outcomes:** 1–4 · **Time:** ~2.5 h
Add four patterns to Shop Core: Strategy for shipping, Adapter for a third-party currency API, Decorator for logging or caching a price lookup, Observer for "order placed" notifications.
**Acceptance:** each pattern is justified in the README (problem, why this pattern, one alternative considered); tests for each; no pattern where a simple function would do.

## Exercises (assessment: scenario quiz plus the lab; eight exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-005-EX01 | 1 | Write a `DiscountFactory.of(String code)` that returns a `Discount`; unknown code throws. |
| JNR-005-EX02 | 1 | Write a builder for `Order` with customer, lines, and an optional coupon; `build()` rejects an empty order. |
| JNR-005-EX03 | 1 | Implement `ShippingStrategy` as two classes and one lambda, and pick one by name. |
| JNR-005-EX04 | 1 | Write an adapter from `VendorApi.rate(String, String)` to your `CurrencyRates` interface. |
| JNR-005-EX05 | 1 | Write a `LoggingPriceLookup` decorator, and a `ProductRepository` in-memory implementation. |
| JNR-005-EX06 | 1 | Implement an `OrderPlaced` listener list with two listeners. |
| JNR-005-EX07 | 2 | Which pattern solves each: many constructor parameters; swap tax algorithm; wrap a legacy API; add caching; notify on events; hide SQL. |
| JNR-005-EX08 | 3, 4 | Name one JDK and one Spring example for three patterns. Then describe a case where a pattern is needless. |

## Solutions
- **EX01** `switch (code) { case "SUMMER10" -> new Percentage(10); ... default -> throw new IllegalArgumentException(code); }`.
- **EX02** Static nested `Builder` with fluent setters; `build()` checks `lines.isEmpty()` and returns an immutable `Order`.
- **EX03** `ShippingStrategy standard = o -> Money.eur(499);` and a pick via `Map<String, ShippingStrategy>`.
- **EX04** `class VendorRatesAdapter implements CurrencyRates { public Money convert(...) { double r = api.rate(...); ... } }`.
- **EX05** The decorator holds a `PriceLookup inner`, logs, then calls `inner.priceOf`; the repository wraps a `Map<Sku, Product>`.
- **EX06** `List<OrderListener>`; loop and call `onPlaced`. Do not depend on order.
- **EX07** Builder; Strategy; Adapter; Decorator; Observer; Repository.
- **EX08** Examples: Factory `List.of` / Spring `BeanFactory`; Strategy `Comparator` / `JdbcTemplate` callbacks; Decorator `BufferedReader` / Spring proxies. Needless: Builder for a two-field object.
- Outcome 2 and 4 are also covered by the scenario quiz in the assessment and quiz Q07–Q10.
