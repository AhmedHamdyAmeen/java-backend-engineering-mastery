# BEG-054 · Build tools — Quiz

Outcomes: O1 why build tools · O2 `pom.xml` · O3 lifecycle · O4 dependencies and conversion.

**Q01 (O1)** A build tool mainly: A. Writes code for you B. Repeats compile, test, and package steps the same way C. Replaces Java D. Draws diagrams
**Q02 (O1)** Manual `javac` does not scale because: A. It cannot compile B. It is deprecated C. Long commands and libraries are hard to repeat D. It needs Maven
**Q03 (O2)** Main Java source folder in Maven: A. `src/java` B. `main/` C. `src/main/java` D. `source`
**Q04 (O2)** Test code lives in: A. `src/test/java` B. `src/main/test` C. `target` D. `tests` at the root
**Q05 (O2)** Which identifies a Maven project? A. Only the folder name B. `groupId`, `artifactId`, `version` C. The IDE D. The JDK path
**Q06 (O3)** `mvn test` also runs: A. `package` B. `deploy` C. Earlier phases such as `compile` D. Nothing else
**Q07 (O3)** `mvn clean` does what? A. Compiles B. Runs tests C. Downloads JUnit D. Deletes `target/`
**Q08 (O4)** Dependencies are downloaded from: A. The JDK B. Maven Central C. Postman D. GitHub issues
**Q09 (O4)** JUnit should have scope: A. `test` B. `compile` C. `runtime` D. `none`
**Q10 (O4)** Should `target/` be committed? A. Yes B. Only on Fridays C. Only the JAR D. No, ignore it

## Answers
Q01 B · Q02 C · Q03 C · Q04 A · Q05 B · Q06 C · Q07 D · Q08 B · Q09 A · Q10 D

## Practical part
Practical check: the data-structures project builds and `mvn test` passes from a clean clone (lab and EX01–EX07). Pass: at least 8 of 10 quiz questions and a build that works on a clean machine.
