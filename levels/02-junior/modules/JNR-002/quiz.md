# JNR-002 · Maven in depth — Quiz

Outcomes: O1 scopes · O2 dependency tree and conflicts · O3 BOMs · O4 plugins and multi-module · O5 reproducible builds.

**Q01 (O1)** Which scope for JUnit? A. `compile` B. `runtime` C. `provided` D. `test`
**Q02 (O1)** Which scope for a database driver used only at run time? A. `runtime` B. `test` C. `provided` D. `system`
**Q03 (O2)** Which command prints the dependency tree? A. `mvn clean` B. `mvn package` C. `mvn dependency:tree` D. `mvn site`
**Q04 (O2)** A transitive dependency is one that: A. You wrote B. Your dependency needs C. Is only for tests D. Is deleted
**Q05 (O2)** In a version conflict, Maven by default picks: A. The newest B. The oldest C. A random one D. The nearest in the tree
**Q06 (O3)** What is a BOM? A. A build log B. A Java compiler C. A POM listing matching versions D. A test report
**Q07 (O3)** Why does Spring Boot use a BOM? A. To make tests faster B. To keep library versions compatible C. To hide code D. To remove tests
**Q08 (O4)** Which plugin runs integration tests (`*IT`)? A. Surefire B. Compiler C. Jar D. Failsafe
**Q09 (O4)** A parent POM uses packaging: A. `pom` B. `jar` C. `war` D. `zip`
**Q10 (O5)** The Maven Wrapper ensures: A. Faster tests B. Smaller jars C. Everyone uses the same Maven version D. No dependencies

## Answers
Q01 D · Q02 A · Q03 C · Q04 B · Q05 D · Q06 C · Q07 B · Q08 D · Q09 A · Q10 C

## Practical part
Seven exercises `JNR-002-EX01` to `EX07` plus the lab; for the assessment, fix a broken multi-module build and explain the cause. Pass: at least 8 of 10 quiz answers, six exercises correct, and `./mvnw verify` green on a clean clone.
