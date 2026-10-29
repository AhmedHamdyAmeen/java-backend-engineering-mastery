# BEG-021 · Encapsulation — Lecture scripts

**Video:** 53 min · **Analogy used throughout:** a bank vault with a teller window: you ask the teller; you never reach into the vault.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-021-L01 · Why hide data (8 min)
**Goal:** see why direct field access is dangerous.

**Key points**
- Encapsulation = keep the data private and let only the object's methods change it.
- If `balance` is public, any code can write `account.balance = -500;`.
- Rules then have to be repeated in every caller, and someone will forget.
- Hiding data lets you change the inside later without breaking callers.
- The public methods are the object's "window"; everything else is hidden.

**Show**
```java
account.balance = -500;   // compiles when balance is public. Nothing stops it.
```

**Check:** What is the main benefit of making fields private? *(Only the class can change its own data, so it can protect its rules.)*

---

## BEG-021-L02 · Access modifiers (10 min)
**Goal:** apply the four visibility levels.

**Key points**
- `private`: only inside the same class.
- *(no modifier)* package-private: classes in the same package.
- `protected`: same package, plus subclasses.
- `public`: everywhere.
- Start with the most restrictive level and open up only when needed.

**Show:** a table with rows private / package-private / protected / public and columns same class / same package / subclass / anywhere.

**Check:** Which level is the default when you write no modifier? *(Package-private.)*

---

## BEG-021-L03 · Invariants: rules the object guarantees (10 min)
**Goal:** enforce a rule inside the class.

**Key points**
- An **invariant** is a rule that is always true for the object, such as "balance is never negative".
- Enforce it in the constructor and in every method that changes the data.
- Reject bad input immediately: throw `IllegalArgumentException` with a clear message.
- Callers then cannot create an invalid object, even by mistake.
- Do not rely on callers to check first.

**Show**
```java
public void withdraw(double amount) {
    if (amount <= 0) throw new IllegalArgumentException("Amount must be positive");
    if (amount > balance) throw new IllegalStateException("Insufficient funds");
    balance -= amount;
}
```

**Check:** Where should the "no negative balance" rule live? *(Inside Account, not in the callers.)*

---

## BEG-021-L04 · Getters, setters, and "tell, don't ask" (8 min)
**Goal:** choose between getters/setters and behavior methods.

**Key points**
- A getter reads a value; a setter replaces it. Add one only when callers truly need it.
- A public `setBalance` breaks the invariant: it lets anyone skip the rules.
- Prefer behavior methods: `deposit`, `withdraw`, `transferTo`.
- "Tell, don't ask": tell the object what to do instead of asking for its data and deciding outside.
- Do not generate getters and setters for every field by reflex.

**Show**
```java
// Ask (bad):  if (a.getBalance() >= 50) a.setBalance(a.getBalance() - 50);
// Tell (good): a.withdraw(50);
```

**Check:** Why is `setBalance` risky? *(It bypasses the rules inside deposit and withdraw.)*

---

## BEG-021-L05 · Immutable objects (9 min)
**Goal:** build a class whose objects never change.

**Key points**
- Immutable = once created, state cannot change. `String` is an example.
- Recipe: `final` class, `private final` fields, no setters, set everything in the constructor.
- Methods that "change" return a new object.
- If a field holds something mutable (a `List`, an array), copy it on the way in and on the way out (defensive copy).
- Immutable objects are safe to share and easy to reason about.

**Show**
```java
public final class Money {
    private final long cents;
    public Money(long cents) { this.cents = cents; }
    public Money plus(Money other) { return new Money(cents + other.cents); }
}
```

**Check:** Why copy a mutable list in the constructor? *(Otherwise the caller keeps a reference and can change your "immutable" state.)*

---

## BEG-021-L06 · Demo: protecting the balance invariant (8 min)
**Goal:** lock down `Account` step by step. Prepares `BEG-021-LAB1`.

**Steps**
1. Start from Bank Accounts v1; show `acc.balance = -1000;` working from `main`.
2. Make all fields `private`; the line no longer compiles.
3. Add a getter for `balance` only; keep `owner` and `number` read-only.
4. Enforce the rules in `deposit` and `withdraw` with exceptions; check the constructor too.
5. **Planned mistake:** add a generated `setBalance` and show it breaks the rule again. Remove it.
6. Introduce an immutable `Money` class and use it for amounts.
