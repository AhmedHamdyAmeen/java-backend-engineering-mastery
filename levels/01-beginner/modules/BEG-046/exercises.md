# BEG-046 · Version control — Exercises and lab

## Lab
### BEG-046-LAB1 · Version your work
**Outcomes:** 1–4 · **Time:** ~3 h
Put the Bank Accounts project under Git with meaningful commits (at least five). Create a feature branch, make conflicting changes on both branches, merge, and resolve the conflict by hand. Add a `.gitignore`.
**Acceptance:** clean history (clear messages, no `target/` or `.idea/`); conflict resolved correctly.

## Exercises (assessment: terminal-only Git task)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-046-EX01 | 1 | In a new folder, initialize a repo, create `Hello.java`, stage and commit it with a clear message. |
| BEG-046-EX02 | 1 | Rewrite these bad messages as good ones: "fix", "stuff", "changes". Use a bug-fix example of your own. |
| BEG-046-EX03 | 2 | Change a file, then show the difference unstaged and staged. Which two commands did you use? |
| BEG-046-EX04 | 2 | List the last five commits in one-line form. |
| BEG-046-EX05 | 3 | Create branch `greeting`, commit a change, switch back, and merge with no conflict. |
| BEG-046-EX06 | 3 | Make both branches edit the same line, merge, and resolve the conflict. |
| BEG-046-EX07 | 4 | Write a `.gitignore` for a Java project; prove `target/` stays untracked. |

## Solutions
- **EX01** `git init`, `git add Hello.java`, `git commit -m "Add Hello program"`.
- **EX02** e.g. "Fix negative balance after withdraw", "Add Account class with deposit", "Rename amount to balance".
- **EX03** `git diff` (unstaged) and `git diff --staged`.
- **EX04** `git log --oneline -5`.
- **EX05** `git switch -c greeting`, commit, `git switch main`, `git merge greeting` (fast-forward).
- **EX06** After `git merge`, open the file, keep the intended text, delete the markers, `git add file`, `git commit`.
- **EX07** `target/`, `*.class`, `.idea/`, `.env`; `git status` does not list them.
