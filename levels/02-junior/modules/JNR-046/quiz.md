# JNR-046 · API testing — Quiz

Outcomes: O1 REST Assured · O2 MockMvc versus HTTP · O3 scenario coverage · O4 assertions.

**Q01 (O1)** REST Assured style is: A. `try/catch/finally` B. `arrange/act/assert` only C. `given/when/then` D. `before/after`
**Q02 (O1)** To use the random server port in a test: A. `@Value("8080")` B. `@LocalServerPort` C. `@Port` D. `@Random`
**Q03 (O2)** `@WebMvcTest` tests: A. The full app with DB B. Only the database C. Docker D. The web layer without a real server
**Q04 (O2)** Best for a full user journey with security and database: A. `@SpringBootTest` with real HTTP B. Unit test C. Mock only D. `@WebMvcTest`
**Q05 (O3)** A missing token should give: A. 200 B. 404 C. 401 D. 201
**Q06 (O3)** A user without the needed role should get: A. 200 B. 403 C. 401 D. 204
**Q07 (O3)** A scenario matrix helps you: A. Skip failures B. Hide bugs C. Delete tests D. List cases before writing tests
**Q08 (O3)** An unknown resource id should give: A. 404 B. 200 C. 401 D. 500
**Q09 (O4)** Better assertion on a response body: A. Full string equality B. Field-level checks that matter C. Only the status D. None
**Q10 (O4)** Why check headers like `Location`? A. They are decoration B. Status already covers them C. They are part of the API contract D. REST Assured requires it

## Answers
Q01 C · Q02 B · Q03 D · Q04 A · Q05 C · Q06 B · Q07 D · Q08 A · Q09 B · Q10 C

## Practical part
Six exercises `JNR-046-EX01` to `EX06` plus the lab; for the assessment, write a scenario matrix for an unseen endpoint. Pass: quiz 8/10, at least five exercises correct, and all matrix rows automated in the lab.
