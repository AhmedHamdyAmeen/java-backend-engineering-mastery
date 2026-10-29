# BEG-031 · Generics — Lecture scripts

**Video:** 48 min · **Analogy used throughout:** labeled storage crates: a crate marked "books" only accepts books.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-031-L01 · Life before generics (7 min)
**Goal:** understand the problem generics solve.

**Key points**
- Old collections held plain `Object`. You had to cast when reading.
- A wrong cast only failed at runtime with `ClassCastException`.
- Generics put the type on the crate: `List<String>` accepts only strings.
- The compiler catches the mistake, and no cast is needed.
- Idea: type safety without casts.

**Show**
```java
List raw = new ArrayList();
raw.add(42);
String s = (String) raw.get(0); // runtime ClassCastException
```

**Check:** When does a wrong cast fail without generics? *(At runtime.)*

---

## BEG-031-L02 · Generic classes (10 min)
**Goal:** write a class with a type parameter.

**Key points**
- `T` is a placeholder for a type, chosen by the user of the class.
- Declare it after the class name: `class Box<T>`.
- `Pair<A, B>` shows two type parameters.
- Use diamond when creating: `new Box<>()`.
- Type arguments must be reference types: `Box<Integer>`, not `Box<int>`.

**Show**
```java
class Box<T> {
    private T value;
    Box(T value) { this.value = value; }
    T get() { return value; }
}
Box<String> b = new Box<>("hi");
String s = b.get(); // no cast
```

**Check:** Can you write `Box<int>`? *(No, use `Box<Integer>`.)*

---

## BEG-031-L03 · Generic methods (8 min)
**Goal:** write a method with its own type parameter.

**Key points**
- Put `<T>` before the return type: `static <T> T first(List<T> list)`.
- The compiler infers `T` from the arguments.
- Useful for utilities that work on many types.
- The method's `T` is independent of any class `T`.

**Show**
```java
static <T> T first(List<T> list) { return list.get(0); }
String s = first(List.of("a", "b"));
```

**Check:** Where does `<T>` go in a generic method? *(Before the return type.)*

---

## BEG-031-L04 · Bounded types (8 min)
**Goal:** limit what a type parameter can be.

**Key points**
- `<T extends Number>` means T must be a `Number` or a subclass.
- The bound lets you call the bound's methods on `T`.
- `<T extends Comparable<T>>` means T can be compared with itself.
- Here `extends` also covers interfaces.

**Show**
```java
static <T extends Comparable<T>> T max(T a, T b) {
    return a.compareTo(b) >= 0 ? a : b;
}
```

**Check:** Why does `max` need `Comparable`? *(To call `compareTo`.)*

---

## BEG-031-L05 · Wildcards: reading the JDK's signatures (7 min)
**Goal:** read signatures with `?`.

**Key points**
- `?` means "some unknown type".
- `List<? extends Number>`: a list of Numbers or subtypes. You can read from it, not add.
- `List<? super Integer>`: you can add Integers.
- Handy memory aid: extends to read (producer), super to write (consumer).
- `List<Integer>` is not a `List<Number>`; wildcards cover that gap.

**Show:** `double sum(List<? extends Number> nums)` accepting `List<Integer>` and `List<Double>`.

**Check:** Can you add to a `List<? extends Number>`? *(No, only read.)*

---

## BEG-031-L06 · Demo: building a generic in-memory repository (8 min)
**Goal:** build `InMemoryRepository<T, ID>`. Prepares `BEG-031-LAB1`.

**Steps**
1. Create `class InMemoryRepository<T, ID>` with a `Map<ID, T>` inside.
2. Add `save(ID id, T item)`, `findById(ID id)`, `findAll()`, `delete(ID id)`.
3. Use it with `<Contact, Integer>` and `<Event, String>`.
4. **Planned mistake:** try `new T()` or use the raw type `InMemoryRepository`; the compiler (or a warning) objects. Fix by passing the item in and using type arguments.
5. Show that saving a wrong type fails at compile time.
