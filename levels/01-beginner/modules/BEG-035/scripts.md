# BEG-035 · Functional basics — Lecture scripts

**Video:** 48 min · **Analogy used throughout:** handing someone a recipe card instead of cooking the dish yourself.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-035-L01 · Passing behavior as a value (10 min)
**Goal:** understand that code can be passed around like data.

**Key points**
- Until now we passed values. Sometimes we want to pass an action: "sort by name", "keep only adults".
- Old way: an anonymous class, which is long and noisy.
- New way: a lambda, a short piece of behavior.
- A functional interface is an interface with exactly one abstract method. A lambda is an implementation of it.
- `Comparator` and `Runnable` are functional interfaces.

**Show**
```java
Comparator<String> byLength = new Comparator<>() {
    public int compare(String a, String b) { return a.length() - b.length(); }
};
Comparator<String> short2 = (a, b) -> Integer.compare(a.length(), b.length());
```

**Check:** What is a functional interface? *(An interface with one abstract method.)*

---

## BEG-035-L02 · Lambda syntax (10 min)
**Goal:** write lambdas correctly.

**Key points**
- Shape: `(parameters) -> body`.
- One parameter: parentheses optional: `n -> n * 2`.
- Types are inferred from context.
- Block body uses braces and `return`: `(a, b) -> { return a + b; }`.
- A lambda can use outside variables only if they are never changed after being set (effectively final).
- If a lambda needs many lines, make it a normal method.

**Show**
```java
Runnable r = () -> System.out.println("hi");
Comparator<Integer> c = (a, b) -> Integer.compare(a, b);
```

**Check:** Can a lambda change a local variable from outside it? *(No; captured variables must be effectively final.)*

---

## BEG-035-L03 · The standard functional interfaces (12 min)
**Goal:** know the five everyday ones.

**Key points**
- `Predicate<T>`: T in, `boolean` out. Method `test`.
- `Function<T, R>`: T in, R out. Method `apply`.
- `Consumer<T>`: T in, nothing out. Method `accept`.
- `Supplier<T>`: nothing in, T out. Method `get`.
- `BiFunction<T, U, R>`: two in, one out. Method `apply`.
- They live in `java.util.function`; no need to write your own for simple cases.

**Show**
```java
Predicate<String> empty = s -> s.isEmpty();
Function<String, Integer> len = s -> s.length();
Consumer<String> print = s -> System.out.println(s);
Supplier<Double> rnd = () -> Math.random();
BiFunction<Integer, Integer, Integer> add = (a, b) -> a + b;
```

**Check:** Which interface takes a value and returns `boolean`? *(`Predicate`.)*

---

## BEG-035-L04 · Method references (8 min)
**Goal:** shorten a lambda that only calls one method.

**Key points**
- `s -> s.length()` can be written `String::length`.
- `s -> System.out.println(s)` becomes `System.out::println`.
- Four forms: `Class::staticMethod`, `object::method`, `Class::instanceMethod`, `Class::new`.
- Use them when they read clearer; keep the lambda when it does more.

**Show**
```java
names.forEach(System.out::println);
names.sort(String::compareToIgnoreCase);
Supplier<List<String>> make = ArrayList::new;
```

**Check:** Rewrite `x -> Integer.parseInt(x)`. *(`Integer::parseInt`.)*

---

## BEG-035-L05 · Demo: replacing anonymous classes with lambdas (8 min)
**Goal:** shrink noisy code. Prepares `BEG-035-LAB1`.

**Steps**
1. Start with an anonymous `Comparator<Contact>` sorting by name.
2. Replace it with a lambda, then with `Comparator.comparing(Contact::getName)`.
3. Replace a loop that keeps adults with a `Predicate<Person>` passed to a method.
4. **Planned mistake:** change a local `count` inside a lambda; the compiler says it must be effectively final. Fix with an `AtomicInteger` or restructure.
5. Compare line counts before and after.
