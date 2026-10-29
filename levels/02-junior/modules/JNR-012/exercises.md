# JNR-012 · Configuration management — Exercises and lab

## Lab
### JNR-012-LAB1 · Shop settings
**Outcomes:** 1–4 · **Time:** ~2 h
1. Create a `ShopProperties` record: currency, tax rate, page-size limits (default and max).
2. Validate it with `@Validated` and constraints.
3. Add `application.yml` plus `application-dev.yml` and `application-prod.yml` with different values.
4. Inject `ShopProperties` into a service; no `@Value` in the code.
5. Prove precedence: override one value with an environment variable and a command-line argument.
**Acceptance:** invalid config prevents startup with a clear message; profiles switch values; no secrets in committed YAML.

## Exercises (assessment: lab check plus precedence quiz)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-012-EX01 | 1 | Add a `dev` profile that changes the log level and the port; start with it. |
| JNR-012-EX02 | 2 | Convert three `@Value` usages to one `@ConfigurationProperties` record. |
| JNR-012-EX03 | 2 | Map `page-size-max` in YAML to a Java record component; state the name rule. |
| JNR-012-EX04 | 3 | Add `@Min(1)` to the page size and set it to 0; read the failure message. |
| JNR-012-EX05 | 4 | Set the same property in `application.yml`, a profile file, an env var, and a command-line argument; predict, then check the winner. |
| JNR-012-EX06 | 4 | Decide where each lives: database password, tax rate, page-size limit, API token. |

## Solutions
- **EX01** `application-dev.yml` with `server.port: 8081` and `logging.level.com.shop: DEBUG`; start with `--spring.profiles.active=dev`.
- **EX02** `@ConfigurationProperties(prefix="shop") record ShopProperties(...)`; inject it where `@Value` fields were.
- **EX03** `pageSizeMax`; kebab-case or camelCase in the file, relaxed binding matches it.
- **EX04** Startup fails with a binding or validation error naming `shop.page-size-max` and the constraint.
- **EX05** Command line wins, then the environment variable, then the profile file, then the base file.
- **EX06** Password and token: environment or secret store. Tax rate and page size: committed YAML (non-secret) with profile overrides.
