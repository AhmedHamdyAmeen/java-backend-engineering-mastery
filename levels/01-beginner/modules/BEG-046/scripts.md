# BEG-046 · Version control — Lecture scripts

**Video:** 71 min · **Analogy used throughout:** a photo album of your project where every page is a snapshot you can flip back to.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-046-L01 · Why version control (7 min)
**Goal:** explain why every project needs history.

**Key points**
- Without history you end up with `final`, `final2`, `final_REAL` copies.
- Version control records every change: who, when, and why.
- You can go back to any earlier snapshot if something breaks.
- Teams can work on the same code without overwriting each other.
- Git is the most used version control tool; it keeps the full history on your own computer.

**Show:** a folder of messy copies next to a clean list of Git snapshots.

**Check:** Name one thing version control gives you that copying folders does not. *(Any: who/why of each change, safe merging with teammates, easy return to old versions.)*

---

## BEG-046-L02 · Repositories, staging, and commits (12 min)
**Goal:** make your first commit.

**Key points**
- A repository (repo) is a project folder that Git tracks.
- `git init` turns a folder into a repo.
- Staging (`git add`) chooses which changes go into the next snapshot.
- A commit (`git commit`) saves the staged changes with a message.
- Good message: short, says what and why. "fix" says nothing.

**Show**
```bash
git init
git add Main.java
git commit -m "Add Main class that prints a greeting"
```

**Check:** What is the order: add or commit first? *(`add` first, then `commit`.)*

---

## BEG-046-L03 · History and diffs (8 min)
**Goal:** look at what changed and when.

**Key points**
- `git status` shows what is changed, staged, or untracked.
- `git log --oneline` lists commits, newest first.
- `git diff` shows changes not yet staged; `git diff --staged` shows staged ones.
- Read `status` before every commit; it prevents surprises.

**Show**
```bash
git status
git diff
git log --oneline
```

**Check:** Which command shows the list of past commits? *(`git log`.)*

---

## BEG-046-L04 · Branches (10 min)
**Goal:** work on a feature without touching the main line.

**Key points**
- A branch is a separate line of commits, like a parallel copy of the album.
- `main` is the default branch; keep it working.
- `git switch -c feature-x` creates and moves to a new branch.
- `git switch main` goes back.
- Small branches with one purpose are easy to review.

**Show**
```bash
git switch -c add-interest
# edit, add, commit
git switch main
git branch
```

**Check:** Which command creates and switches to a new branch? *(`git switch -c name`.)*

---

## BEG-046-L05 · Merging and conflicts (12 min)
**Goal:** combine branches and fix a conflict by hand.

**Key points**
- `git merge branch` brings that branch's commits into the current branch.
- If two branches changed the same lines, Git cannot choose: a merge conflict.
- Git marks the file with `<<<<<<<`, `=======`, `>>>>>>>`.
- You edit the file to the correct final text, remove the markers, then `git add` and `git commit`.
- A conflict is normal, not a failure.

**Show**
```text
<<<<<<< HEAD
double rate = 0.02;
=======
double rate = 0.03;
>>>>>>> add-interest
```

**Check:** What must you remove from the file before committing? *(The three marker lines.)*

---

## BEG-046-L06 · `.gitignore` (6 min)
**Goal:** keep generated files and secrets out of Git.

**Key points**
- `.gitignore` lists patterns Git must not track.
- Ignore build output (`target/`, `*.class`), IDE folders (`.idea/`), and secret files (`.env`).
- A file already committed stays tracked; ignoring it later is not enough.
- A password committed once is in history; treat it as leaked and change it.

**Show**
```text
target/
*.class
.idea/
.env
```

**Check:** Should `target/` be committed? *(No; it is rebuilt from source.)*

---

## BEG-046-L07 · Demo: putting Bank Accounts under Git (8 min)
**Goal:** version an existing project with clean commits. Prepares BEG-046-LAB1.

**Steps**
1. Open a terminal in the Bank Accounts folder; run `git init`.
2. Create `.gitignore` with `*.class` and `.idea/`.
3. **Planned mistake:** run `git add .` first without a `.gitignore`; `git status` shows `.class` files staged. Fix: `git restore --staged .`, create `.gitignore`, add again.
4. Commit in small steps: "Add Account class", then "Add deposit and withdraw".
5. Show `git log --oneline`.

---

## BEG-046-L08 · Demo: creating and resolving a merge conflict (8 min)
**Goal:** cause a conflict on purpose and resolve it. Prepares BEG-046-LAB1.

**Steps**
1. Create branch `feature`; change one line in `Account.java`; commit.
2. Switch to `main`; change the same line differently; commit.
3. Run `git merge feature`; Git reports a conflict.
4. **Planned mistake:** commit with the markers still in the file; the build breaks. Fix: reopen the file, keep the right text, remove markers, commit again.
5. Run `git log --oneline --graph` to see the merge.
