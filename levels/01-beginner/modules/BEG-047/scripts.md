# BEG-047 · GitHub — Lecture scripts

**Video:** 48 min · **Analogy used throughout:** a shared online bookshelf where you keep a copy of your album and others can suggest edits.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-047-L01 · Remotes, push, and pull (10 min)
**Goal:** connect a local repo to GitHub and sync it.

**Key points**
- A remote is a copy of your repo on another server; GitHub hosts remotes.
- By convention the main remote is named `origin`.
- `git push` sends your commits to the remote.
- `git pull` brings new commits from the remote to you.
- `git clone <url>` copies an existing remote repo to your computer.

**Show**
```bash
git remote add origin https://github.com/you/bank-accounts.git
git push -u origin main
git pull
```

**Check:** Which command sends your commits to GitHub? *(`git push`.)*

---

## BEG-047-L02 · Authentication with GitHub (SSH keys or tokens) (8 min)
**Goal:** prove who you are to GitHub safely.

**Key points**
- GitHub does not accept your account password for Git over HTTPS.
- Option 1: a personal access token used in place of a password (verify current steps before recording).
- Option 2: an SSH key pair; the public key goes to GitHub, the private key never leaves your machine.
- Never commit a token or a private key.

**Show**
```bash
ssh-keygen -t ed25519 -C "you@example.com"
# add the .pub file in GitHub settings, then:
ssh -T git@github.com
```

**Check:** Which half of an SSH key do you upload to GitHub? *(The public key.)*

---

## BEG-047-L03 · Pull requests and reviews (12 min)
**Goal:** propose a change and get it reviewed before it reaches `main`.

**Key points**
- A pull request (PR) asks to merge one branch into another.
- Push a branch, then open a PR on GitHub with a clear title and description.
- Reviewers comment on lines; you answer and push more commits to the same branch.
- When approved, merge the PR.
- Do not push directly to `main`; PRs are how teams stay safe.

**Show:** a PR page with a diff, one review comment, and a "Merge pull request" button.

**Check:** Where do extra commits go after a review comment? *(Onto the same branch; the PR updates.)*

---

## BEG-047-L04 · Markdown and a good README (10 min)
**Goal:** write a README that lets a stranger run your project.

**Key points**
- Markdown is plain text with simple marks: `#` heading, `-` list, backticks for code.
- A README says what the project is, how to set it up, and how to use it.
- Setup steps must be exact: Java version, build command, run command.
- A short example of output helps.

**Show**
```markdown
# Bank Accounts
Console app for deposits and withdrawals.

## Setup
Requires Java 21. Run `javac Main.java`.

## Usage
`java Main`
```

**Check:** Which section lets others run the project? *(Setup.)*

---

## BEG-047-L05 · Demo: publishing a project and reviewing a pull request (8 min)
**Goal:** publish a repo and run one PR round. Prepares BEG-047-LAB1.

**Steps**
1. Create an empty repo on GitHub; add it as `origin`; push `main`.
2. Add a `README.md` with setup and usage.
3. Create branch `readme-typo`, change one line, push it, and open a PR.
4. A peer leaves a comment; push a fix to the same branch.
5. **Planned mistake:** commit a change straight to `main` by accident. Fix: show `git revert` or move it to a branch and explain why PRs prevent this.
6. Merge the PR.
