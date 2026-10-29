# BEG-013 · Loops — Lecture scripts

**Video:** 58 min · **Analogy used throughout:** running laps on a track with a lap counter and a finish line.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-013-L01 · Why loops: repetition without copy-paste (6 min)
**Goal:** see why repeating code by hand fails and loops fix it.

**Key points**
- Copy-pasting a line 100 times is slow and breaks when the count changes.
- A loop repeats a block while a condition holds.
- Every loop has three parts: start, condition, update (the lap counter).
- Each pass through the body is one iteration.
- Java has `for`, `while`, and `do-while`.

**Show**
```java
// instead of ten println lines
for (int i = 1; i <= 10; i++) {
    System.out.println("Line " + i);
}
```

**Check:** What are the three parts of a loop? *(Start, condition, update.)*

---

## BEG-013-L02 · The `for` loop (10 min)
**Goal:** write a counting loop correctly.

**Key points**
- Shape: `for (start; condition; update) { body }`.
- Use it when you know how many times to repeat.
- `i++` adds one after each iteration.
- The condition is checked before every pass.
- Count down with `i--`, skip with `i += 2`.

**Show**
```java
int sum = 0;
for (int i = 1; i <= 5; i++) {
    sum += i;
}
System.out.println(sum); // 15
```

**Check:** How many times does `for (int i = 0; i < 3; i++)` run? *(3 times: 0, 1, 2.)*

---

## BEG-013-L03 · `while` and `do-while` (10 min)
**Goal:** loop when you do not know the count in advance.

**Key points**
- `while (condition)` checks first, so it may run zero times.
- `do { ... } while (condition);` runs once, then checks. Note the final semicolon.
- Use `while` for "until something happens" (valid input, game over).
- You must change something in the body, or the loop never ends.
- Prefer `for` for counting, `while` for waiting.

**Show**
```java
int n;
do {
    System.out.print("Enter 1-10: ");
    n = scanner.nextInt();
} while (n < 1 || n > 10);
```

**Check:** Which loop always runs at least once? *(`do-while`.)*

---

## BEG-013-L04 · `break`, `continue`, and loop control (8 min)
**Goal:** leave or skip part of a loop on purpose.

**Key points**
- `break` stops the whole loop right now.
- `continue` skips the rest of this pass and goes to the next.
- Use them for clear special cases, not to hide tangled logic.
- In nested loops they affect only the innermost loop.
- Do not change the loop variable inside the body.

**Show**
```java
for (int i = 1; i <= 10; i++) {
    if (i % 2 == 0) continue; // skip evens
    if (i > 7) break;         // stop after 7
    System.out.println(i);    // 1 3 5 7
}
```

**Check:** What does `continue` do? *(Skips to the next iteration.)*

---

## BEG-013-L05 · Nested loops (10 min)
**Goal:** use a loop inside a loop for rows and columns.

**Key points**
- The inner loop runs completely for each pass of the outer loop.
- Total runs = outer count × inner count.
- Think of rows (outer) and columns (inner) of a grid.
- Use different names: `row`, `col`, not `i`, `i`.
- Big nested loops get slow quickly.

**Show**
```java
for (int row = 1; row <= 3; row++) {
    for (int col = 1; col <= 4; col++) {
        System.out.print("* ");
    }
    System.out.println();
}
```
Body runs 3 × 4 = 12 times.

**Check:** How many times does the body run for 5 rows and 6 columns? *(30.)*

---

## BEG-013-L06 · Off-by-one errors and infinite loops (6 min)
**Goal:** spot the two classic loop bugs.

**Key points**
- Off by one: running one time too many or too few, often `<` vs `<=`.
- Test the first and last iteration by hand.
- Infinite loop: the condition never becomes false.
- Common cause: forgetting the update, or updating the wrong variable.
- Stop a runaway program with the stop button in IntelliJ.

**Show**
```java
int i = 0;
while (i < 5) {
    System.out.println(i);
    // missing i++  -> infinite loop
}
```

**Check:** What usually causes an infinite `while`? *(The variable in the condition is never updated.)*

---

## BEG-013-L07 · Demo: number guessing game, stepping through the loop in the debugger (8 min)
**Goal:** build the guessing game and watch the loop run in the debugger. Prepares `BEG-013-LAB1`.

**Steps**
1. Create a random target: `new Random().nextInt(100) + 1`.
2. Write a `while` loop with an attempt counter and a limit of 7.
3. Read a guess, print "higher", "lower", or "correct", and stop on correct.
4. Set one breakpoint on the loop line; step over and watch `attempts` change.
5. **Planned mistake:** forget `attempts++`; the game never ends. The debugger shows `attempts` stuck at 0.
6. Add the increment, rerun, then add a replay question.

**Check:** What did the debugger show that the screen did not? *(The variable values on each pass.)*
