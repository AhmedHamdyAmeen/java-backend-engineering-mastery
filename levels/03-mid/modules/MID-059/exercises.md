# MID-059 · Architectural styles — Exercises and lab

## Lab
### MID-059-LAB1 · Hexagonal Shop
**Outcomes:** 1–3 · **Time:** ~3 h
1. Restructure Shop into modules (`catalog`, `orders`, `inventory`, `payments`), each with `api` and `internal` packages.
2. In `orders`, move the domain to plain Java with outbound ports `OrderRepository` and `PaymentGateway`; implement JPA and payment adapters.
3. Add ArchUnit tests: the domain has no `org.springframework..` or `jakarta.persistence..` imports; modules only use each other's `api`.
4. Add a second payment adapter (fake) and select it by profile.
**Acceptance:** the payment adapter can be swapped without touching the domain; ArchUnit tests pass and fail when a violation is introduced.

## Exercises (assessment: architecture-style comparison for a scenario; five exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-059-EX01 | 1 | Write one paragraph each on what layered, hexagonal, and clean architecture protect and what they cost. |
| MID-059-EX02 | 2 | Given a service that injects `JpaRepository` and `RestTemplate` into business logic, list the dependencies to invert and name the ports. |
| MID-059-EX03 | 2 | Write an ArchUnit rule that forbids `..domain..` from depending on `org.springframework..`. |
| MID-059-EX04 | 3 | Sketch a modular monolith for a booking system with three modules; define each module's public API and what stays internal. |
| MID-059-EX05 | 4 | A 4-person startup with a changing domain and a 40-person bank team with a stable domain: pick a style for each and justify. |

## Solutions
- **EX01** Layered: simplicity, but the domain depends on persistence. Hexagonal: domain isolated behind ports, costs extra mapping. Clean: same protection with an explicit use-case ring, costs more ceremony.
- **EX02** Invert: `OrderRepository` and `PaymentGateway` (outbound ports in the domain); adapters implement them; the service depends only on the ports.
- **EX03** `noClasses().that().resideInAPackage("..domain..").should().dependOnClassesThat().resideInAPackage("org.springframework..")` and `.check(importedClasses)`.
- **EX04** For example `catalog`, `booking`, `payments`; each exposes an `api` interface plus DTOs/events; entities, repositories, and mappers are package-private.
- **EX05** Startup: modular monolith with a light hexagonal core (cheap to change, few people). Bank: hexagonal or clean modular monolith with enforced boundaries; justify by team size, complexity, and change rate. Any justified answer using those three drivers is acceptable.
- Outcome 3 is also checked by the lab (ArchUnit and module APIs).
