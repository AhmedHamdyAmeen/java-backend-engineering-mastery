# JNR-016 · Spring testing basics — Quiz

Outcomes: O1 plain unit tests · O2 `@WebMvcTest` and MockMvc · O3 basic Mockito · O4 slice vs full context.

**Q01 (O1)** A service with constructor injection can be unit-tested by: A. Starting the full app B. Calling `new` with fakes C. Using a database D. It cannot be tested without Spring
**Q02 (O1)** Which test type should be the most numerous? A. Full-context B. End-to-end in a browser C. Manual D. Plain unit tests
**Q03 (O2)** `@WebMvcTest` loads: A. The whole application B. Only the web layer for the chosen controllers C. Only the database D. Nothing
**Q04 (O2)** `MockMvc` is used to: A. Send fake HTTP requests without a real server B. Mock the database C. Start Tomcat D. Generate JSON
**Q05 (O2)** For a controller validation test, assert: A. Only that a response arrives B. Status 400 and the error body C. The log file D. The Maven version
**Q06 (O3)** `when(repo.findById(1L)).thenReturn(...)` does what? A. Calls the real repository B. Deletes data C. Defines the answer the mock returns D. Starts a transaction
**Q07 (O3)** What should you mock in a controller test? A. The controller B. The service the controller calls C. The JSON library D. The test class
**Q08 (O3)** Asserting only the status code in a test is: A. Always sufficient B. Weak: the body could be wrong C. Required D. Illegal
**Q09 (O4)** `@SpringBootTest` is costly because: A. It starts the whole application context B. It uses a different language C. It runs once only D. It disables tests
**Q10 (O4)** A new `@MockitoBean` or changed properties often: A. Reuse the cache B. Speed things up C. Are ignored D. Create a new context and slow the suite

## Answers
Q01 B · Q02 D · Q03 B · Q04 A · Q05 B · Q06 C · Q07 B · Q08 B · Q09 A · Q10 D

## Practical part
Six exercises `JNR-016-EX01` to `EX06` plus the lab. The assessment: write the missing tests for a provided controller (success, validation failure, not found). Pass: quiz at least 8/10, the three missing tests written and passing with body assertions, lab acceptance met.
