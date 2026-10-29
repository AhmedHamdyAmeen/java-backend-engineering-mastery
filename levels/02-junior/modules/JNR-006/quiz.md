# JNR-006 · Logging — Quiz

Outcomes: O1 SLF4J and levels · O2 Logback config · O3 exceptions · O4 sensitive data · O5 structured logging.

**Q01 (O1)** SLF4J is: A. A database B. A logging API C. A web server D. A test tool
**Q02 (O1)** Which is the best log call? A. `log.info("Order " + id)` B. `System.out.println(id)` C. `log.info(id)` D. `log.info("Order {}", id)`
**Q03 (O1)** Which level for an expected "user not found"? A. `ERROR` B. `FATAL` C. `INFO` or `DEBUG` D. None
**Q04 (O2)** In Logback, an appender defines: A. The Java version B. Where logs go C. The class name D. The test order
**Q05 (O2)** You can set `com.shop` to `DEBUG` and the rest to `INFO` using: A. Per-package logger levels B. Code changes only C. Maven scopes D. A new class
**Q06 (O3)** How do you log an exception with its stack trace? A. `log.error(e.getMessage())` B. `log.error("Failed", e)` C. `System.out.println(e)` D. Ignore it
**Q07 (O3)** Log-and-rethrow is a problem because: A. It is faster B. It is required C. The same error is logged many times D. It hides the level
**Q08 (O4)** Which must never be logged? A. Order ID B. Item count C. Time taken D. A password
**Q09 (O4)** A good way to log a card number is: A. In clear text B. Hash only C. Masked, last four digits only D. Base64
**Q10 (O5)** JSON logs help because: A. Machines can search by field B. They are smaller C. They need no library D. They remove levels

## Answers
Q01 B · Q02 D · Q03 C · Q04 B · Q05 A · Q06 B · Q07 C · Q08 D · Q09 C · Q10 A

## Practical part
Six exercises `JNR-006-EX01` to `EX06` plus the lab; the assessment reviews a log file and a logging config for problems. Pass: at least 8 of 10 quiz answers, five exercises correct, and a lab with no secrets and no duplicate stack traces in the logs.
