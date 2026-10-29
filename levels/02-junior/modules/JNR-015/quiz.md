# JNR-015 · Error handling — Quiz

Outcomes: O1 exception hierarchy · O2 central mapping · O3 Problem Details · O4 no leaks.

**Q01 (O1)** An unknown product id should lead to HTTP: A. 200 B. 500 C. 400 D. 404
**Q02 (O1)** Who should pick the HTTP status? A. The repository B. The central handler, from the exception type C. The database D. The client
**Q03 (O1)** A duplicate SKU maps best to: A. 409 B. 404 C. 200 D. 503
**Q04 (O2)** `@RestControllerAdvice` is used to: A. Define routes B. Handle exceptions for all controllers in one place C. Validate DTOs D. Create beans
**Q05 (O2)** Putting `try/catch` in every controller is: A. Required B. Best practice C. Duplication; centralize it D. Faster
**Q06 (O3)** Problem Details is defined by: A. RFC 9457 B. JPA C. HTTP/1.0 D. Jakarta Validation
**Q07 (O3)** Its content type is: A. `text/plain` B. `application/problem+json` C. `application/xml` D. `application/error`
**Q08 (O3)** Which type does Spring provide for it? A. `ErrorBody` B. `ResponseEntity` only C. `ApiError` D. `ProblemDetail`
**Q09 (O4)** Where should a stack trace go? A. The response body B. The page title C. The server log D. A cookie
**Q10 (O4)** A 500 response for an unexpected error should contain: A. The exception message B. A generic message C. The SQL D. The class name

## Answers
Q01 D · Q02 B · Q03 A · Q04 B · Q05 C · Q06 A · Q07 B · Q08 D · Q09 C · Q10 B

## Practical part
Five exercises `JNR-015-EX01` to `EX05` plus the lab. The assessment is the error-contract review (EX05). Pass: quiz at least 8/10, EX05 finds all three flaws, lab acceptance met.
