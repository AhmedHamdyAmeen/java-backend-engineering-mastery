# JNR-008 · Spring ecosystem — Exercises and lab

## Lab
### JNR-008-LAB1 · Shop API skeleton
**Outcomes:** 1–3 · **Time:** ~1 h
1. Generate a Maven project with Spring Initializr: Java, current Boot, dependencies Web, Validation, Actuator.
2. Open it in the IDE and list its parts (pom, wrapper, main class, resources, tests).
3. Run it with `./mvnw spring-boot:run`.
4. Call `/actuator/health` with a browser or `curl`.
5. Commit to a new `shop-api` repository with a short README.
**Acceptance:** runs from the terminal with `./mvnw spring-boot:run`; `/actuator/health` returns `UP`; only the three starters are present.

## Exercises (assessment: quiz)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-008-EX01 | 1 | In one sentence each, state what Spring Framework, Boot, Data, and Security add. |
| JNR-008-EX02 | 2 | Take three classes that depend on each other and write the `new` wiring in `main`. List two problems that appear as classes grow. |
| JNR-008-EX03 | 3 | Generate a project; label each generated file or folder with its purpose. |
| JNR-008-EX04 | 3 | Add the Web starter, then run `./mvnw dependency:tree` and name three libraries it brought (for example Tomcat, Jackson, Spring MVC). |
| JNR-008-EX05 | 1 | Place these in the right project: password hashing, `@SpringBootApplication`, `JpaRepository`, dependency injection. |
| JNR-008-EX06 | 2 | Find in the Boot docs how to change the server port; write the property. |

## Solutions
- **EX01** Framework: container, DI, MVC. Boot: starters, auto-configuration, runnable app. Data: repositories over databases. Security: authentication, authorization, attack protection.
- **EX02** Problems: every change to a constructor forces edits in the wiring; swapping an implementation or creating test versions means editing the code; shared instances must be managed by hand.
- **EX03** `pom.xml` build and dependencies; `mvnw` wrapper; `src/main/java` code with the `@SpringBootApplication` class; `src/main/resources` settings; `src/test` tests.
- **EX04** Examples: embedded Tomcat, Jackson, spring-webmvc, spring-boot-starter-logging.
- **EX05** Security: password hashing; Boot: `@SpringBootApplication`; Data: `JpaRepository`; Framework: dependency injection.
- **EX06** `server.port=9090` (or `server.port: 9090` in YAML).
