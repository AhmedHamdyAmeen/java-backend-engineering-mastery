# BEG-056 · AI coding assistants for learners — Exercises and lab

## Lab
### BEG-056-LAB1 · Explain, don't copy
**Outcomes:** 1–5 · **Time:** ~1.5 h
Use three bugs from the `BEG-018-LAB1` bug hunt. For each:
1. Write your own hypothesis first.
2. Ask an assistant using goal, code, exact error, and what you tried (no secrets or personal data).
3. Confirm or reject its answer with the debugger or a test.
4. Record one case where the assistant was wrong or incomplete.

**Acceptance:** written log per bug with your hypothesis, the assistant's answer, and the evidence that settled it.

## Exercises (assessment: short quiz plus the lab log)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-056-EX01 | 1 | In five sentences, explain tokens, next-token prediction, and training data to a friend. |
| BEG-056-EX02 | 2 | Given three assistant answers (provided), mark which contain an invented method or wrong claim and show how you checked. |
| BEG-056-EX03 | 3 | Rewrite the weak question "my code doesn't work, help" as a question with goal, code, error, and attempts. |
| BEG-056-EX04 | 4 | After trying yourself, ask an assistant to explain one exception; then explain it back in your own words without looking. |
| BEG-056-EX05 | 5 | Mark each as safe or unsafe to paste: a stack trace, an API key, a customer email, a 10-line method. |

## Solutions
- **EX01** The model is trained on large text and code; text is split into tokens; it predicts the next token repeatedly; so it is fluent but may be wrong.
- **EX02** Verify by compiling, running, and reading the official documentation; invented methods are rejected by the compiler.
- **EX03** For example: "Goal: sum the grades. Code: (method). Error: ArithmeticException at line 8. Tried: printed `count`, it is 0."
- **EX04** Open-ended; a good answer states the cause, the line, and the fix in the learner's own words.
- **EX05** Stack trace: usually safe if it contains no secrets (check first); API key: unsafe; customer email: unsafe (personal data); 10-line method: safe if it contains no secrets and policy allows it.
- Outcomes 1 and 5 are also covered by the quiz; outcome 2 by the lab record of a wrong answer.
