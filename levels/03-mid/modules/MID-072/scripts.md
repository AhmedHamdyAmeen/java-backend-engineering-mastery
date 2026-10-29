# MID-072 · AI-assisted engineering at codebase scale — Lecture scripts

**Video:** 60 min · **Analogy used throughout:** a fast but overconfident junior colleague: give a clear brief and the right files, check every claim, and keep the safety net on.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-072-L01 · AI assistants on large codebases (8 min)
**Goal:** give an assistant the right context, not the whole repository.

**Key points**
- Context is limited; relevant beats large. Include the files involved, the test, the convention doc, and the failing output.
- State the goal, constraints, and what must not change.
- Point to existing patterns: "follow `PaymentService`'s error handling".
- Keep a short project conventions file the assistant reads (tool-specific; verify the current mechanism before recording).
- Never paste secrets, tokens, or customer data into prompts; use synthetic data.

**Show:** a prompt with goal, three files, the failing test output, and "do not change public method signatures".

**Check:** Name two things never to include in a prompt. *(Secrets and customer data.)*

---

## MID-072-L02 · AI-assisted debugging with evidence (10 min)
**Goal:** use AI to form hypotheses, then prove them.

**Key points**
- Give the stack trace, relevant log lines (trace id), and what changed recently.
- Ask for several ranked hypotheses and how to test each; not for a patch.
- Confirm with evidence: reproduce, add a log or metric, check the profile.
- Only change code once a hypothesis is confirmed.
- Write a regression test that fails before the fix.

**Show:** a hypothesis table: cause, evidence for, test, result.

**Check:** What do you do before applying an AI-suggested fix? *(Confirm the cause with evidence and reproduce the bug.)*

---

## MID-072-L03 · Refactoring with AI under a safety net (10 min)
**Goal:** refactor in small, verified steps.

**Key points**
- Start green: tests and contract tests pass before you begin.
- Ask for one small step at a time; run tests after each; commit each step.
- Reject any change that alters behavior or public contracts, even if it looks cleaner.
- Characterization tests protect untested code before you touch it.
- Keep diffs small enough to review; split large ones.

**Show:** a sequence of commits: extract method, rename, move class, each with green tests.

**Check:** What do you do when tests fail after an AI step? *(Revert or fix that small step; do not continue on red.)*

---

## MID-072-L04 · Generating tests worth keeping (10 min)
**Goal:** keep valuable tests and discard the rest.

**Key points**
- Ask for edge cases, error paths, boundaries, and a regression test for a known bug.
- Tests that mirror the implementation line by line add no protection.
- A generated test that asserts a current bug cements it; check the expected value against the requirement.
- Use mutation testing (verify the tool and version, such as PIT, before recording) to see if new tests catch changes.
- Delete flaky or redundant tests.

**Show:** a mutation report where generated tests kill 40% of mutants and a better edge-case test adds more.

**Check:** What does a surviving mutant tell you? *(No test noticed that changed behavior.)*

---

## MID-072-L05 · Review discipline and measuring quality (9 min)
**Goal:** review AI output rigorously and measure real effects.

**Key points**
- The author is responsible for every line they submit, whoever or whatever wrote it.
- Mark AI-originated changes in the description; keep a prompt log for traceability.
- Check for hallucinated APIs, missing error handling, security issues, and license concerns.
- Measure review time, defect rate, change failure rate, and test quality; not lines produced.
- Compare before and after on a team basis and adjust practice.

**Show:** a small dashboard: review time, escaped defects, mutation score, per month.

**Check:** Why is "lines generated" a poor measure? *(Volume says nothing about correctness or value.)*

---

## MID-072-L06 · Demo: an AI-assisted refactor of the order saga under green tests (13 min)
**Goal:** refactor the Shop order saga orchestrator with AI. Prepares `MID-072-LAB1`.

**Steps**
1. Confirm the tests and contract tests are green; add a characterization test for compensation.
2. Prompt with goal, the saga class, its tests, and constraints; ask for a plan of small steps.
3. Apply step one (extract state transitions); run tests; commit.
4. **Planned mistake:** accept a large AI diff that also "simplifies" retry logic; a test fails because compensation order changed. Fix: reject and redo as small steps.
5. Ask AI for edge-case tests; discard one that only restates the code; run mutation tests.
6. Write the PR description with the prompt log and accepted and rejected suggestions.
