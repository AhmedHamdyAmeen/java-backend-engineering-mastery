# BEG-016 · Problem-solving — Lecture scripts

**Video:** 53 min · **Analogy used throughout:** planning a trip with a map before you start driving.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-016-L01 · Understanding the problem first (8 min)
**Goal:** know exactly what is being asked before writing code.

**Key points**
- Coding before understanding is driving without knowing the destination.
- Restate the problem in your own words.
- Name the inputs (what you get), outputs (what you must produce), and constraints (limits and rules).
- Work one small example by hand.
- Ask questions about anything unclear.

**Show**
Problem: "find the second largest number."
Inputs: a list of integers. Output: one integer. Constraints: at least two values? duplicates? Example: `[4, 9, 7]` gives 7.

**Check:** Name the three things to identify first. *(Inputs, outputs, constraints.)*

---

## BEG-016-L02 · Decomposition (8 min)
**Goal:** split a big problem into small steps you can solve.

**Key points**
- Big problems are a chain of small ones, like legs of a trip.
- Write each step in one plain sentence.
- Solve each step separately, then join them.
- Each step often becomes a method later.
- If a step is still big, split it again.

**Show**
Problem: average of valid grades.
1. Read the grades. 2. Skip invalid ones. 3. Add up the valid ones. 4. Divide by the count. 5. Print the result.

**Check:** What does each small step often become in code? *(A method.)*

---

## BEG-016-L03 · Pseudocode and flowcharts (10 min)
**Goal:** describe a solution in plain structure before Java.

**Key points**
- Pseudocode is plain English with code-like structure: IF, FOR, SET.
- No syntax rules; focus on logic.
- A flowchart uses boxes for steps, diamonds for yes/no decisions, and arrows for order.
- Both let you find mistakes cheaply, before coding.
- Keep the plan next to the code and update both.

**Show**
```text
SET largest = first value
FOR each other value
    IF value > largest
        SET largest = value
PRINT largest
```

**Check:** What shape is a decision in a flowchart? *(A diamond.)*

---

## BEG-016-L04 · Hand-tracing with a variable table (10 min)
**Goal:** run code on paper to see what it really does.

**Key points**
- Make a table: one column per variable, one row per step.
- Execute one line at a time and write the new values.
- Compare with what you expected; the first difference is the bug.
- Trace small inputs first.
- The debugger (BEG-018) does this for you, but tracing builds the skill.

**Show**
`sum = 0; for i = 1..3: sum += i`

| step | i | sum |
| --- | --- | --- |
| start | - | 0 |
| 1 | 1 | 1 |
| 2 | 2 | 3 |
| 3 | 3 | 6 |

**Check:** Where do you look for the bug in a trace table? *(At the first row that differs from what you expected.)*

---

## BEG-016-L05 · Thinking in edge cases (9 min)
**Goal:** list the unusual inputs before coding.

**Key points**
- Edge cases are inputs at the limits where code often breaks.
- Typical list: empty, one element, two elements, maximum, minimum, negative, zero, duplicates, invalid.
- Happy-path-only testing misses most bugs.
- Write the list with the expected result for each.
- Turn the list into test inputs later.

**Show**
For "largest number in an array": empty array (no answer, decide what to do), one element, all equal, all negative, largest at the start or the end.

**Check:** Name three edge cases for any list problem. *(Empty, one element, duplicates or negatives.)*

---

## BEG-016-L06 · Demo: plan before code on an unseen problem (8 min)
**Goal:** solve a new problem using the full plan-first routine. Prepares `BEG-016-LAB1`.

**Steps**
1. Read the problem: "count how many words in a sentence are longer than 4 letters."
2. Restate it; list inputs, outputs, constraints.
3. Write pseudocode and the edge cases: empty text, extra spaces, punctuation.
4. Trace the pseudocode on one example with a variable table.
5. **Planned mistake:** code straight from the first idea and miss extra spaces; `split(" ")` gives empty words. Return to the edge-case list and fix with `trim()` and `split("\\s+")`.
6. Check that the plan and code match.

**Check:** Which step found the bug? *(The edge-case list, which we skipped at first.)*
