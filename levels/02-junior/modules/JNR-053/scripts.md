# JNR-053 · Team workflows — Lecture scripts

**Video:** 50 min · **Analogy used throughout:** a relay race: small, clean handoffs keep the team fast.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## JNR-053-L01 · Branching strategies (8 min)
**Goal:** pick a branching approach that keeps merging easy.

**Key points**
- Trunk-based development: everyone merges small changes to `main` at least daily; unfinished features hide behind a feature flag.
- Short-lived feature branches: branch from `main`, merge within a day or two via a pull request.
- Long-lived branches cause painful merges; avoid them.
- Name branches clearly: `feature/cart-discount`, `fix/order-total`.
- Keep `main` always releasable; CI protects it.

**Show:** a drawing: `main` with short branches merging back within a day, versus a branch alive for three weeks.

**Check:** Why avoid long-lived branches? *(They drift from `main` and cause large, risky merges.)*

---

## JNR-053-L02 · Good pull requests (8 min)
**Goal:** write PRs that a reviewer can act on quickly.

**Key points**
- Keep it small: one purpose, ideally under a few hundred changed lines.
- Title says what; description says why, how to test, and what to look at.
- Link the issue; add screenshots or API examples when useful.
- Self-review before asking others; remove debug code.
- Make sure CI is green before requesting review.

**Show:** a PR template: Summary, Why, How tested, Risks, Linked issue.

**Check:** What should a PR description explain besides what changed? *(Why, and how it was tested.)*

---

## JNR-053-L03 · Code review as reviewer and author (12 min)
**Goal:** give and receive feedback well.

**Key points**
- Reviewers check correctness, tests, clarity, and risks first; style comes last (tools can check style).
- Comment on the code, not the person; ask questions: "What happens if the cart is empty?"
- Mark comments as blocking or optional (nit).
- Authors: assume good intent, respond to every comment, and explain or change.
- Approve when it is good enough, not perfect; follow up later for minor ideas.

**Show:** two comments: "This is wrong" versus "This will fail for an empty list; could we add a test for it?"

**Check:** Which comments should a reviewer raise first, correctness or formatting? *(Correctness.)*

---

## JNR-053-L04 · Issues, boards, and agile basics (12 min)
**Goal:** break work down and join the team rhythm.

**Key points**
- An issue describes one piece of work with acceptance criteria ("done when ...").
- Split large features into issues that fit in one to three days.
- Estimate roughly (small, medium, large, or points) and accept that estimates are guesses.
- Boards show work as To do, In progress, In review, Done.
- Scrum events: planning, daily stand-up, review (demo), retrospective (what to improve). Kanban focuses on limiting work in progress.

**Show:** a board with four columns and an issue with acceptance criteria.

**Check:** What is a retrospective for? *(Learning what to improve in how the team works.)*

---

## JNR-053-L05 · Demo: a pull request from issue to merge (10 min)
**Goal:** follow one change through the whole flow. Prepares `JNR-053-LAB1`.

**Steps**
1. Pick an issue with acceptance criteria and move it to In progress.
2. Create a branch, make a small change with a test, and commit with clear messages.
3. Open a PR using the template, link the issue, and wait for CI.
4. A reviewer leaves one blocking and one optional comment; the author replies and updates.
5. **Planned mistake:** the PR includes an unrelated refactor, making it too big; split it into two PRs.
6. Merge, delete the branch, and watch the issue close.
