# BEG-022 · Inheritance — Lecture scripts

**Video:** 66 min · **Analogy used throughout:** a family tree: a child gets traits from a parent but can have its own.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-022-L01 · Reusing behavior with `extends` (10 min)
**Goal:** create a subclass that reuses a superclass.

**Key points**
- `class SavingsAccount extends Account` makes `SavingsAccount` a **subclass** of `Account` (the **superclass**).
- The subclass gets the accessible fields and methods of the parent and can add its own.
- Java allows only one superclass per class.
- Use the **is-a** test: a savings account *is an* account. A car is not an engine.
- Inherit to model "is a kind of", not just to save typing.

**Show**
```java
public class SavingsAccount extends Account {
    private double interestRate;
    public void addInterest() { deposit(getBalance() * interestRate); }
}
```

**Check:** Can a class extend two classes? *(No, only one.)*

---

## BEG-022-L02 · Constructors and `super` (10 min)
**Goal:** build the parent part of an object correctly.

**Key points**
- Constructors are **not** inherited.
- A subclass constructor must call a superclass constructor with `super(...)` as its first statement.
- If you write nothing, Java inserts `super()`; this fails if the parent has no no-argument constructor.
- The parent part is built first, then the child part.
- `super.method()` calls the parent's version of a method.

**Show**
```java
public SavingsAccount(String owner, String number, double rate) {
    super(owner, number);
    this.interestRate = rate;
}
```

**Check:** What must be the first statement of a subclass constructor? *(A call to `super(...)` or `this(...)`.)*

---

## BEG-022-L03 · Overriding methods (10 min)
**Goal:** replace a parent's behavior in the child.

**Key points**
- **Overriding:** same name and parameters, new body in the subclass.
- Always add `@Override`: the compiler then catches typos and wrong signatures.
- You may call the parent's version with `super.withdraw(amount)`.
- Do not weaken the contract: the child should still honor what the parent promises.
- Private members and constructors are not inherited, so they cannot be overridden. Static methods are hidden, not overridden.

**Show**
```java
@Override
public void withdraw(double amount) {
    // checking account: allow overdraft up to a limit
}
```
Show a typo `widthdraw` that compiles silently without `@Override` and fails with it.

**Check:** What does `@Override` protect you from? *(Mistyped names or wrong parameters that silently create a new method.)*

---

## BEG-022-L04 · `final` classes and methods (6 min)
**Goal:** stop inheritance or overriding when it is unsafe.

**Key points**
- `final class` cannot be extended (`String` is final).
- `final` method cannot be overridden.
- Use it for classes not designed for extension, and for critical rules.
- Immutable classes should be final.
- Design for inheritance deliberately, or forbid it.

**Show**
```java
public final class Money { ... }
public final void audit() { ... }
```

**Check:** Can you extend a `final` class? *(No.)*

---

## BEG-022-L05 · Composition over inheritance (14 min)
**Goal:** choose "has-a" when "is-a" does not fit.

**Key points**
- **Composition:** a class holds another object in a field and uses it ("has-a").
- Inheritance ties the child tightly to the parent; changes in the parent can break children.
- Bad sign: the child inherits methods it should not have (a `Stack extends ArrayList`).
- Bad sign: inheritance only for code reuse, or deep hierarchies of 4+ levels.
- Composition is flexible: you can swap the held part at runtime.

**Show**
```java
class Car {
    private final Engine engine;      // has-a, not extends Engine
    Car(Engine engine) { this.engine = engine; }
    void start() { engine.ignite(); }
}
```

**Check:** Is "Car extends Engine" correct? *(No; a car has an engine, it is not one.)*

---

## BEG-022-L06 · Demo: savings and checking accounts with `extends` (8 min)
**Goal:** add two account types to Bank Accounts. Prepares `BEG-022-LAB1`.

**Steps**
1. Start from `Account` (v2). Make fields accessible through methods or `protected` only where needed.
2. Create `SavingsAccount extends Account` with a rate and `addInterest()`.
3. Create `CheckingAccount extends Account` with an overdraft limit; override `withdraw` using `@Override`.
4. Use `super(...)` in both constructors.
5. **Planned mistake:** forget `super(...)` while `Account` has no no-argument constructor; read the compile error and fix.
6. In `main`, create one of each and call the inherited and overridden methods.

---

## BEG-022-L07 · Demo: refactoring bad inheritance into composition (8 min)
**Goal:** replace a wrong "is-a" with "has-a". Prepares `BEG-022-LAB1`.

**Steps**
1. Show a provided bad hierarchy: `Stack extends ArrayList<String>` exposing `add(0, x)` and `remove(i)`.
2. Name the broken rule: users can break the "last in, first out" behavior.
3. Create `Stack` with a private `ArrayList` field.
4. Expose only `push`, `pop`, `peek`, `isEmpty`, forwarding to the list.
5. **Planned mistake:** leave a public `getItems()` returning the internal list; show it leaks control. Return a copy or remove it.
6. Explain the refactor in two sentences, as required by the lab.
