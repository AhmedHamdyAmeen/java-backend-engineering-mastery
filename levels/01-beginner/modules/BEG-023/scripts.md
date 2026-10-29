# BEG-023 · Polymorphism — Lecture scripts

**Video:** 48 min · **Analogy used throughout:** a bank teller pressing the same "month-end" button on every account card, and each card type doing its own thing.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-023-L01 · One call, many behaviors (10 min)
**Goal:** understand that the same call can run different code.

**Key points**
- **Polymorphism** = "many forms": one method call, different behavior depending on the real object.
- A `Account` reference can hold a `SavingsAccount` or a `CheckingAccount` object.
- Calling `acc.monthEnd()` runs the version belonging to the real object.
- The caller does not need to know which kind it has.
- It only works for overridden instance methods.

**Show**
```java
Account a = new SavingsAccount("Ana", "S-1", 0.02);
a.monthEnd();   // runs SavingsAccount.monthEnd, not Account.monthEnd
```

**Check:** Which `monthEnd` runs: the reference type's or the object's? *(The object's.)*

---

## BEG-023-L02 · Upcasting, downcasting, and `instanceof` (10 min)
**Goal:** move between parent and child types safely.

**Key points**
- **Upcasting:** child to parent. Automatic and always safe: `Account a = new SavingsAccount(...)`.
- Through the parent reference you can only call methods the parent declares.
- **Downcasting:** parent to child, written `(SavingsAccount) a`. Risky: fails with `ClassCastException` if wrong.
- Check first with `instanceof`: `if (a instanceof SavingsAccount s)`.
- Needing many downcasts is a design smell.

**Show**
```java
Account a = new SavingsAccount("Ana", "S-1", 0.02);
if (a instanceof SavingsAccount s) { s.addInterest(); }
```

**Check:** Which direction needs an explicit cast? *(Downcasting, parent to child.)*

---

## BEG-023-L03 · Dynamic dispatch under the hood (conceptual) (8 min)
**Goal:** know how Java picks the method at run time.

**Key points**
- **Compile time:** Java checks the method exists on the reference type.
- **Run time:** the JVM looks at the real class of the object and picks its version. This is **dynamic dispatch**.
- Roughly: each class has a table of its methods; the object points to its class.
- Fields and static methods are not dispatched this way; they follow the reference type.
- **Overloading** (same name, different parameters) is chosen at compile time; **overriding** at run time.

**Show:** a diagram: reference `a` (type Account) → object (class SavingsAccount) → method table where `monthEnd` points to the Savings version.

**Check:** Is overloading resolved at compile time or run time? *(Compile time.)*

---

## BEG-023-L04 · Replacing conditionals with polymorphism (12 min)
**Goal:** remove `if`/`switch` on type.

**Key points**
- A chain like `if (type.equals("SAVINGS")) ... else if (type.equals("CHECKING")) ...` repeats everywhere a new type appears.
- Move each branch into an overriding method of its own class.
- The caller becomes one line: `account.monthEnd()`.
- Adding a new type means adding a class; the calling code stays unchanged.
- Not every `if` is a problem; replace those that switch on kind.

**Show**
```java
// before
if (a instanceof SavingsAccount) { ... } else if (a instanceof CheckingAccount) { ... }
// after
a.monthEnd();
```

**Check:** What do you do to add a new account type after the refactor? *(Write a new subclass; the loop does not change.)*

---

## BEG-023-L05 · Demo: month-end processing without a single type check (8 min)
**Goal:** process mixed accounts in one loop. Prepares `BEG-023-LAB1`.

**Steps**
1. Start with a loop full of `instanceof` checks that applies interest or fees.
2. Add `monthEnd()` to `Account` (default: do nothing).
3. Override it in `SavingsAccount` (add interest) and `CheckingAccount` (charge a fee).
4. Replace the loop body with `a.monthEnd()` over a `List<Account>`.
5. **Planned mistake:** misspell the override as `monthend()`; without `@Override` the wrong code runs. Add `@Override` and see the compiler error.
6. Add a `BusinessAccount` class and run the same loop untouched.
