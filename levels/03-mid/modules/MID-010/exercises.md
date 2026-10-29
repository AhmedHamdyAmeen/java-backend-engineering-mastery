# MID-010 · Java module system — Exercises and lab

## Lab
### MID-010-LAB1 · Boundaries
**Outcomes:** 1–3 · **Time:** ~1.5 h
Modularize Shop Core with JPMS (descriptor, exported API package, opened model package if needed). Enforce Shop API's feature boundaries with ArchUnit tests. Introduce a forbidden dependency and show the build failing.
**Acceptance:** a forbidden dependency fails the build.

## Exercises (assessment: quiz plus lab)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-010-EX01 | 1 | Write a `module-info.java` for `com.shop.core` that requires `java.sql` and exports one package. |
| MID-010-EX02 | 1 | Add `opens ... to` for a model package used by Jackson; explain the error without it. |
| MID-010-EX03 | 2 | Explain classpath vs module path and strong encapsulation in four sentences, with an example of what encapsulation blocks. |
| MID-010-EX04 | 2 | Compile a class that uses an unexported package from another module; read the error. |
| MID-010-EX05 | 3 | For Shop API (Spring Boot), argue for or against JPMS and name one alternative. |
| MID-010-EX06 | 3 | Write an ArchUnit rule: services must not depend on controllers. |

## Solutions
- **EX01** `module com.shop.core { requires java.sql; exports com.shop.core.api; }`
- **EX02** Without `opens`, reflection throws `InaccessibleObjectException` for private-member access; add `opens com.shop.core.model to com.fasterxml.jackson.databind;`.
- **EX03** Classpath: flat, everything public is visible. Module path: only exported packages of required modules are visible. Encapsulation blocks access to internals even if `public` (and deep reflection unless opened).
- **EX04** The compiler reports the package is not visible or not exported.
- **EX05** Typical answer: against for the Boot service (reflection-heavy, library gaps, high cost); use ArchUnit or build modules for boundaries. A reasoned answer for a library is acceptable.
- **EX06** `noClasses().that().resideInAPackage("..service..").should().dependOnClassesThat().resideInAPackage("..controller..")` with `@AnalyzeClasses` (verify against the ArchUnit version).
