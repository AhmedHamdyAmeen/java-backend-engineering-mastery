# JNR-047 · Testing practices — Exercises and lab

## Lab
### JNR-047-LAB1 · Suite cleanup
**Outcomes:** 1–4 · **Time:** ~2 h
Refactor the Shop test suite: builders, deterministic clocks, no order dependence; record runtime before and after.
**Acceptance:** 10 consecutive runs green.

## Exercises (assessment: test-quality review)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-047-EX01 | 1 | Rename `test1`, `placeOrderTest`, and `testCart` into behavior names and restructure one test as Arrange-Act-Assert. |
| JNR-047-EX02 | 2 | Write a `ProductBuilder` with defaults and use it in three tests. |
| JNR-047-EX03 | 2 | Create an object mother with `outOfStock()`, `expensive()`, and `discounted()`. |
| JNR-047-EX04 | 3 | Make a coupon-expiry test deterministic with an injected `Clock`. |
| JNR-047-EX05 | 3 | Replace a `Thread.sleep(1000)` with Awaitility or a synchronous call. |
| JNR-047-EX06 | 3 | List four causes of flaky tests and one fix for each. |
| JNR-047-EX07 | 4 | Given 5 unit, 40 slice, and 120 full integration tests, explain what is wrong and how to rebalance. |

## Solutions
- **EX01** `placingOrderReducesStock`, `rejectsOrderWhenCartIsEmpty`, `totalIncludesTax`.
- **EX02** Defaults valid; `aProduct().withStock(0).build()`.
- **EX03** `static Product outOfStock() { return aProduct().withStock(0).build(); }` and so on.
- **EX04** `Clock.fixed(Instant.parse(...), UTC)` passed into the service; assert before and after expiry by moving the clock.
- **EX05** `await().atMost(2, SECONDS).until(() -> repo.count() == 1);`, or make the code run synchronously in tests.
- **EX06** Time (fixed clock), order (isolated data), randomness (seed), async/network (await or stub).
- **EX07** Too many slow tests; move logic checks down to unit tests and keep a few integration journeys.
- Common mistakes (tests coupled to implementation) are checked in the assessment review.
