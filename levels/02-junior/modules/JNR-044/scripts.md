# JNR-044 · Mocking — Lecture scripts

**Video:** 55 min · **Analogy used throughout:** a film set with stand-ins: a stunt double, a prop, a script supervisor, and a cardboard cutout.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## JNR-044-L01 · Test doubles taxonomy (8 min)
**Goal:** name the kinds of test double and pick the right one.

**Key points**
- A test double is any stand-in for a real collaborator during a test.
- A **stub** returns canned answers. A **mock** also records calls so you can verify them.
- A **spy** wraps a real object and records calls. A **fake** is a simple working version, such as an in-memory repository.
- Prefer a fake or the real object when it is cheap; use a mock when you must check an interaction or simulate failure.
- The goal is to isolate the code under test, not to remove every dependency.

**Show:** a table: type / what it does / Shop example (stub: exchange rates; mock: email sender; spy: real calculator; fake: in-memory `OrderRepository`).

**Check:** Which double is a working in-memory version of a repository? *(A fake.)*

---

## JNR-044-L02 · Stubbing with Mockito (10 min)
**Goal:** make a mock return values or throw exceptions.

**Key points**
- `@ExtendWith(MockitoExtension.class)` with `@Mock` and `@InjectMocks` sets things up. Verify the current Mockito version before recording.
- `when(mock.method(arg)).thenReturn(value)` stubs a return.
- `thenThrow(...)` simulates failure, such as a timeout.
- Unstubbed methods return defaults (null, 0, empty collections).
- Use argument matchers (`any()`, `eq()`) sparingly, and if one argument uses a matcher, all must.

**Show**
```java
when(gateway.charge(any(), eq(new BigDecimal("50.00"))))
    .thenReturn(PaymentResult.approved("tx-1"));
when(gateway.charge(any(), eq(new BigDecimal("99.00"))))
    .thenThrow(new GatewayTimeoutException());
```

**Check:** What does an unstubbed method returning a `List` give? *(An empty list.)*

---

## JNR-044-L03 · Verifying interactions (8 min)
**Goal:** check that an important call happened, and only that.

**Key points**
- `verify(mock).method(arg)` checks the call happened once.
- `verify(mock, never())` and `times(n)` check absence and counts.
- Verify calls with real side effects (send email, charge card), not every internal call.
- Verifying everything freezes the implementation; refactoring then breaks tests that should pass.
- Prefer asserting on results and state when you can.

**Show**
```java
service.placeOrder(cmd);
verify(emailSender).sendConfirmation(order.id());
verify(gateway, never()).refund(any());
```

**Check:** Name one call worth verifying. *(One with a side effect outside the object, such as sending an email.)*

---

## JNR-044-L04 · Argument captors (7 min)
**Goal:** inspect the object that was passed to a collaborator.

**Key points**
- `ArgumentCaptor<T>` records the argument of a call.
- Use it when the code builds an object and hands it away (for example a saved `Order`).
- Capture with `verify(...).save(captor.capture())`, then `captor.getValue()`.
- Assert on the captured object with AssertJ.
- Do not capture when you can assert on a returned value.

**Show**
```java
var captor = ArgumentCaptor.forClass(Order.class);
verify(orderRepository).save(captor.capture());
assertThat(captor.getValue().status()).isEqualTo(OrderStatus.PAID);
```

**Check:** When is a captor useful? *(When the object you want to check is passed to a collaborator, not returned.)*

---

## JNR-044-L05 · When not to mock (12 min)
**Goal:** recognize over-mocking and choose better options.

**Key points**
- Do not mock types you do not own (JDBC, `HttpClient`); wrap them in your own interface and mock or fake that.
- Do not mock value objects, simple data classes, or collections; use real ones.
- A mock that returns another mock signals bad design or a leaky test.
- Verifying every call ties the test to the implementation.
- Prefer a fake repository for logic tests; prove the real database in integration tests.

**Show:** a "before" test with eight mocks and twelve `verify` lines, and an "after" using a fake repository, one mocked gateway, and result assertions.

**Check:** Why avoid mocking a JDBC `Connection`? *(You do not own that type; the test would mirror its internals, not behavior.)*

---

## JNR-044-L06 · Demo: mocking the payment gateway's three outcomes (10 min)
**Goal:** test `OrderService` for success, decline, and timeout. Prepares `JNR-044-LAB1`.

**Steps**
1. Create an in-memory fake `OrderRepository`.
2. Mock `PaymentGateway`; stub an approval and assert the order is `PAID`.
3. Stub a decline and assert the order is `PAYMENT_FAILED`.
4. Stub `thenThrow(new GatewayTimeoutException())` and assert the order stays `PENDING`.
5. **Planned mistake:** verify five internal calls; then rename a private method and watch the test break for no good reason. Fix by asserting on results.
