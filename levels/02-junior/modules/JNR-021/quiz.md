# JNR-021 · OpenAPI — Quiz

Outcomes: O1 read a spec · O2 generate and serve docs · O3 enrich docs · O4 code-first vs contract-first.

**Q01 (O1)** OpenAPI is: A. A Java library only B. A database C. A standard description of an HTTP API D. A web server
**Q02 (O1)** Reusable schemas are defined under: A. `servers` B. `components/schemas` C. `info` D. `paths`
**Q03 (O1)** In a spec, `responses` are keyed by: A. HTTP status code B. Method name C. Class name D. Port
**Q04 (O2)** Swagger UI is: A. A test framework B. A build tool C. A database client D. A page to read and try the API
**Q05 (O2)** springdoc builds the spec from: A. Hand-written XML only B. Your controllers and DTOs C. The database schema D. Log files
**Q06 (O3)** Why add examples? A. They make the server faster B. They change status codes C. Newcomers can copy a working request D. They are required by Spring
**Q07 (O3)** Which should be documented? A. Only success responses B. Only `200` C. Nothing, the code is enough D. Error responses such as `400` and `404`
**Q08 (O3)** Docs say `200` but the code returns `201`. This is: A. Drift between docs and behavior B. Normal C. A Swagger feature D. Caching
**Q09 (O4)** Contract-first means: A. Code, then docs B. No documentation C. The spec is written and agreed before the code D. Only generated code
**Q10 (O4)** A benefit of code-first is: A. No code needed B. Docs always match the code easily C. No tests needed D. No versioning needed

## Answers
Q01 C · Q02 B · Q03 A · Q04 D · Q05 B · Q06 C · Q07 D · Q08 A · Q09 C · Q10 B

## Practical part
Six exercises `JNR-021-EX01` to `EX06` plus the documented-API lab. Pass: at least five exercises and a lab where every endpoint is callable from Swagger UI alone, with the spec committed.
