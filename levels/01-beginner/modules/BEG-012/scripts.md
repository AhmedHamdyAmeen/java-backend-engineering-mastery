# BEG-012 · Conditions — Lecture scripts

**Video:** 52 min · **Analogy used throughout:** a road junction with signs that send each car down exactly one road.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-012-L01 · Making decisions with `if` (10 min)
**Goal:** run a block of code only when a condition is true.

**Key points**
- A condition is a question with a `true` or `false` answer (a `boolean`).
- `if (condition) { ... }` runs the block only when the answer is true.
- `else` is the road taken when the answer is false.
- Always use braces, even for one line. It prevents quiet bugs.
- Use `==` to compare, never a single `=`.

**Show**
```java
int age = 17;
if (age >= 18) {
    System.out.println("Adult");
} else {
    System.out.println("Minor");
}
```

**Check:** What type must the condition in an `if` have? *(boolean.)*

---

## BEG-012-L02 · `else if` chains and boundary values (8 min)
**Goal:** cover every case in a chain, including the edges.

**Key points**
- Java checks the chain top to bottom and takes the first true branch.
- Order matters: put the most specific test first.
- A boundary is the exact value where the answer changes (59 vs 60).
- `<` and `<=` differ only at the boundary, so test it by hand.
- End with `else` to catch everything left over.

**Show**
```java
if (score >= 90) grade = 'A';
else if (score >= 80) grade = 'B';
else if (score >= 70) grade = 'C';
else grade = 'F';
```
Test 90, 89, 80, 79, 70, 69.

**Check:** What grade does a score of exactly 80 get here? *(B.)*

---

## BEG-012-L03 · Classic `switch` and fall-through (8 min)
**Goal:** use `switch` for one value with many fixed choices, and avoid fall-through.

**Key points**
- `switch` picks a `case` that equals one value (int, char, String, enum).
- Each `case` should end with `break`.
- Without `break`, Java keeps running the next case. This is fall-through.
- `default` handles every value not listed.
- Use `switch` for exact matches, `if` for ranges.

**Show**
```java
switch (day) {
    case 6:
    case 7:
        System.out.println("Weekend");
        break;
    default:
        System.out.println("Weekday");
}
```

**Check:** What happens if you forget `break`? *(Execution falls into the next case.)*

---

## BEG-012-L04 · Switch expressions (modern Java) (8 min)
**Goal:** write a `switch` that produces a value, with no fall-through.

**Key points**
- The arrow form `case X -> value` never falls through, so no `break`.
- A switch expression returns a value you can assign.
- List several labels with a comma: `case 6, 7 ->`.
- It must cover all cases, so `default` is usually needed.
- Verify the Java version supports it (Java 14 and later) before recording.

**Show**
```java
String type = switch (day) {
    case 6, 7 -> "Weekend";
    default -> "Weekday";
};
```

**Check:** Why is `default` needed in a switch expression over an `int`? *(The expression must give a value for every possible int.)*

---

## BEG-012-L05 · Taming nested conditions (10 min)
**Goal:** flatten deep `if` nesting so it is easy to read.

**Key points**
- Deep nesting is a maze: each level adds more to remember.
- Combine tests with `&&` and `||` when they lead to the same result.
- An early exit (`return`, or rejecting bad input first) removes one level.
- Name a tricky test with a `boolean` variable: `boolean isMember = ...`.
- Check for overlapping branches (two that can both be true) and unreachable ones (never true).

**Show**
```java
// before: if (a) { if (b) { go(); } }
if (a && b) { go(); }
```

**Check:** Which operator replaces a nested `if` inside an `if`? *(`&&`.)*

---

## BEG-012-L06 · Demo: shipping cost rules and their boundaries (8 min)
**Goal:** turn written business rules into clean conditions and test the boundaries. Prepares `BEG-012-LAB1`.

**Steps**
1. Read the rules: up to 1 kg costs 5, up to 5 kg costs 10, above that 20; members get 10% off.
2. Write the weight chain with `else if` and a `double cost`.
3. Add the membership discount after the chain.
4. Build a test table: weights 0.5, 1, 1.01, 5, 5.01.
5. **Planned mistake:** use `weight < 1` instead of `<= 1`. The 1 kg row prints 10, not 5.
6. Fix with `<=`, rerun the table, and tick every row.

**Check:** Which input values find a boundary bug fastest? *(The exact boundary values and the ones just beside them.)*
