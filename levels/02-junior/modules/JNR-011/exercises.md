# JNR-011 · Spring Boot — Exercises and lab

## Lab
### JNR-011-LAB1 · Under the hood
**Outcomes:** 1–4 · **Time:** ~2 h
1. Run the Shop API with `--debug` and save the conditions evaluation report.
2. Pick three auto-configurations that applied (positive matches) and one that did not (negative match); for each, write the condition that decided it.
3. Override the default JSON date format (property first, then customizer).
4. Build the executable JAR and run it with `java -jar`.
**Acceptance:** written explanation matches the report; date format changed; JAR runs.

## Exercises (assessment: explain the startup sequence of the Shop API)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-011-EX01 | 1 | Explain in three sentences what a starter and an auto-configuration are and how they differ. |
| JNR-011-EX02 | 1 | Name the three conditions `@ConditionalOnClass`, `@ConditionalOnMissingBean`, `@ConditionalOnProperty` and give one example of each. |
| JNR-011-EX03 | 2 | In the report, find why a `DataSource` was not created in a project without a database starter. |
| JNR-011-EX04 | 3 | Define your own `Clock` or `ObjectMapper` bean and confirm in the report that Boot's default backed off. |
| JNR-011-EX05 | 4 | Build the JAR, list its contents with `jar tf`, and find the embedded server library. |
| JNR-011-EX06 | 4 | Write the startup sequence of the Shop API: `main`, `SpringApplication.run`, context creation, scanning, auto-configuration, server start, "Started". |

## Solutions
- **EX01** A starter is a dependency bundle; auto-configuration is the code, triggered by what is on the classpath, that creates beans. Starter supplies the libraries; auto-configuration wires them.
- **EX02** Class present (Tomcat classes); missing bean (no user-defined `ObjectMapper`); property (`spring.main.banner-mode`, or a feature flag).
- **EX03** Negative match: required classes, or a bean of the needed type, are absent.
- **EX04** The report lists the default bean under negative matches with `@ConditionalOnMissingBean` found a bean.
- **EX05** `jar tf target/*.jar` shows `BOOT-INF/lib/tomcat-embed-core-*.jar`.
- **EX06** `main` calls `run`; Boot prepares the environment and creates the context; scanning finds your beans; auto-configuration adds the defaults; the embedded server starts; the app logs "Started".
