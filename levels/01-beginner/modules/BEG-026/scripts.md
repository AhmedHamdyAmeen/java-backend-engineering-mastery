# BEG-026 · Java object model — Lecture scripts

**Video:** 53 min · **Analogy used throughout:** two banknotes: same serial number means the very same note (identity); same value means equal money (equality).
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-026-L01 · The `Object` class (8 min)
**Goal:** know the class every object inherits from.

**Key points**
- Every class extends `Object`, directly or indirectly, even if you write no `extends`.
- So every object has `toString()`, `equals(Object)`, and `hashCode()`.
- Also `getClass()` (the object's runtime class); `wait`/`notify` come much later.
- The default versions are generic: identity-based `equals`, a cryptic `toString`.
- Override them when your class has a meaningful value or description.

**Show**
```java
Account a = new Account("Ana", "A-1");
System.out.println(a);   // Account@1b6d3586  (default toString)
```

**Check:** What class does `Account` extend if you write no `extends`? *(`Object`.)*

---

## BEG-026-L02 · Identity vs equality (10 min)
**Goal:** tell `==` from `equals` and fix string bugs.

**Key points**
- `==` on objects asks: are these the very same object in memory (identity)?
- `equals` asks: do they have the same value (equality), if the class defines it.
- Default `Object.equals` behaves like `==`.
- `String` overrides `equals`, so compare text with `.equals`, never `==`.
- `==` on strings can seem to work (string literals are shared) and then fail with strings built at run time.

**Show**
```java
String a = "bank";
String b = new String("bank");
System.out.println(a == b);       // false
System.out.println(a.equals(b));  // true
```

**Check:** Which operator compares string content? *(`equals`.)*

---

## BEG-026-L03 · The `equals`/`hashCode` contract (15 min)
**Goal:** implement both methods correctly together.

**Key points**
- `equals` must be reflexive, symmetric, transitive, consistent, and false for `null`.
- If two objects are equal, they **must** have the same `hashCode`. Unequal objects may share a hash, but fewer clashes is better.
- Hash-based collections (`HashSet`, `HashMap`) use `hashCode` first to find the bucket, then `equals`.
- Break the contract and a set can hold "duplicates" or fail to find an element.
- Use the same fields in both; do not use fields that change after the object is stored. Use `Objects.equals` and `Objects.hash`.

**Show**
```java
@Override public boolean equals(Object o) {
    if (this == o) return true;
    if (!(o instanceof Money m)) return false;
    return cents == m.cents && currency.equals(m.currency);
}
@Override public int hashCode() { return Objects.hash(cents, currency); }
```

**Check:** If `a.equals(b)` is true, what must be true of their hash codes? *(They must be equal.)*

---

## BEG-026-L04 · `toString` (5 min)
**Goal:** make objects readable in logs.

**Key points**
- `toString()` returns a text description; print and logging call it automatically.
- Include the class name and the key fields.
- Never include secrets (passwords, full card numbers).
- Keep it short and without side effects.
- IDEs can generate it, but check what it exposes.

**Show**
```java
@Override public String toString() { return "Account[" + number + ", balance=" + balance + "]"; }
```

**Check:** Should `toString` print a password? *(No.)*

---

## BEG-026-L05 · Records as a preview: equality for free (7 min)
**Goal:** see how modern Java removes the boilerplate (preview only; records are taught later).

**Key points**
- A `record` declares an immutable data carrier in one line.
- The compiler generates the constructor, accessors, `equals`, `hashCode`, and `toString` from the fields.
- Two records with the same values are equal.
- Good for value-like types such as `Money`.
- Check the Java version before recording; records are standard in current LTS releases.

**Show**
```java
record Money(long cents, String currency) { }
new Money(100, "SAR").equals(new Money(100, "SAR"));  // true
```

**Check:** What does a record generate for you? *(Constructor, accessors, `equals`, `hashCode`, `toString`.)*

---

## BEG-026-L06 · Demo: the broken HashSet and the equals/hashCode fix (8 min)
**Goal:** observe duplicates and repair them. Prepares `BEG-026-LAB1`.

**Steps**
1. Create `Money` with `cents` and `currency`, no overrides.
2. Add `new Money(100, "SAR")` twice to a `HashSet<Money>`; the size is 2.
3. Override only `equals`; the set often still has 2 (different hash codes).
4. **Planned mistake:** that half-fix; explain that the set never calls `equals` because the buckets differ.
5. Add `hashCode` with `Objects.hash(cents, currency)`; the size is 1.
6. Add `toString` to make the output readable.
