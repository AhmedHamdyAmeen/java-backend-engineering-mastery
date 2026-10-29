# JNR-003 · Code quality — Lecture scripts

**Video:** 65 min · **Analogy used throughout:** tidying a workshop: tools with clear labels, each in its place, so anyone can find them.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## JNR-003-L01 · Code is read more than written (6 min)
**Goal:** see why readability matters most.

**Key points**
- You write a line once. Many people read it many times.
- Most work on a job is reading and changing existing code.
- Clear code costs less to change and has fewer bugs.
- Clever code is not good code; plain code is.
- Quality habits are small and repeated: names, small methods, tests.

**Show:** two versions of one method side by side: one with `a`, `b`, `x` and one with clear names.

**Check:** Who reads your code most? *(Other developers, including you later.)*

---

## JNR-003-L02 · Naming (10 min)
**Goal:** name things so the code reads as intent.

**Key points**
- A name says what, not how: `totalWithTax`, not `calc2`.
- Classes are nouns (`Cart`); methods are verbs (`addItem`); booleans read as questions (`isEmpty`).
- Avoid abbreviations and noise words like `Manager`, `Data`, `Info`.
- One word per idea: do not mix `get`, `fetch`, and `retrieve`.
- Rename with the IDE (Shift+F6 in IntelliJ), so every usage changes safely.

**Show**
```java
// before
double calc(double p, int q, double d) { return p * q - d; }
// after
Money lineTotal(Money unitPrice, int quantity, Money discount) { ... }
```

**Check:** Better name for `boolean flag` that says a cart has no items? *(`isEmpty`.)*

---

## JNR-003-L03 · Cohesion and coupling (10 min)
**Goal:** judge how well a class is built.

**Key points**
- Cohesion: do the parts of a class belong together? High cohesion is good.
- Coupling: how much does one class depend on others? Low coupling is good.
- Like a workshop: tools for one job in one drawer, and little need to walk between rooms.
- Reduce coupling: depend on a small interface, not on a concrete class; hide details.
- A class that does many unrelated things has low cohesion; split it.

**Show:** a diagram of `CheckoutService` linked to five concrete classes, then to two interfaces.

**Check:** Which do you want: high or low coupling? *(Low coupling, high cohesion.)*

---

## JNR-003-L04 · DRY, KISS, YAGNI — and their limits (9 min)
**Goal:** apply three rules and know when they clash.

**Key points**
- DRY: do not repeat the same knowledge in many places.
- KISS: keep it simple; the simplest design that works.
- YAGNI: do not build things you do not need yet.
- Conflict: removing small duplication can make code more complex (DRY against KISS).
- Rule of thumb: wait for the third repeat before you abstract; similar code is not always the same knowledge.

**Show:** two similar methods; one merge that needs a flag parameter and gets harder to read.

**Check:** When do you abstract repeated code? *(When the same idea appears about three times and is really the same.)*

---

## JNR-003-L05 · A catalog of code smells (12 min)
**Goal:** recognize common smells and the fix for each.

**Key points**
- A smell is a hint of a problem, not a bug.
- Long method: extract smaller methods.
- Large class: extract a class.
- Feature envy: a method uses another class's data more than its own; move it there.
- Primitive obsession: using `String` or `double` for ideas like money or email; make a small type (a record).
- Duplicated logic: extract a method.

**Show**
```java
// primitive obsession
void charge(double amount, String currency) { ... }
// better
void charge(Money amount) { ... }
```

**Check:** Which smell is `double price` for money? *(Primitive obsession.)*

---

## JNR-003-L06 · Safe refactoring with the IDE (8 min)
**Goal:** change structure without changing behavior.

**Key points**
- Refactoring: change the code's structure, not what it does.
- Always have tests first, and run them after each step.
- Use IDE tools: Rename, Extract Method, Extract Variable, Move, Inline.
- One small step per commit, named after the refactoring.
- No new features and no bug fixes in the same commit.

**Show:** the Extract Method dialog on a block inside `CheckoutService`.

**Check:** What must you have before refactoring? *(Tests that pass.)*

---

## JNR-003-L07 · Demo: refactoring a long method under green tests (10 min)
**Goal:** shrink a long `checkout` method step by step. Prepares JNR-003-LAB1.

**Steps**
1. Run all tests: green.
2. Rename unclear variables with the IDE.
3. Extract Method for the discount block; run tests; commit "Extract calculateDiscount".
4. **Planned mistake:** also change the rounding "while we are here"; a test turns red. Fix: undo, keep the commit pure, and do the change later in a separate commit.
5. Replace `double` money with the `Money` record where tests allow.
6. Show the final method: short, readable, tests green.

**Check:** Why undo the rounding change? *(A refactoring commit must not change behavior.)*
