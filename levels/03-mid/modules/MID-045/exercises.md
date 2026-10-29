# MID-045 · Advanced testing — Exercises and lab

## Lab
### MID-045-LAB1 · Contracts for Shop
**Outcomes:** 1–4 · **Time:** ~3 h
Write contracts between `orders` and `inventory` (HTTP) and for `OrderPlaced` (Kafka), verified in both pipelines. Add jqwik property tests for the Order aggregate.
**Acceptance:** renaming a field fails the provider build.

## Exercises (assessment: lab plus a test-strategy question)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-045-EX01 | 1 | List the problems of an end-to-end test that places an order across four services; propose which checks move lower. |
| MID-045-EX02 | 2 | Write a consumer test in `orders` producing a Pact (or Spring Cloud Contract) for `GET /stock/{sku}`. |
| MID-045-EX03 | 2 | Rewrite a contract that asserts a whole response body so it matches only the fields used. |
| MID-045-EX04 | 2 | Write a message contract for `OrderPlaced` and verify it in the producer. |
| MID-045-EX05 | 3 | Add contract verification to the provider pipeline so a failure blocks the build. |
| MID-045-EX06 | 4 | Write two jqwik properties for the Order aggregate (total equals sum of lines; total never negative). |
| MID-045-EX07 | 1–3 | Test-strategy question: for a new `payments` service called by `orders`, state which tests you write at each level and why. |

## Solutions
- **EX01** Slow, brittle, hard to diagnose; move validation to unit tests, interactions to contract tests, DB behavior to Testcontainers; keep one smoke test.
- **EX02** Define the interaction (request, response with `sku` string and `available` integer) in the consumer test; the generated file is published.
- **EX03** Replace exact body matching with type matchers on `sku` and `available` only.
- **EX04** Message contract with `orderId` and `totalCents`; the provider test builds the real event and checks it against the contract.
- **EX05** Pipeline step runs provider verification against published contracts; non-zero exit fails the job.
- **EX06** `@Property` with a generator of valid orders; assertions as in the lecture; second property: `total() >= 0`.
- **EX07** Unit tests for payment rules, consumer contract with `payments`, Testcontainers for persistence, a smoke test; end-to-end only for the happy path.

**Outcome 3** is also checked by lab criterion "renaming a field fails the provider build".
