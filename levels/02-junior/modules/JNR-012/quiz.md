# JNR-012 · Configuration management — Quiz

Outcomes: O1 YAML and profiles · O2 typed properties · O3 validation · O4 precedence.

**Q01 (O1)** Which file adds settings only for the `dev` profile? A. `dev.yml` B. `application-dev.yml` C. `application.dev` D. `profile-dev.yml`
**Q02 (O1)** Choose a profile without editing files: A. Rename the JAR B. Set `SPRING_PROFILES_ACTIVE` C. Change `pom.xml` D. Restart the IDE only
**Q03 (O2)** Annotation to bind a group of settings to a type: A. `@Value` B. `@ConfigurationProperties` C. `@Profile` D. `@Qualifier`
**Q04 (O2)** Why a record for properties? A. Records are faster B. Immutable, constructor-bound values C. Records need setters D. Required by YAML
**Q05 (O2)** `page-size-max` in YAML binds to the Java name: A. `page_size_max` B. `PageSizeMax` C. `pagesizemax` only D. `pageSizeMax`
**Q06 (O3)** What does `@Validated` on a properties record enable? A. Faster startup B. Constraint checks on the bound values C. Profile switching D. Encryption
**Q07 (O3)** A property fails validation. The app: A. Starts and logs a warning B. Starts with defaults C. Fails to start with a message naming the property D. Crashes later at first request
**Q08 (O4)** Which source wins? A. `application.yml` over env var B. Env var over `application.yml` C. Default in code over command line D. They are merged randomly
**Q09 (O4)** Highest priority among these: A. Command-line argument B. Base `application.yml` C. Profile file D. Default in code
**Q10 (O4)** Where do database passwords belong? A. Committed `application.yml` B. Source code constants C. Environment or secret store D. The README

## Answers
Q01 B · Q02 B · Q03 B · Q04 B · Q05 D · Q06 B · Q07 C · Q08 B · Q09 A · Q10 C

## Practical part
Six exercises `JNR-012-EX01` to `EX06` plus the lab (with the precedence check in step 5). Pass: quiz at least 8/10, lab acceptance met, EX05 predicted correctly.
