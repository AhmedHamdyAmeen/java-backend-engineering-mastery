# JNR-054 · Troubleshooting — Lecture scripts

**Video:** 55 min · **Analogy used throughout:** a doctor diagnosing a patient: symptoms, history, one test at a time, then treatment.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## JNR-054-L01 · A troubleshooting method (8 min)
**Goal:** follow a repeatable method instead of guessing.

**Key points**
- Steps: reproduce, narrow down, form one hypothesis, test it, fix, verify, prevent.
- Reproduce first; a bug you cannot reproduce you cannot confirm fixed.
- Change one thing at a time and note what you changed.
- Ask "what changed?": a deploy, config, data, or dependency.
- Write down what you tried; it helps you and others.

**Show:** a loop diagram: Observe, Hypothesis, Experiment, Result, back to Observe.

**Check:** Why change only one thing at a time? *(So you know which change had the effect.)*

---

## JNR-054-L02 · Logs and stack traces in production (12 min)
**Goal:** read deployed logs to find where a failure starts.

**Key points**
- Find the time of the problem, then read around it (`docker logs --since 10m`, `journalctl -u shop --since ...`).
- In a stack trace, read the exception type and message, then the "Caused by" chain to the root cause; the first lines of your own package show where.
- Use a request or correlation id to follow one request through the logs.
- Search for `ERROR` and `WARN`, then look at the lines just before the first error.
- Do not log secrets or personal data.

**Show**
```text
ERROR OrderService - Could not place order 4711
org.springframework.dao.DataIntegrityViolationException: ...
Caused by: org.postgresql.util.PSQLException: ERROR: null value in column "currency"
	at com.shop.order.OrderService.place(OrderService.java:58)
```

**Check:** Which part of a stack trace usually names the root cause? *(The last "Caused by".)*

---

## JNR-054-L03 · Environment differences (10 min)
**Goal:** explain "works on my machine".

**Key points**
- Compare config (environment variables, profiles), data (size, special values), and versions (Java, database, libraries).
- Check the image tag and Git commit that is actually running.
- Production data has cases test data lacks: nulls, long text, accents, large volumes.
- Time zones, locales, and file paths differ between machines.
- Make environments alike: same image, same database version (Testcontainers helps).

**Show:** a table: item / local / production, with rows for Java version, DB version, profile, data size, time zone.

**Check:** Name two kinds of environment difference. *(For example config values, data, library versions.)*

---

## JNR-054-L04 · From bug to regression test (8 min)
**Goal:** lock in the fix with a test.

**Key points**
- First write a test that reproduces the bug and fails.
- Then fix the code until the test passes.
- Choose the lowest test level that reproduces it: unit if possible, integration if it depends on the database.
- The test name describes the behavior: `acceptsOrderWithoutCoupon`.
- A short bug report records symptom, root cause, fix, and the test.

**Show:** a bug report template: Symptom, Steps to reproduce, Root cause, Fix, Regression test, Prevention.

**Check:** When do you write the regression test? *(Before the fix, so you see it fail.)*

---

## JNR-054-L05 · Asking for help well (7 min)
**Goal:** ask questions that get fast answers.

**Key points**
- Try for a bounded time first (for example 30 minutes), then ask.
- Say what you expected, what happened, and what you already tried.
- Include the error text, version, a minimal example, and links to logs or the PR.
- Ask in the team channel when others may benefit.
- Write down the answer; thank the helper.

**Show:** a good message: "Order API returns 500 for orders without a coupon on staging; local is fine. Logs: link. I compared env vars and Java versions; same. Next I will check the DB data. Any idea?"

**Check:** What three things should a question include? *(Expected result, actual result, what you tried.)*

---

## JNR-054-L06 · Demo: diagnosing a production fault from logs (10 min)
**Goal:** work from logs to root cause, fix, and test. Prepares `JNR-054-LAB1`.

**Steps**
1. A user reports "orders fail". Note the time and find the logs.
2. Locate the first `ERROR`; read the "Caused by" chain to the root cause.
3. Reproduce locally by creating the same data in a test.
4. Write the failing regression test, then fix the code, then run the test.
5. **Planned mistake:** changing the config and the code at the same time; revert one so you know which change fixed it.
6. Write a short bug report with root cause, fix, and test.
