# JNR-044 · Mocking — Exercises and lab

## Lab
### JNR-044-LAB1 · Order service tests
**Outcomes:** 1–4 · **Time:** ~2.5 h
Test `OrderService` with a mocked payment gateway (success, decline, timeout) and an in-memory fake repository.
**Acceptance:** tests survive an internal refactor of the service.

## Exercises (assessment: refactor an over-mocked test suite)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-044-EX01 | 1 | Classify these as stub, mock, spy, or fake: canned exchange rate, in-memory `ProductRepository`, email sender checked for a call, real calculator with call counting. |
| JNR-044-EX02 | 2 | Stub `PaymentGateway.charge` to approve one amount and throw `GatewayTimeoutException` for another; test both. |
| JNR-044-EX03 | 2 | Verify that `EmailSender.sendConfirmation` is called once on success and `never()` on decline. |
| JNR-044-EX04 | 3 | Use an `ArgumentCaptor` to assert the saved `Order` has status `PAID` and the correct total. |
| JNR-044-EX05 | 4 | Given a test with eight mocks and 12 `verify` lines, remove the unnecessary verifies and replace the repository mock with a fake. |
| JNR-044-EX06 | 4 | A test mocks `HttpClient` directly. Redesign it with your own `RateProvider` interface. |
| JNR-044-EX07 | 4 | Explain what "mocks returning mocks" says about the design and how to fix it. |

## Solutions
- **EX01** Stub, fake, mock, spy.
- **EX02** `when(gateway.charge(any(), eq(a))).thenReturn(approved)` and `when(gateway.charge(any(), eq(b))).thenThrow(new GatewayTimeoutException())`; assert the result state of each order.
- **EX03** `verify(emailSender).sendConfirmation(id)` and `verify(emailSender, never()).sendConfirmation(any())`.
- **EX04** `verify(repo).save(captor.capture()); assertThat(captor.getValue().status()).isEqualTo(PAID);` plus a total assertion.
- **EX05** Keep only side-effect verifies (charge, email); assert on returned order and fake repository content.
- **EX06** Define `interface RateProvider { BigDecimal rate(String code); }` implemented by an `HttpClient` adapter; mock or fake `RateProvider` in unit tests; test the adapter separately.
- **EX07** The code reaches through several objects (law of Demeter) or the test is too coupled; pass the needed value in, or return a simple value from the first collaborator.
- Outcome 1 is also covered by quiz Q01–Q02; the "survives a refactor" acceptance in the lab covers outcome 4.
