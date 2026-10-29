# BEG-024 · Abstract classes and interfaces — Lecture scripts

**Video:** 53 min · **Analogy used throughout:** a wall socket: any device that fits the plug works, and the wall does not care which device it is.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-024-L01 · Interfaces as contracts (12 min)
**Goal:** declare an interface and implement it in several classes.

**Key points**
- An **interface** lists methods a class promises to provide, without saying how.
- A class says `implements Notifier` and must write every method of it.
- A class can implement many interfaces (unlike `extends`).
- Interface methods are `public` and abstract by default; fields are constants.
- You can use the interface as a type: `Notifier n = new EmailNotifier();`.

**Show**
```java
public interface Notifier { void send(String to, String message); }
public class EmailNotifier implements Notifier {
    @Override public void send(String to, String message) { /* send email */ }
}
```

**Check:** Can a class implement two interfaces? *(Yes.)*

---

## BEG-024-L02 · Abstract classes (10 min)
**Goal:** write a partly finished parent class.

**Key points**
- An `abstract class` cannot be instantiated with `new`.
- It can hold fields, constructors, normal methods, and `abstract` methods (no body).
- Subclasses must implement every abstract method (unless they are abstract too).
- Use it to share state and code among closely related classes.
- A class has only one superclass, so choose carefully.

**Show**
```java
public abstract class Account {
    protected double balance;
    public abstract double monthlyFee();
    public void deposit(double a) { balance += a; }
}
```

**Check:** Can you write `new Account()` for an abstract class? *(No.)*

---

## BEG-024-L03 · Interface vs abstract class: decision guide (10 min)
**Goal:** pick the right tool.

**Key points**
- Interface: a capability or role ("can notify", "can be compared"). No instance state. Many per class.
- Abstract class: a shared base with state and common code ("is a kind of account"). One per class.
- Unrelated classes can share an interface; abstract classes suit one family.
- Default choice: start with an interface; add an abstract class only when sharing real state or code.
- You can combine: an interface plus an abstract helper class that implements part of it.

**Show:** a two-column table: question / interface / abstract class (shared fields? many parents? unrelated types?).

**Check:** You need `Email` and `Printer` to both be `Sendable`, but they are unrelated. Which one? *(Interface.)*

---

## BEG-024-L04 · Default and static interface methods (8 min)
**Goal:** know what `default` is for and its risks.

**Key points**
- A `default` method has a body inside the interface; implementers inherit it.
- Purpose: add a method to an existing interface without breaking all implementers.
- Risk: two interfaces with the same default method force the class to choose; it is easy to hide logic in interfaces.
- A `static` interface method is a utility called as `Notifier.of(...)`.
- Do not use defaults to build state-like behavior; keep interfaces small.

**Show**
```java
public interface Notifier {
    void send(String to, String message);
    default void sendAll(List<String> to, String m) { for (String t : to) send(t, m); }
}
```

**Check:** Why were default methods added? *(To evolve interfaces without breaking existing implementations.)*

---

## BEG-024-L05 · Programming to an interface (5 min)
**Goal:** depend on the contract, not the class.

**Key points**
- Declare variables and parameters with the interface type: `Notifier`, not `EmailNotifier`.
- The code using it works with any implementation, including a fake one in tests.
- Swapping implementations needs no change in the user class.
- Example from the library: `List<String> x = new ArrayList<>();`.
- Choose the concrete class in one place only.

**Show**
```java
class Bank { private final Notifier notifier; Bank(Notifier n) { this.notifier = n; } }
```

**Check:** Why declare `List<String>` instead of `ArrayList<String>`? *(You can change the implementation without changing other code.)*

---

## BEG-024-L06 · Demo: pluggable notification channels (8 min)
**Goal:** let the bank send statements through any channel. Prepares `BEG-024-LAB1`.

**Steps**
1. Declare `Notifier` with one focused method `send(String to, String message)`.
2. Implement `ConsoleNotifier`, then `EmailNotifier` and `SmsNotifier` (printing is fine for the demo).
3. Give `Bank` a `Notifier` field set in its constructor.
4. Call `notifier.send(...)` from `Bank.sendStatement(...)`; run with each channel.
5. **Planned mistake:** declare the field as `EmailNotifier`; show swapping to SMS now requires editing `Bank`. Change the type to `Notifier`.
6. Confirm `Bank` imports and uses only the interface.
