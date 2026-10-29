# MID-045 · Advanced testing — Quiz

Outcomes: O1 limits of end-to-end tests · O2 consumer-driven contracts · O3 contracts in CI · O4 property-based tests.

**Q01 (O1)** A main weakness of end-to-end tests across many services: A. They are too fast B. They need no environment C. They only test one class D. They are slow and brittle
**Q02 (O1)** Most checks should be: A. At lower levels (unit, integration, contract) B. End-to-end C. Manual only D. Skipped
**Q03 (O2)** In a consumer-driven contract, the expectations come from: A. The provider only B. A random generator C. The consumer D. The database
**Q04 (O2)** A contract should assert: A. The entire payload byte for byte B. Only the fields the consumer uses C. Server logs D. The provider's class names
**Q05 (O2)** Message contracts apply to: A. HTTP only B. Databases only C. Logs D. Kafka events as well as HTTP
**Q06 (O3)** The provider verifies contracts: A. In its own pipeline against the real provider code B. Manually once a year C. In production only D. Never
**Q07 (O3)** The provider renames a field a consumer uses. Result: A. Nothing B. The provider build fails C. The consumer build passes silently in production D. The broker restarts
**Q08 (O3)** Safe way to remove a field: A. Delete it at once B. Rename it quietly C. Add the replacement, migrate consumers, then remove D. Ask the consumer to guess
**Q09 (O4)** A property-based test: A. Checks a fixed list of examples B. Checks a rule over many generated inputs C. Replaces all unit tests D. Needs no assertions
**Q10 (O4)** Shrinking in jqwik: A. Reduces the number of tests B. Compresses reports C. Reduces a failing input to a minimal one D. Deletes the generator

## Answers
Q01 D · Q02 A · Q03 C · Q04 B · Q05 D · Q06 A · Q07 B · Q08 C · Q09 B · Q10 C

## Practical part
Seven exercises `MID-045-EX01` to `EX07` (EX07 is the test-strategy question) plus the contracts lab. Pass: at least five exercises and a lab where renaming a field fails the provider build.
