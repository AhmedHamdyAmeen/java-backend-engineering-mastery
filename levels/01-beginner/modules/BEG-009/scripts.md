# BEG-009 · Variables and data types — Lecture scripts

**Video:** 63 min · **Analogy used throughout:** labeled storage boxes of different sizes.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-009-L01 · Variables as labeled boxes (8 min)
**Goal:** declare and use a variable.

**Key points**
- A variable is a named box that holds one value.
- Declare it with a type and a name: `int age = 30;`.
- The type says what kind of value fits in the box.
- You can change the value later: `age = 31;`.
- A variable must be given a value before you use it.

**Show**
```java
int age = 30;
age = 31;
System.out.println(age);
```

**Check:** What are the two things a declaration needs? *(A type and a name.)*

---

## BEG-009-L02 · The eight primitive types (12 min)
**Goal:** pick the right primitive for the data.

**Key points**
- Whole numbers: `byte`, `short`, `int`, `long`. Use `int` by default; `long` for big values.
- Decimals: `float`, `double`. Use `double` by default.
- One character: `char`, in single quotes: `'A'`.
- True or false: `boolean`.
- Each type has a size and range. `int` holds about ±2 billion.
- Do not use `double` for money; it cannot store decimals like 0.1 exactly. (A better tool comes later.)

**Show:** a table: type / size / example value.

**Check:** Which type for a person's age? *(`int`.)* For `true`/`false`? *(`boolean`.)*

---

## BEG-009-L03 · Strings and reference types (8 min)
**Goal:** use `String` and know it is not a primitive.

**Key points**
- `String` holds text: `String name = "Ana";`.
- Primitives hold the value itself. Reference types hold a pointer to an object elsewhere in memory.
- `String` is a reference type; its name starts with a capital letter.
- `null` means "no object here".
- Compare text with `.equals(...)`, not `==`. The reason comes in a later module.

**Show:** a primitive box holding `30`, and a reference box holding an arrow to a `"Ana"` object.

**Check:** Is `int` a primitive or a reference type? *(Primitive.)*

---

## BEG-009-L04 · Literals, constants, and naming (8 min)
**Goal:** write values and names the Java way.

**Key points**
- A literal is a value written in code: `42`, `3.14`, `'A'`, `"Hi"`, `true`.
- `long` literals end in `L`: `5000000000L`. `float` literals end in `f`.
- `final` makes a variable a constant: `final double TAX = 0.15;`.
- Variables and methods use camelCase: `totalPrice`.
- Constants use UPPER_SNAKE_CASE; classes use PascalCase.
- Pick names that explain themselves.

**Show:** a before/after of `int x1 = 5;` versus `int itemCount = 5;`.

**Check:** What does `final` do? *(Stops the value from being changed.)*

---

## BEG-009-L05 · Type conversion and casting (12 min)
**Goal:** predict what happens when types mix.

**Key points**
- Widening is safe and automatic: `int` into `double`.
- Narrowing may lose data and needs a cast: `int x = (int) 3.9;` gives `3`.
- A cast cuts off the decimals; it does not round.
- Integer division drops the fraction: `7 / 2` is `3`.
- Overflow: an `int` past its limit wraps around to a negative number.

**Show**
```java
int a = 7 / 2;        // 3
double b = 7 / 2.0;   // 3.5
int big = Integer.MAX_VALUE + 1; // overflow
```

**Check:** What is `(int) 9.99`? *(9.)*

---

## BEG-009-L06 · Local type inference with `var` (7 min)
**Goal:** use `var` where the type is obvious.

**Key points**
- `var count = 10;` lets the compiler pick the type (`int`).
- The type is still fixed; `var` is not dynamic.
- Only for local variables with a value on the same line.
- Use it when the right side makes the type clear; avoid it when it hides the type.

**Show:** `var name = "Ana";` (clear) versus `var x = compute();` (unclear).

**Check:** Can you write `var x;` with no value? *(No.)*

---

## BEG-009-L07 · Demo: unit converter and an integer overflow (8 min)
**Goal:** apply types to a small program. Prepares `BEG-009-LAB1`.

**Steps**
1. Declare Celsius as a `double` and convert to Fahrenheit.
2. Convert kilometres to miles; print with text.
3. Store a price as `int` cents instead of `double`.
4. **Planned mistake:** `int half = 5 / 2;` prints `2`, not 2.5. Fix with `5 / 2.0`.
5. Show overflow: `Integer.MAX_VALUE + 1` becomes negative; explain in a comment.
