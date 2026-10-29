# JNR-006 · Logging — Exercises and lab

## Lab
### JNR-006-LAB1 · Observable Shop
**Outcomes:** 1–5 · **Time:** ~1.5 h
Add SLF4J logging to Shop Core and the CLI. Switch to JSON output by configuration only. Show a masked card number in the output.
**Acceptance:** no secrets in logs; no duplicate stack traces; levels chosen correctly; JSON output enabled without code changes.

## Exercises (assessment: review a log file and a logging config for problems, plus six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-006-EX01 | 1 | Convert `System.out.println("Order " + id + " saved")` to an SLF4J call with a placeholder and the right level. |
| JNR-006-EX02 | 2 | Write a `logback.xml` with a console appender, a pattern, root `INFO`, and `com.shop` at `DEBUG`. |
| JNR-006-EX03 | 1 | Choose a level: payment declined, database down, order placed, loop variable value, retry succeeded. |
| JNR-006-EX04 | 3 | Fix a catch block that does `log.error(e.getMessage()); throw e;`. |
| JNR-006-EX05 | 4 | Write `mask(String card)` that returns only the last four digits, and list five values never to log. |
| JNR-006-EX06 | 5 | Explain in three sentences why JSON logs help, and show one example line. |

## Solutions
- **EX01** `log.info("Order {} saved", id);`
- **EX02** `<logger name="com.shop" level="DEBUG"/>` and `<root level="INFO"><appender-ref ref="STDOUT"/></root>` with `<pattern>%d %-5level %logger{20} - %msg%n</pattern>`.
- **EX03** `WARN`; `ERROR`; `INFO`; `DEBUG`; `INFO` or `WARN` (team choice, justified).
- **EX04** Either log with the exception and handle: `log.error("Payment failed", e);` or just `throw e` and log at the top level, not both.
- **EX05** `"**** **** **** " + card.substring(card.length() - 4)`. Never log: passwords, tokens, API keys, full card numbers, national IDs.
- **EX06** Machines can filter by field, count errors, and follow one request; people still read the message field.
- Outcome 2 and 5 are also covered by the lab and quiz Q02, Q09–Q10.
