# JNR-001 · Modern Java — Lecture scripts

**Video:** 80 min · **Analogy used throughout:** a sealed, labeled shipping crate: you cannot change what is inside, and the label lists every kind of crate that exists.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## JNR-001-L01 · Java's release model and LTS versions (8 min)
**Goal:** choose a Java version for production with a clear reason.

**Key points**
- A new Java version comes out every six months (March and September).
- Most versions get support for only about six months.
- An LTS (long-term support) version gets years of updates. LTS releases come every two years.
- Companies run LTS versions in production, because upgrades are less frequent and safer.
- Preview features are early drafts: they may change, so do not use them in production code.

**Show:** a timeline with the release dates and the LTS versions marked (verify version before recording).

**Check:** Why do most teams pick an LTS version? *(It is supported and patched for years, so upgrades are rarer.)*

---

## JNR-001-L02 · Records (12 min)
**Goal:** replace a boilerplate data class with a record.

**Key points**
- A record is a short way to write an immutable data class.
- Java generates the constructor, getters (like `name()`), `equals`, `hashCode`, and `toString`.
- A compact constructor has no parameter list. Use it to validate the values.
- Records are shallow: if a component is a mutable list, copy it with `List.copyOf`.
- Records cannot have setters or extra instance fields.

**Show**
```java
public record Money(long cents, String currency) {
    public Money {
        if (cents < 0) throw new IllegalArgumentException("negative");
        currency = currency.toUpperCase();
    }
}
```

**Check:** What does a compact constructor do? *(It runs checks or cleans values before the fields are set.)*

---

## JNR-001-L03 · Sealed classes and interfaces (10 min)
**Goal:** model a closed set of types.

**Key points**
- `sealed` lists exactly which classes may implement an interface.
- Like a crate label: no other kind of crate can exist.
- Use `permits` to name the allowed types.
- Each allowed type must be `final`, `sealed`, or `non-sealed`. Records are final already.
- The compiler now knows every case, which helps `switch`.

**Show**
```java
sealed interface Discount permits Percentage, FixedAmount, BuyXGetY {}
record Percentage(int percent) implements Discount {}
record FixedAmount(Money amount) implements Discount {}
record BuyXGetY(int buy, int free) implements Discount {}
```

**Check:** What does `permits` do? *(It names the only types allowed to implement the sealed interface.)*

---

## JNR-001-L04 · Switch expressions and pattern matching (15 min)
**Goal:** handle every case of a sealed type with a switch.

**Key points**
- A switch expression returns a value and uses `->`, with no fall-through.
- A pattern in a case matches a type and gives it a name: `case Percentage p`.
- On a sealed type, the switch must cover all cases or it will not compile.
- Do not add `default`: it hides the compile error when you add a new type.
- `instanceof` patterns do the same for single checks: `if (o instanceof String s)`.

**Show**
```java
Money apply(Discount d, Money price) {
    return switch (d) {
        case Percentage p  -> price.minusPercent(p.percent());
        case FixedAmount f -> price.minus(f.amount());
        case BuyXGetY b    -> price; // handled per cart line
    };
}
```

**Check:** Why avoid `default` on a sealed switch? *(It stops the compiler from warning you about a new, unhandled type.)*

---

## JNR-001-L05 · Record patterns (10 min)
**Goal:** take a record apart directly in a pattern.

**Key points**
- A record pattern pulls out the components: `case Percentage(int percent)`.
- It works in `switch` and in `instanceof`.
- Patterns can be nested, for example a record inside a record.
- Use it when you only need the parts, not the whole object.
- Stop nesting when the line becomes hard to read.

**Show**
```java
return switch (d) {
    case Percentage(int percent) -> price.minusPercent(percent);
    case FixedAmount(Money amount) -> price.minus(amount);
    case BuyXGetY(int buy, int free) -> price;
};
```

**Check:** What is the benefit of `case Percentage(int percent)` over `case Percentage p`? *(You get the value directly, without calling `p.percent()`.)*

---

## JNR-001-L06 · Text blocks and other small wins (7 min)
**Goal:** write multi-line text clearly and use other small features.

**Key points**
- A text block starts and ends with three quotes.
- It keeps line breaks and removes common indentation. Good for JSON and SQL.
- `var` for local variables when the type is obvious.
- `List.of`, `Map.of`, and `Stream.toList()` give short, immutable collections.
- Helpful `NullPointerException` messages tell you which variable was null.

**Show**
```java
String json = """
    {"sku": "A-1", "price": 1999}
    """;
```

**Check:** What are text blocks best for? *(Multi-line text such as JSON, SQL, or HTML.)*

---

## JNR-001-L07 · What changed since the last LTS (updated per release) (8 min)
**Goal:** know how to read release notes and spot the features that matter.

**Key points**
- Read the release notes for each new version; look for "final", not "preview".
- Check what moved from preview to final since the last LTS.
- Note anything removed or deprecated that your code uses.
- Decide: does the new feature remove code you maintain today?
- This lecture is re-recorded for each new LTS (verify version before recording).

**Show:** a table: feature / version it became final / used in Shop Core? (fill in at recording time).

**Check:** Which features can you use in production? *(Final features, not preview ones.)*

---

## JNR-001-L08 · Demo: modernizing a legacy Java class step by step (10 min)
**Goal:** turn an old getter/setter class into modern Java. Prepares JNR-001-LAB1.

**Steps**
1. Show the legacy `Product` class: fields, getters, setters, `equals`, `hashCode`, `toString`.
2. Run the existing tests so you have a safety net.
3. Replace the class with a record; remove the setters and fix the callers.
4. **Planned mistake:** the class had a `List<String> tags`. Passing a list that the caller changes later breaks immutability. Fix: copy it in the compact constructor with `List.copyOf`.
5. Replace the `if/else instanceof` chain with a sealed interface and a switch.
6. Run the tests again and list what you removed.

**Check:** Why copy the list? *(A record is shallow; a shared list can still be changed from outside.)*
