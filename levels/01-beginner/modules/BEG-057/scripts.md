# BEG-057 · Verifying AI-generated code — Lecture scripts

**Video:** 40 min · **Analogy used throughout:** a proofreader checking a draft written by a fast but sometimes careless assistant.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-057-L01 · Generated code is a draft, not an answer (8 min)
**Goal:** treat AI-generated code as untrusted until you have checked it.

**Key points**
- An AI assistant writes code that looks right, but it predicts text; it does not run or understand your requirement.
- Typical faults: off-by-one errors, missing edge cases (empty, `null`, negative), wrong complexity, and **invented** library calls (methods that do not exist).
- You are responsible for any code you submit or ship, whoever wrote it.
- Rule: if you cannot explain a line, you cannot use it.
- Workflow: write the requirement, get a draft, read it, test it, fix it, explain it.

**Show:** a short generated method with a plausible call such as `list.firstOrNull()` (not a Java method) that fails to compile.

**Check:** Who is responsible for generated code you submit? *(You are.)*

---

## BEG-057-L02 · Reading and tracing code you did not write (10 min)
**Goal:** explain generated code by tracing it by hand.

**Key points**
- Read once for the idea, then trace line by line with a small input.
- Keep a table of variable values after each step (a **trace table**).
- Trace the edges too: empty input, one item, the last item.
- Check the complexity: look for hidden loops such as `contains` inside a loop.
- Write one sentence per block saying what it does; gaps show what you do not yet understand.

**Show**
```java
int countPositives(int[] a) {
    int c = 0;
    for (int i = 1; i < a.length; i++)   // starts at 1: skips a[0]
        if (a[i] > 0) c++;
    return c;
}
```
Trace `[5, -1, 2]`: result 1, but the right answer is 2.

**Check:** What does a trace table record? *(The values of variables after each step.)*

---

## BEG-057-L03 · Testing generated code against the requirement (8 min)
**Goal:** write tests from the requirement, not from the generated code.

**Key points**
- Write the tests **before** you look at the generated code, using the requirement alone.
- A test copied from the code's behavior only confirms the bug.
- Cover the normal case, boundaries, and invalid input (BEG-045 skills).
- Add a size test (a large input) to catch slow solutions.
- When a test fails, decide whether the code or your test is wrong by rereading the requirement.

**Show:** requirement "return the index of a value in a sorted array, or -1"; tests for empty array, first item, last item, missing value, one item.

**Check:** Why write tests before reading the generated code? *(So they reflect the requirement, not the code's mistakes.)*

---

## BEG-057-L04 · Licensing, integrity, and disclosure (6 min)
**Goal:** know the rules for using AI-generated code honestly.

**Key points**
- Generated code can resemble existing open-source code; **licenses** may apply. Check your employer's or project's policy.
- Never paste secrets, customer data, or private code into a public assistant.
- **Academic integrity**: follow your course's rules. If AI use is allowed with disclosure, say what you used it for.
- A good disclosure: the tool, what you asked it for, and what you changed or tested.
- Submitting code you cannot explain, as if it were your own, breaks the rules.

**Show:** a README line: "Binary search first drafted with an AI assistant; I wrote the tests and fixed a boundary bug."

**Check:** What does an honest disclosure contain? *(What tool, what for, and what you checked or changed.)*

---

## BEG-057-L05 · Demo: catching a subtle bug in generated binary search with tests (8 min)
**Goal:** find a hidden defect in generated code with tests written from the requirement. Prepares BEG-057-LAB1.

**Steps**
1. Write the requirement: `search(int[] sorted, int target)` returns the index or -1.
2. Write tests first: empty array, one item (found and not found), first, last, middle, missing, duplicates not needed.
3. Paste the generated code; it compiles and the middle tests pass.
4. **Planned mistake:** the generated loop is `while (lo < hi)` instead of `lo <= hi`. The test "one item, found" fails because the loop never runs.
5. Trace by hand with `[7]` to see why; fix the condition and rerun until green.
6. Check the complexity: O(log n). Explain the final code in a comment.

**Check:** Which test caught the bug? *(The one-item array search; the loop never ran.)*
