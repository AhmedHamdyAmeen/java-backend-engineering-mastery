# BEG-054 · Build tools — Exercises and lab

## Lab
### BEG-054-LAB1 · Mavenize
**Outcomes:** 1–4 · **Time:** ~2.5 h
Convert the data-structures project to Maven with JUnit as a test dependency; `mvn test` passes from the terminal.
**Acceptance:** builds on a clean machine.

## Exercises (assessment: practical check)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-054-EX01 | 1 | List three problems with compiling a ten-library project by hand with `javac`. |
| BEG-054-EX02 | 2 | Label `groupId`, `artifactId`, `version`, a dependency, and a plugin in a given `pom.xml`. |
| BEG-054-EX03 | 2 | Place five given files into the correct Maven folders. |
| BEG-054-EX04 | 3 | Run `mvn compile`, `mvn test`, and `mvn package`; say what each produced. |
| BEG-054-EX05 | 3 | Explain why `mvn package` also runs the tests. |
| BEG-054-EX06 | 4 | Add a library from Maven Central and use one class from it. |
| BEG-054-EX07 | 4 | Make sure `target/` is not committed in the converted project. |

## Solutions
- **EX01** Long class paths, manual downloads of JARs, no repeatable steps (and no test running).
- **EX02** Coordinates sit at the top; dependencies under `<dependencies>`; plugins under `<build><plugins>`.
- **EX03** Main classes in `src/main/java`; tests in `src/test/java`; `pom.xml` at the root.
- **EX04** `compile` makes classes in `target/classes`; `test` runs tests; `package` creates a JAR in `target/`.
- **EX05** Lifecycle phases run in order; `test` comes before `package`.
- **EX06** Add the `<dependency>` block, then import its class; Maven downloads it on the next build.
- **EX07** `.gitignore` contains `target/`; `git status` does not show it.
