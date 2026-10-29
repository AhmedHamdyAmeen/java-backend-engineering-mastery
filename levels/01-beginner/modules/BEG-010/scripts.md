# BEG-010 · Operators — Lecture scripts

**Video:** 48 min · **Analogy used throughout:** a calculator with a few extra buttons.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-010-L01 · Arithmetic operators and integer division (10 min)
**Goal:** predict the result of arithmetic on numbers.

**Key points**
- `+ - * /` work as expected; `%` gives the remainder (modulo).
- With two `int`s, `/` drops the fraction: `7 / 2` is `3`.
- Make one side a `double` to keep decimals: `7 / 2.0` is `3.5`.
- `7 % 2` is `1`. Use `%` to test even or odd: `n % 2 == 0`.
- Dividing an `int` by zero throws an error while running; a `double` gives `Infinity`.

**Show**
```java
System.out.println(7 / 2);    // 3
System.out.println(7 / 2.0);  // 3.5
System.out.println(7 % 2);    // 1
```

**Check:** What is `10 % 3`? *(1.)*

---

## BEG-010-L02 · Comparison and logical operators (10 min)
**Goal:** build `true`/`false` expressions.

**Key points**
- Comparison: `==  !=  <  >  <=  >=`. Each gives a `boolean`.
- `=` assigns; `==` compares. Mixing them up is a classic mistake.
- Logical: `&&` (and), `||` (or), `!` (not).
- `a && b` is true only if both are true; `a || b` if at least one is.
- You cannot chain `1 < x < 10`. Write `x > 1 && x < 10`.

**Show**
```java
int age = 20;
boolean adult = age >= 18;
boolean teen = age >= 13 && age <= 19;
```

**Check:** Write "x is between 1 and 10". *(`x > 1 && x < 10`.)*

---

## BEG-010-L03 · Assignment and compound assignment (6 min)
**Goal:** update a variable concisely.

**Key points**
- `=` stores the right side into the left variable.
- `x += 5` means `x = x + 5`. Also `-=  *=  /=  %=`.
- The right side is calculated first, then stored.
- Compound assignment on `int` quietly casts back to `int`.

**Show:** `int total = 10; total += 5; total *= 2;` prints `30`.

**Check:** After `int x = 4; x -= 1;`, what is `x`? *(3.)*

---

## BEG-010-L04 · Increment, decrement, and precedence (8 min)
**Goal:** tell prefix from postfix and read mixed expressions.

**Key points**
- `i++` adds 1. `i--` subtracts 1.
- Postfix `i++` gives the old value, then adds. Prefix `++i` adds, then gives the new value.
- Precedence: `*  /  %` before `+  -`, then comparison, then `&&`, then `||`.
- Parentheses override the order. Use them to make intent clear.

**Show**
```java
int i = 5;
int a = i++;  // a = 5, i = 6
int b = ++i;  // i = 7, b = 7
System.out.println(2 + 3 * 4);   // 14
System.out.println((2 + 3) * 4); // 20
```

**Check:** After `int i = 1; int j = i++;`, what are `i` and `j`? *(`i` is 2, `j` is 1.)*

---

## BEG-010-L05 · Short-circuit evaluation (6 min)
**Goal:** use `&&` and `||` to avoid errors.

**Key points**
- `a && b`: if `a` is false, Java does not evaluate `b`.
- `a || b`: if `a` is true, Java does not evaluate `b`.
- Put the safe check first: `d != 0 && 10 / d > 1` never divides by zero.
- Do not rely on side effects inside the second operand.

**Show:** the same condition with the check first (safe) and last (crashes).

**Check:** Why is `d != 0 && 10 / d > 1` safe? *(If `d` is 0 the right side never runs.)*

---

## BEG-010-L06 · Demo: predict-then-run expression challenge (8 min)
**Goal:** build the habit of predicting before running. Prepares `BEG-010-LAB1`.

**Steps**
1. Write six expressions on screen and predict each aloud.
2. Run them in one program and compare.
3. Cover `7 / 2`, `7 % 3`, `i++` vs `++i`, and precedence.
4. **Planned mistake:** predict `1 + 2 + "3"` as `6`; the answer is `"33"`. Explain left-to-right evaluation.
5. Record each mismatch with a one-line reason.
