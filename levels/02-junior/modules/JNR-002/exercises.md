# JNR-002 · Maven in depth — Exercises and lab

## Lab
### JNR-002-LAB1 · Shop multi-module
**Outcomes:** 1–5 · **Time:** ~2 h
Split the project into `shop-core` and `shop-cli` with a parent POM, central dependency management, and the Maven Wrapper. A version conflict is planted in the starter; diagnose it with `dependency:tree` and fix it.
**Acceptance:** `./mvnw verify` passes on a clean clone; no version is hard-coded in a child module; the README explains the conflict cause.

## Exercises (assessment: fix a broken multi-module build and explain the cause, plus six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-002-EX01 | 1 | Pick a scope for each: JUnit, Postgres JDBC driver, Servlet API (server provides it), Guava used in your code. |
| JNR-002-EX02 | 2 | Run `dependency:tree` on a project and name one transitive dependency and the dependency that brought it. |
| JNR-002-EX03 | 2 | Two libraries need `commons-lang3` 3.9 and 3.14. Which does Maven choose by default? Show two ways to control it. |
| JNR-002-EX04 | 3 | Import a BOM and add one dependency without a version. Explain why this is safer. |
| JNR-002-EX05 | 4 | Configure the compiler plugin for the Java release, and say which plugin runs `*Test` and which runs `*IT`. |
| JNR-002-EX06 | 4 | Create a parent POM with two modules, where one depends on the other. Show the build order. |
| JNR-002-EX07 | 5 | Add the wrapper, remove Maven from your PATH, and run the build. List three things that make a build reproducible. |

## Solutions
- **EX01** JUnit `test`; JDBC driver `runtime`; Servlet API `provided`; Guava `compile`.
- **EX02** Example: `failureaccess` brought by `guava`. Read it from the tree indentation.
- **EX03** The nearest declaration wins; if equal distance, the first declared. Control with `dependencyManagement` (pin) or a direct dependency or exclusion.
- **EX04** `<scope>import</scope><type>pom</type>` in `dependencyManagement`; the version comes from the BOM, so libraries match.
- **EX05** `<release>` in `maven-compiler-plugin`; Surefire runs `*Test`; Failsafe runs `*IT`.
- **EX06** The parent lists `<modules>`; the dependency module builds first (Maven sorts by dependencies).
- **EX07** `mvn wrapper:wrapper`, then `./mvnw verify`. Reproducible: fixed versions (no ranges), wrapper-pinned Maven, same Java release.
- All outcomes are also covered by the lab; outcome 5 is covered by quiz Q10.
