# BEG-019 · OOP introduction — Exercises and lab

## Lab
### BEG-019-LAB1 · Noun and verb hunt
**Outcomes:** 1, 2, 3 · **Time:** ~1 h
From a one-page description of a bank (provided by the instructor), list candidate classes (nouns), their state, and their behaviors (verbs). Justify each choice and say which nouns you rejected and why.
**Acceptance:** reasonable candidates with justification.

## Exercises (assessment: quiz plus the noun/verb analysis)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-019-EX01 | 1 | Write two or three sentences on what goes wrong when you store 500 accounts in parallel arrays. |
| BEG-019-EX02 | 1 | Sketch (in words) how the same deposit looks procedurally and object-oriented. |
| BEG-019-EX03 | 2 | For a library book, list three pieces of state and three behaviors. |
| BEG-019-EX04 | 2 | Underline nouns and verbs: "A student enrolls in a course. The teacher grades the exam." |
| BEG-019-EX05 | 3 | Explain class vs object using a cookie cutter and cookies (or your own analogy). |
| BEG-019-EX06 | 3 | Say whether each is a class or an object: `Account`, Ana's account, `Customer`, the customer named Omar. |

## Solutions
- **EX01** Related values are split across arrays, easy to get out of sync, and any code can change any value with no protection; adding a field means editing everything.
- **EX02** Procedural: `deposit(balances, 3, 50)`. OO: `account.deposit(50)`; the account owns its balance.
- **EX03** For example state: title, author, isBorrowed. Behavior: borrow, return, describe.
- **EX04** Nouns: student, course, teacher, exam. Verbs: enrolls, grades.
- **EX05** The cutter is the class (shape defined once); each cookie is an object with its own state (e.g., icing).
- **EX06** Class, object, class, object.
- Outcome 2 is also covered by the lab; all outcomes also appear in the quiz.
