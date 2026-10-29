# BEG-014 · Methods — Lecture scripts

**Video:** 72 min · **Analogy used throughout:** a recipe card in a kitchen: a named set of steps that takes ingredients and gives back a dish.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-014-L01 · Why methods: naming and reuse (8 min)
**Goal:** see why we give a block of code a name.

**Key points**
- A method is a named block of code you can run many times.
- Write the logic once, call it from anywhere (a recipe card, not rewriting the recipe).
- A good name explains what the method does: `calculateTax`.
- Short methods are easier to read, test, and fix.
- You have already used methods: `println`, `nextInt`, `main`.

**Show**
```java
static void greet() {
    System.out.println("Hello!");
}
// in main: greet(); greet();
```

**Check:** What is the main benefit of a method? *(Write the logic once and reuse it by name.)*

---

## BEG-014-L02 · Parameters and return values (10 min)
**Goal:** pass data in and get a result out.

**Key points**
- Parameters are the ingredients: `static int add(int a, int b)`.
- The return type is the dish: `int` here; `void` means nothing comes back.
- `return` sends the value back and ends the method.
- Arguments are the real values you pass when calling.
- A method should do one job: compute or print, not both.

**Show**
```java
static int add(int a, int b) {
    return a + b;
}
int total = add(3, 4); // 7
```

**Check:** What does `void` mean as a return type? *(The method returns no value.)*

---

## BEG-014-L03 · Method signatures and overloading (8 min)
**Goal:** write several methods with the same name and let Java choose.

**Key points**
- A signature is the name plus the parameter types, in order.
- Overloading: same name, different parameter lists.
- Java picks the method that matches the arguments best.
- Changing only the return type is not overloading and does not compile.
- Use it when the action is the same but the input differs.

**Show**
```java
static int max(int a, int b) { return a > b ? a : b; }
static double max(double a, double b) { return a > b ? a : b; }
max(2, 5);     // int version
max(2.5, 1.0); // double version
```

**Check:** Can two methods differ only by return type? *(No.)*

---

## BEG-014-L04 · Scope: where variables live (8 min)
**Goal:** know which variables each part of the code can see.

**Key points**
- A variable lives only inside the braces where it is declared.
- Parameters and variables inside a method are private to that method (local).
- Each call gets its own fresh copy.
- Java passes arguments by value: the method gets a copy of the value.
- Changing a primitive parameter does not change the caller's variable. For objects, the copy is of the reference, so the same object is shared.

**Show**
```java
static void addOne(int x) { x = x + 1; }
int n = 5;
addOne(n);
System.out.println(n); // still 5
```

**Check:** After `addOne(n)`, what is `n`? *(Still 5; the method changed only its copy.)*

---

## BEG-014-L05 · The call stack (10 min)
**Goal:** picture how Java tracks method calls.

**Key points**
- The call stack is a pile of plates: each call puts a new plate (frame) on top.
- A frame holds that call's parameters and local variables.
- When a method returns, its plate is removed and the one below continues.
- The method on top is the one currently running.
- Too many plates cause `StackOverflowError`.

**Show:** a diagram: `main` at the bottom, `calculate` above, `add` on top, then `add` removed as it returns.

**Check:** Which method is running when the stack has `main`, `a`, `b`? *(`b`, the top one.)*

---

## BEG-014-L06 · Recursion basics (12 min)
**Goal:** write a method that calls itself safely.

**Key points**
- Recursion: a method solves a problem by calling itself on a smaller version.
- It needs a base case, where it stops without calling itself.
- Every call must move toward the base case.
- No base case means calls pile up until a stack overflow.
- Many recursive tasks can also be written with a loop.

**Show**
```java
static int factorial(int n) {
    if (n <= 1) return 1;        // base case
    return n * factorial(n - 1); // smaller problem
}
```

**Check:** What is the base case above? *(`n <= 1`, which returns 1.)*

---

## BEG-014-L07 · Demo: building the calculator one method at a time (8 min)
**Goal:** grow the calculator from small methods. Prepares `BEG-014-LAB1`.

**Steps**
1. Write `add`, `subtract`, `multiply` as methods that return values.
2. Write `divide` and return a message or a flag when the divisor is zero.
3. Write a `printMenu()` method and a loop in `main` that calls the right method.
4. **Planned mistake:** put the `println` inside `add`. It cannot be reused for a total. Move printing to the caller.
5. Add `power` (loop) and mention `factorial` is next.

**Check:** Why return a value instead of printing it? *(The caller can reuse it, test it, and format it.)*

---

## BEG-014-L08 · Demo: tracing recursion on the call stack (8 min)
**Goal:** watch `factorial(4)` build and unwind on the stack.

**Steps**
1. Set a breakpoint on the first line of `factorial`.
2. Run `factorial(4)` and step in. Open the Frames panel.
3. Watch frames for `n = 4, 3, 2, 1` pile up.
4. Step on: each frame returns its result and disappears (1, 2, 6, 24).
5. **Planned mistake:** remove the base case and run: `StackOverflowError`. Show the repeating lines in the stack trace.
6. Restore the base case.

**Check:** What does the stack look like at the deepest point? *(Four `factorial` frames above `main`.)*
