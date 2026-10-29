# JNR-011 · Spring Boot — Quiz

Outcomes: O1 starters and auto-configuration · O2 conditions report · O3 overriding · O4 embedded server and JAR.

**Q01 (O1)** A starter is: A. A bundle of dependencies for a job B. A test runner C. A database D. A Java compiler flag
**Q02 (O1)** Auto-configuration decides what to create based on: A. Random choice B. Conditions such as classpath contents and existing beans C. The IDE D. The OS
**Q03 (O1)** `@ConditionalOnMissingBean` means: A. Create the bean only if you have not defined one B. Always create it C. Delete other beans D. Fail startup
**Q04 (O2)** How do you turn on the conditions evaluation report? A. `--debug` B. `--quiet` C. `--clean` D. `-Xmx`
**Q05 (O2)** An auto-configuration appears under "Negative matches". It means: A. It is broken B. Its conditions were not met so it did not apply C. It ran twice D. It was deleted from the JAR
**Q06 (O3)** The preferred first way to change a Boot default: A. Exclude the auto-configuration B. Edit Boot's source C. Set a property D. Rewrite `main`
**Q07 (O3)** You define your own `ObjectMapper` bean. Boot's default: A. Backs off B. Creates a second one C. Fails startup D. Overrides yours
**Q08 (O3)** Blindly excluding auto-configurations is risky because: A. It is slow B. You may remove needed beans without seeing why C. Maven forbids it D. It changes the Java version
**Q09 (O4)** The embedded server is: A. Installed separately B. Part of the application's own process and JAR C. A cloud service D. Optional for web apps
**Q10 (O4)** To run the built executable JAR you need: A. `java -jar app.jar` and a Java runtime B. Maven installed C. An application server D. An IDE

## Answers
Q01 A · Q02 B · Q03 A · Q04 A · Q05 B · Q06 C · Q07 A · Q08 B · Q09 B · Q10 A

## Practical part
Six exercises `JNR-011-EX01` to `EX06` plus the lab. The assessment is EX06: explaining the Shop API startup sequence. Pass: quiz at least 8/10, the lab explanation matches the report, EX06 correct.
