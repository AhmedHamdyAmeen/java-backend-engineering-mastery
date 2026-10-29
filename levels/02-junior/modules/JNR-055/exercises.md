# JNR-055 · AI-assisted development workflow — Exercises and lab

## Lab
### JNR-055-LAB1 · Assisted refactoring
**Outcomes:** 1–5 · **Time:** ~2 h
Use an assistant to help refactor the `CheckoutService` from `JNR-003-LAB1` and to generate missing unit tests. Keep a log of prompts, what you accepted, what you rejected, and why. Draft a one-page team AI-use policy for Shop.
**Acceptance:** tests stay green throughout; every generated test has meaningful assertions; at least two suggestions rejected with reasons; a one-page team AI-use policy drafted for Shop.

## Exercises (assessment: review a provided AI-assisted pull request and find its defects and policy issues, plus six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-055-EX01 | 1 | List three tasks where you would use an assistant and three where you would not. Give a reason for each. |
| JNR-055-EX02 | 2 | Rewrite the prompt "make this better" for a method of your choice, with code, constraints, conventions, and expected result. |
| JNR-055-EX03 | 3 | Generate tests for `Money.add` with an assistant. Mark any test with a weak assertion and fix it. |
| JNR-055-EX04 | 3 | Take one generated test, break the production code on purpose, and report whether the test catches it. |
| JNR-055-EX05 | 4 | Review a given 400-line AI-assisted pull request description. Write five review comments. |
| JNR-055-EX06 | 4 | Write the disclosure line you would put in a pull request that used an assistant. |
| JNR-055-EX07 | 5 | Mark which of these may go into a prompt: a stack trace without secrets, a `.env` file, customer emails, a public method signature. |

## Solutions
- **EX01** Use: boilerplate, explaining code, draft tests. Do not use: security-sensitive logic, secrets handling, code you cannot verify.
- **EX02** Example: "Java 21, Shop Core. Code below. Keep the signature, no behavior change, JUnit 5. Extract the tax block into `calculateTax` and list changes."
- **EX03** Weak: `assertNotNull(result)`. Fix: `assertEquals(new Money(300, "EUR"), a.add(b))`.
- **EX04** Change `+` to `-` in the code; a useful test turns red. A test that stays green is useless; strengthen or remove it.
- **EX05** Examples: PR is too large, ask to split; method name that does not exist in the library; deleted null check; tests assert nothing; no AI disclosure.
- **EX06** "AI assistance: used [tool] to draft tests and one extraction; reviewed and edited by me."
- **EX07** Allowed: stack trace without secrets, public method signature (if policy allows). Not allowed: `.env` file, customer emails.
- Outcome 1 is also covered by quiz Q01–Q02; outcome 5 by the lab policy and quiz Q09–Q10.
