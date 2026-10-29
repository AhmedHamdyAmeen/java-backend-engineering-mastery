# JNR-006 · Logging — Lecture scripts

**Video:** 55 min · **Analogy used throughout:** a ship's logbook: dated entries written by the crew so that others can understand what happened later.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## JNR-006-L01 · Why `System.out` is not logging (6 min)
**Goal:** see what `println` cannot do.

**Key points**
- `println` has no time, no level, and no source class.
- You cannot turn it off or filter it without editing code.
- It goes to one place only: the console.
- Real logging adds timestamps, levels, files, and rotation.
- A logging library lets operations change the output without changing the code.

**Show:** `System.out.println("saved")` next to `2025-01-10 10:15:02 INFO  OrderService - Order 42 saved`.

**Check:** Name two things a log line has that `println` lacks. *(For example time and level.)*

---

## JNR-006-L02 · SLF4J and Logback (10 min)
**Goal:** log through SLF4J and configure Logback.

**Key points**
- SLF4J is the API you write against. Logback is the engine that writes the output.
- Create one logger per class: `LoggerFactory.getLogger(OrderService.class)`.
- Use `{}` placeholders, not string concatenation: the message is built only if the level is on.
- Logback config (`logback.xml`) has appenders (where), patterns (format), and levels (what).
- Set levels per package, for example `com.shop` at `DEBUG` and the rest at `INFO`.

**Show**
```java
private static final Logger log = LoggerFactory.getLogger(OrderService.class);
log.info("Order {} placed for customer {}", orderId, customerId);
```

**Check:** Why use `{}` and not `+`? *(The text is built only when that level is enabled.)*

---

## JNR-006-L03 · Choosing log levels (8 min)
**Goal:** pick the right level.

**Key points**
- `ERROR`: something failed and needs attention.
- `WARN`: odd, but the system carried on.
- `INFO`: important business events, such as "order placed".
- `DEBUG`: details for developers; usually off in production.
- `TRACE`: very fine detail. Do not use `ERROR` for expected cases, like a user typing a wrong password.

**Show:** a table: situation / level (payment declined: `WARN`; database down: `ERROR`; order placed: `INFO`).

**Check:** Level for "user not found, as expected"? *(Not `ERROR`; `INFO` or `DEBUG`.)*

---

## JNR-006-L04 · Logging exceptions well (7 min)
**Goal:** log an exception once, with its stack trace.

**Key points**
- Pass the exception as the last argument: `log.error("Payment failed for {}", id, e)`.
- Do not use `e.getMessage()` alone; you lose the stack trace.
- Log it once, at the place that handles it.
- Do not log and rethrow: the same error then appears many times.
- Either handle it (log) or pass it up (throw), not both.

**Show**
```java
try { pay(order); }
catch (PaymentException e) {
    log.error("Payment failed for order {}", order.id(), e);
}
```

**Check:** Why is log-and-rethrow bad? *(The same error is logged several times and confuses readers.)*

---

## JNR-006-L05 · Sensitive data in logs (7 min)
**Goal:** keep secrets and personal data out of logs.

**Key points**
- Logs are copied, stored, and read by many people.
- Never log passwords, tokens, API keys, full card numbers, or national IDs.
- Mask what you must show: `**** **** **** 1111`.
- Be careful with `toString()` of objects: it may include secrets.
- Review log statements in code review.

**Show**
```java
log.info("Charging card {}", mask(cardNumber)); // **** **** **** 1111
```

**Check:** May you log a password "just for debugging"? *(No, never.)*

---

## JNR-006-L06 · Structured logging (7 min)
**Goal:** explain why logs can be JSON.

**Key points**
- Text logs are for people; JSON logs are for machines too.
- A JSON line has named fields: time, level, message, orderId.
- Log tools can search and count by field.
- Context values (like a request ID) can be attached to every line (MDC).
- Switch format by configuration, not by code.

**Show**
```json
{"time":"2025-01-10T10:15:02Z","level":"INFO","logger":"OrderService","message":"Order placed","orderId":42}
```

**Check:** Why JSON logs? *(Machines can search and filter by field.)*

---

## JNR-006-L07 · Demo: from `println` to structured JSON logs (10 min)
**Goal:** replace `println` calls with SLF4J and JSON output. Prepares JNR-006-LAB1.

**Steps**
1. Show Shop CLI with `System.out.println` debugging.
2. Add SLF4J and Logback dependencies in the POM (verify versions before recording).
3. Replace `println` with `log.info` and placeholders.
4. **Planned mistake:** log the card number in clear text, then spot it in the output. Fix: mask it with a helper and add a test.
5. Switch the output to JSON through Logback configuration (a JSON encoder; verify the library).
6. Trigger an error and show one stack trace, not two.

**Check:** What changed between text and JSON output? *(Only the configuration.)*
