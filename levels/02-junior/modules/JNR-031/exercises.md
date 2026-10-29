# JNR-031 · Transactions — Exercises and lab

## Lab
### JNR-031-LAB1 · Place order
**Outcomes:** 1–5 · **Time:** ~3 h
1. Implement `OrderService.placeOrder` that reserves stock and creates the order in one transaction.
2. Write failure tests: out-of-stock on the second line and a forced exception after saving the order; assert no stock change and no order row remains.
3. Add `readOnly = true` on the order query method.
4. Fix the provided money-transfer exercise that has a planted self-invocation bug; add a test that fails first.
5. Keep any payment call outside the transaction (a stub is enough).

**Acceptance:** failure tests prove atomicity.

## Exercises (assessment: fix a broken transaction implementation and explain why it failed)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-031-EX01 | 1 | Give one concrete failure for each of A, C, I, and D using Shop examples. |
| JNR-031-EX02 | 2 | Move `@Transactional` from the controller to the correct service method. |
| JNR-031-EX03 | 3 | A method throws a checked `PaymentException` and data is still committed. Fix it in two ways. |
| JNR-031-EX04 | 4 | Explain in your own words why `this.method()` skips the transaction, and give two fixes. |
| JNR-031-EX05 | 5 | Restructure `placeOrder` so the payment API is called outside the transaction. |
| JNR-031-EX06 | 3, 4 | Fix a broken transaction implementation (provided) and write the explanation. |

## Solutions
- **EX01** A: crash after debit, before credit. C: stock would become negative. I: another request reads half-updated stock. D: committed order disappears after a restart without durability.
- **EX02** The service method `placeOrder` gets `@Transactional`; controllers stay free of it.
- **EX03** `@Transactional(rollbackFor = PaymentException.class)` or make the exception extend `RuntimeException`.
- **EX04** The proxy intercepts only calls from other beans; `this` is the raw object. Fix: move the method to another bean, or put the annotation on the public entry method.
- **EX05** Call payment first (or after commit) in a non-transactional coordinator method; the transactional part only reserves stock and saves the order.
- **EX06** Typical faults: annotation on a private method, a swallowed exception in a `catch`, or self-invocation; fix and describe which proxy rule was broken.
- Outcome 1 is also covered by the quiz.
