# BEG-020 · Classes and objects — Lecture scripts

**Video:** 66 min · **Analogy used throughout:** a blueprint and the houses built from it.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-020-L01 · Writing your first class (10 min)
**Goal:** write a class with fields in its own file.

**Key points**
- One public class per file; the file name matches the class name: `Account.java`.
- Class names start with a capital letter (`Account`, `BankStatement`).
- Fields are variables declared inside the class, outside any method.
- Each object gets its own copy of every instance field.
- Fields not given a value get a default: `0`, `0.0`, `false`, or `null`.

**Show**
```java
public class Account {
    String owner;
    String number;
    double balance;
}
```
(Using `double` for money is a shortcut for now; a better type comes in BEG-021.)

**Check:** What is the default value of an `int` field? *(0.)*

---

## BEG-020-L02 · Constructors (10 min)
**Goal:** create objects in a valid starting state.

**Key points**
- A constructor has the class name and no return type. It runs when you use `new`.
- If you write none, Java gives a no-argument one for free; once you write one, that free one disappears.
- **Overloading:** several constructors with different parameter lists.
- Keep constructors simple: set fields, do not do heavy work (no files, no network).
- A constructor can call another with `this(...)` to avoid repeating code.

**Show**
```java
public Account(String owner, String number, double balance) {
    this.owner = owner; this.number = number; this.balance = balance;
}
public Account(String owner, String number) {
    this(owner, number, 0.0);
}
```

**Check:** Does a constructor declare a return type? *(No.)*

---

## BEG-020-L03 · Instance methods and `this` (10 min)
**Goal:** write methods that work on the object's own data.

**Key points**
- An instance method is declared without `static` and runs on one particular object.
- Inside it, fields refer to that object's state.
- `this` means "the object I am running on".
- Use `this.balance` when a parameter has the same name as a field (shadowing); without `this` you assign the parameter to itself.
- Methods can return values or be `void`.

**Show**
```java
void deposit(double amount) { this.balance += amount; }
double getBalance() { return balance; }
```
Show the bug: `Account(String owner) { owner = owner; }` leaves the field `null`.

**Check:** What does `this` refer to? *(The current object.)*

---

## BEG-020-L04 · Creating and using objects (8 min)
**Goal:** build objects with `new` and call methods.

**Key points**
- `new Account("Ana", "A-1")` creates the object and runs a constructor.
- The variable holds a reference (an arrow) to the object, not the object itself.
- Call a method with the dot: `ana.deposit(50);`.
- Two variables can point to the same object; `b = a;` copies the arrow, not the object.
- A variable set to `null` points to nothing; calling a method on it throws `NullPointerException`.

**Show**
```java
Account ana = new Account("Ana", "A-1");
Account omar = new Account("Omar", "A-2", 80);
ana.deposit(50);
```

**Check:** After `Account b = ana;`, how many account objects exist? *(One, with two references.)*

---

## BEG-020-L05 · `static`: belonging to the class (12 min)
**Goal:** choose between instance and `static` members.

**Key points**
- Instance members belong to each object. `static` members belong to the class, one shared copy.
- Call static members by class name: `Account.getCount()`.
- A static method has no `this`, so it cannot use instance fields directly.
- Good uses: constants, utility methods, a shared counter.
- Rule of thumb: if it depends on one object's state, it is not static. Do not make everything static.

**Show**
```java
static int count = 0;
static final double MIN_DEPOSIT = 0.01;
Account(...) { count++; }
```

**Check:** Can a static method read `balance` directly? *(No; there is no object. It needs a reference.)*

---

## BEG-020-L06 · Demo: Bank Accounts v1 from an empty file (8 min)
**Goal:** build `Account` and a small `main` step by step. Prepares `BEG-020-LAB1`.

**Steps**
1. Create `Account.java` with fields `owner`, `number`, `balance`.
2. Add a constructor taking all three, then an overloaded one with balance 0 using `this(...)`.
3. Add `deposit` and `withdraw` methods.
4. In `Main`, create two accounts and move money in and out; print balances.
5. **Planned mistake:** write `owner = owner;` in the constructor and see `null` in the output. Fix with `this.owner = owner;`.
6. Keep `main` to wiring only: create objects, call methods, print.

---

## BEG-020-L07 · Demo: static vs instance, seen in the debugger (8 min)
**Goal:** see where static and instance data live. Prepares `BEG-020-LAB1`.

**Steps**
1. Add `static int count` to `Account` and increment it in the constructor.
2. Create three accounts and set a breakpoint after the third.
3. In the debugger variables view, show each object with its own `balance`, and `count` shown once for the class.
4. Print `Account.count`; it shows 3 no matter which object you use.
5. **Planned mistake:** make `balance` static. All accounts now show the same balance. Fix by removing `static`.
6. Summarize: shared across all = static; one per object = instance.
