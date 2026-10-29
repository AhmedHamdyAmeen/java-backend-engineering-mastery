# JNR-055 · AI-assisted development workflow — Lecture scripts

**Video:** 62 min · **Analogy used throughout:** a fast but new teammate: helpful, quick, sometimes confidently wrong, and always needs a review.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## JNR-055-L01 · Assistants in the professional workflow (10 min)
**Goal:** know what an AI assistant is good for, and when to leave it off.

**Key points**
- An assistant suggests code (completion), answers questions (chat), and proposes edits (refactoring).
- Good uses: boilerplate, explaining unfamiliar code, first drafts of tests, small refactorings.
- Weak uses: new design decisions, security-sensitive code, anything you cannot check.
- It can be wrong and sound sure. You are responsible for every line you commit.
- Do not use it to skip learning: if you cannot explain the code, do not commit it.

**Show:** a table: task / use the assistant? / why.

**Check:** Who is responsible for AI-written code you commit? *(You are.)*

---

## JNR-055-L02 · Prompts with context: code, constraints, conventions (12 min)
**Goal:** write prompts that get useful answers.

**Key points**
- Give the relevant code, not the whole project.
- State constraints: Java version, libraries allowed, no behavior change.
- State conventions: naming, test style, formatting used by the team.
- Say the expected result: "return a refactored method and a list of changes".
- Ask for small steps, then check each one.

**Show**
```
Context: Java, Shop Core, CheckoutService.calculateTotal (code below).
Constraints: no behavior change; keep the public signature; no new libraries.
Conventions: JUnit 5, AssertJ, method names in camelCase.
Task: extract the discount block into a private method.
Result: the changed code only, plus one line per change.
```

**Check:** Name three things a good prompt includes. *(Code, constraints, conventions, and the expected result: any three.)*

---

## JNR-055-L03 · AI for tests and boilerplate, and how to review it (10 min)
**Goal:** use generated tests safely.

**Key points**
- Assistants write tests quickly, but often weak ones.
- Check each test: does it assert a real result, or only that nothing throws?
- Look for missing cases: empty cart, zero, negative, boundaries.
- Break the code on purpose: a good test fails; a useless test stays green.
- Read generated boilerplate like any other code before you accept it.

**Show**
```java
// weak: asserts nothing useful
assertNotNull(service.calculateTotal(cart));
// meaningful
assertEquals(new Money(1800, "EUR"), service.calculateTotal(cart));
```

**Check:** How can you test whether a generated test is useful? *(Change the code to be wrong; the test should fail.)*

---

## JNR-055-L04 · Reviewing AI-assisted pull requests (10 min)
**Goal:** review AI-assisted changes with the same standards as human code.

**Key points**
- The standard does not change: correctness, tests, readability, security.
- Large generated diffs are a warning sign; ask for smaller pull requests.
- Watch for invented methods, wrong imports, hidden behavior changes, and deleted checks.
- Ask the author to explain any part they cannot explain.
- Disclose AI use in the pull request when the team requires it.

**Show:** a review checklist with six items.

**Check:** Should AI-written code get a lighter review? *(No, the same review standard.)*

---

## JNR-055-L05 · Team policies: code privacy, secrets, licenses (8 min)
**Goal:** follow the team rules for AI tools.

**Key points**
- Use only tools your employer has approved.
- Never paste secrets (keys, passwords, tokens) or customer data into a prompt.
- Proprietary code may be private; check the policy before sharing it with a tool.
- Generated code may resemble licensed code; follow the team rules on licenses.
- When unsure, ask your lead before using the tool.

**Show:** a one-page policy outline: approved tools, forbidden inputs, disclosure, review rule.

**Check:** May you paste a production API key into a prompt? *(No, never.)*

---

## JNR-055-L06 · Demo: refactoring a long method with an assistant under green tests (12 min)
**Goal:** refactor `CheckoutService` with an assistant while keeping tests green. Prepares JNR-055-LAB1.

**Steps**
1. Run the tests: green. Open the log file for prompts.
2. Write a context-rich prompt to extract the discount block; read the proposed diff.
3. Accept the small change; run the tests; log what you accepted.
4. **Planned mistake:** accept a large suggestion that also changes rounding; a test fails. Fix: reject it, log the reason, and ask again for only the extraction.
5. Ask the assistant for missing tests; check each assertion; delete one that asserts nothing useful.
6. Commit with a note that AI helped, if the team requires it.

**Check:** What do you do with a big suggestion that breaks a test? *(Reject it and ask again for a smaller step.)*
