# JNR-007 · Configuration — Exercises and lab

## Lab
### JNR-007-LAB1 · Configurable CLI
**Outcomes:** 1–4 · **Time:** ~1.5 h
Read currency, tax rate, and an API key from a file in the Shop CLI. Allow each to be overridden by an environment variable. Commit a `.env.example` instead of real values and add `.env` to `.gitignore`.
**Acceptance:** the same JAR behaves differently per environment; no secrets in Git; missing required values give a clear error; the README states the precedence order.

## Exercises (assessment: quiz on precedence plus lab check; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-007-EX01 | 1 | Move three hard-coded values (currency, tax rate, shipping fee) into `application.properties` and load them. |
| JNR-007-EX02 | 1 | Write the same settings in YAML, and mark the indentation rule. |
| JNR-007-EX03 | 1 | Override one value with an environment variable and another with `-D`. Show both commands. |
| JNR-007-EX04 | 2 | Identify the twelve-factor violation: `if (System.getenv("ENV").equals("prod")) fee = 5;`. Fix it. |
| JNR-007-EX05 | 3 | Given file=0.19, profile file=0.16, env var=0.07, command line absent, which value wins? Write the order. |
| JNR-007-EX06 | 4 | A teammate committed `.env` with an API key. List the steps to fix it. |

## Solutions
- **EX01** `Properties p = new Properties(); p.load(in);` and `p.getProperty("shop.currency")`.
- **EX02** `shop:` then two-space indented keys; no tabs.
- **EX03** `SHOP_TAX_RATE=0.07 java -jar shop-cli.jar` and `java -Dshop.currency=USD -jar shop-cli.jar`.
- **EX04** Environment-specific code. Move the fee into configuration (`shop.shipping-fee`) and set it per environment.
- **EX05** `0.07` (environment variable). Order: file < profile file < environment variable < command line.
- **EX06** Revoke and replace the key; `git rm --cached .env`; add `.env` to `.gitignore`; commit `.env.example`; clean history if the policy needs it.
- Outcome 3 is also covered by quiz Q06–Q07; outcome 2 by EX04 and quiz Q02.
