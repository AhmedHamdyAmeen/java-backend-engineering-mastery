# BEG-047 · GitHub — Exercises and lab

## Lab
### BEG-047-LAB1 · Public portfolio start
**Outcomes:** 1–3 · **Time:** ~2 h
Publish two projects to GitHub, each with a README. Open a PR for a small change and have a peer review it.
**Acceptance:** repos public; PR has at least one review round.

## Exercises (assessment: portfolio check)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-047-EX01 | 1 | Create a GitHub repo, connect it to a local repo as `origin`, and push `main`. |
| BEG-047-EX02 | 1 | Clone your repo into a second folder, commit there, push, then pull in the first folder. |
| BEG-047-EX03 | 1 | Set up SSH or a token and show that `git push` works without asking for the account password. |
| BEG-047-EX04 | 2 | Make a change on a branch and open a PR with a title and a description. |
| BEG-047-EX05 | 2 | Review a classmate's PR: leave one line comment and approve; answer a comment on your own PR and merge. |
| BEG-047-EX06 | 3 | Write a README with description, setup, and usage sections for one project. |
| BEG-047-EX07 | 3 | Ask a peer to follow only your README to run the project; note where they got stuck and fix it. |

## Solutions
- **EX01** `git remote add origin <url>`, `git push -u origin main`.
- **EX02** `git clone <url> copy`, commit and `git push` in `copy`, then `git pull` in the original.
- **EX03** For SSH: `ssh-keygen`, upload the `.pub` file, `git remote set-url origin git@github.com:you/repo.git`.
- **EX04** `git switch -c small-change`, commit, `git push -u origin small-change`, then "Compare & pull request".
- **EX05** Use the Files changed tab for line comments; push the fix to the same branch; use Merge pull request.
- **EX06** Headings `# Title`, `## Setup`, `## Usage` with exact commands and the Java version.
- **EX07** Typical gaps: missing Java version, missing build command, wrong folder; add them to the README.
