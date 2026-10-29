# JNR-045 · Integration testing — Quiz

Outcomes: O1 Testcontainers tests · O2 service connections · O3 data isolation · O4 H2 versus production database.

**Q01 (O1)** Integration tests mainly prove: A. Private method logic B. Code style C. Parts work together with real infrastructure D. Compiler speed
**Q02 (O1)** Testcontainers needs which tool running? A. Kubernetes B. Docker C. Jenkins D. Nothing
**Q03 (O1)** `@DataJpaTest` loads: A. The JPA slice only B. The whole app and web server C. Only controllers D. Nothing
**Q04 (O1)** To keep your PostgreSQL container with `@DataJpaTest` use: A. `@MockBean` B. `@Disabled` C. `@AutoConfigureTestDatabase(replace = NONE)` D. `@Nested`
**Q05 (O2)** `@ServiceConnection` does what? A. Starts Kubernetes B. Configures the datasource from the container C. Mocks the database D. Deletes tables
**Q06 (O3)** Shared mutable data between tests causes: A. Order-dependent failures B. Faster tests C. Better coverage D. Smaller JARs
**Q07 (O3)** A good way to avoid data collisions: A. Fixed emails B. Unique data per test C. Sleep in tests D. Share rows across tests
**Q08 (O3)** `@Transactional` on a test does not roll back data created: A. In the repository B. In memory C. By real HTTP requests handled on another thread D. In a method
**Q09 (O4)** Why is H2 not a substitute for PostgreSQL? A. Behavior and SQL differ B. It is always faster C. It needs Docker D. It has no tables
**Q10 (O4)** A query passing on H2 but failing in production shows: A. Bad network B. Production bug in Docker C. Test data too small D. H2 hid a difference in SQL behavior

## Answers
Q01 C · Q02 B · Q03 A · Q04 C · Q05 B · Q06 A · Q07 B · Q08 C · Q09 A · Q10 D

## Practical part
Seven exercises `JNR-045-EX01` to `EX07` plus the lab; for the assessment, add integration tests for an untested repository. Pass: quiz 8/10, at least five exercises correct, and the suite green on a clean machine with only Docker.
