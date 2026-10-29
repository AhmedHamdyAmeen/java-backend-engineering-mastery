# BEG-037 · Optional — Lecture scripts

**Video:** 33 min · **Analogy used throughout:** a gift box that may or may not contain a gift; you check before you use it.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-037-L01 · The billion-dollar mistake: null (8 min)
**Goal:** see why `null` is dangerous.

**Key points**
- `null` means "no object". Using it throws `NullPointerException`.
- Nothing in a method signature warns that the result may be `null`.
- The inventor of null references called it a "billion-dollar mistake" because of the bugs it causes.
- Callers forget the check and the program crashes later.
- `Optional<T>` makes "might be empty" visible in the type.

**Show**
```java
String name = findName(id);      // may be null
System.out.println(name.length()); // NullPointerException
```

**Check:** What does Java throw when you call a method on `null`? *(`NullPointerException`.)*

---

## BEG-037-L02 · Using Optional well (10 min)
**Goal:** return and unwrap an `Optional`.

**Key points**
- Return `Optional<T>` from a method that may find nothing: `Optional.of(x)`, `Optional.empty()`, `Optional.ofNullable(x)`.
- `isPresent()` and `ifPresent(...)` check and act.
- `map` transforms the inside; `filter` keeps it only if it matches.
- Unwrap with `orElse(default)`, `orElseGet(supplier)` (computes the default only if needed), or `orElseThrow(...)`.
- Avoid a bare `get()`: it throws if empty.

**Show**
```java
Optional<Contact> found = repo.findById(5);
String name = found.map(Contact::getName).orElse("unknown");
Contact c = found.orElseThrow(() -> new NoSuchElementException("No contact 5"));
```

**Check:** Which method computes the default only when the value is missing? *(`orElseGet`.)*

---

## BEG-037-L03 · Optional anti-patterns (7 min)
**Goal:** know where not to use it.

**Key points**
- Not for fields in classes.
- Not for method parameters; use overloads or a plain value.
- Not for collections: return an empty list, not `Optional<List<T>>`.
- Never `optional.get()` without checking.
- Do not write `if (opt.isPresent()) return opt.get();` when `map` or `orElse` is shorter.
- Never assign `null` to an `Optional` variable.

**Show:** a table of "do" and "don't" lines.

**Check:** What should a method return instead of `Optional<List<String>>`? *(An empty list.)*

---

## BEG-037-L04 · Demo: making `findById` return Optional (8 min)
**Goal:** convert a lookup. Prepares `BEG-037-LAB1`.

**Steps**
1. Start with `Contact findById(int id)` returning `null` when missing.
2. Change it to `Optional<Contact>` using `Optional.ofNullable(map.get(id))`.
3. Update callers to use `orElseThrow` or `map(...).orElse(...)`.
4. **Planned mistake:** a caller uses `findById(9).get()` on a missing id and gets `NoSuchElementException`; fix with `orElseThrow` and a helpful message.
5. Run the missing-id case and read the message.
