# BEG-036 · Stream API — Lecture scripts

**Video:** 71 min · **Analogy used throughout:** a factory conveyor belt: items move past stations that filter, change, and pack them.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-036-L01 · Streams vs loops (8 min)
**Goal:** see what a stream is and why use one.

**Key points**
- A stream is a pipeline of operations over data. It does not store data and does not change the source.
- Three parts: a source (`list.stream()`), intermediate operations, one terminal operation.
- A loop says how; a stream says what.
- A stream can be used once only.
- Streams are a tool, not a replacement for every loop.

**Show**
```java
List<String> longNames = names.stream()
    .filter(n -> n.length() > 3)
    .map(String::toUpperCase)
    .toList();
```

**Check:** Can you reuse a stream after the terminal operation? *(No.)*

---

## BEG-036-L02 · Intermediate operations (12 min)
**Goal:** shape the data in the pipeline.

**Key points**
- `filter(predicate)`: keep matching items.
- `map(function)`: change each item.
- `sorted()` or `sorted(comparator)`: order items.
- `distinct()`: remove duplicates.
- `limit(n)` and `skip(n)`: take or skip items.
- Each returns a new stream, so you chain them.
- Do not put side effects (changing outside variables) in `map`.

**Show**
```java
List<Integer> top3 = nums.stream()
    .distinct().sorted(Comparator.reverseOrder()).limit(3).toList();
```

**Check:** Which operation removes duplicates? *(`distinct`.)*

---

## BEG-036-L03 · Terminal operations and laziness (10 min)
**Goal:** finish a pipeline and understand when work happens.

**Key points**
- Nothing runs until a terminal operation is called. That is laziness.
- `collect(...)` or `toList()` gather results.
- `count()`, `reduce(...)` (combine into one value), `anyMatch`, `allMatch`, `noneMatch`.
- `findFirst()` returns an `Optional` (explained in BEG-037).
- Short-circuiting: `findFirst`, `anyMatch`, and `limit` stop early.

**Show**
```java
int sum = nums.stream().reduce(0, Integer::sum);
boolean hasNeg = nums.stream().anyMatch(n -> n < 0);
long evens = nums.stream().filter(n -> n % 2 == 0).count();
```

**Check:** What happens if a pipeline has no terminal operation? *(Nothing runs.)*

---

## BEG-036-L04 · `flatMap` (8 min)
**Goal:** flatten nested collections.

**Key points**
- `map` turns one item into one item.
- `flatMap` turns one item into a stream of many and joins them into one stream.
- Use it for a list of lists, or each order having many items.
- The function you give must return a stream.

**Show**
```java
List<String> allItems = orders.stream()
    .flatMap(o -> o.getItems().stream())
    .toList();
```

**Check:** You have `List<List<String>>` and want one flat stream of strings. Which operation? *(`flatMap`.)*

---

## BEG-036-L05 · Collectors and grouping (12 min)
**Goal:** group and total data.

**Key points**
- `Collectors.toList()`, `toSet()`, `joining(", ")` gather results.
- `groupingBy(classifier)` returns a `Map` from key to list.
- A second argument, the downstream collector, aggregates each group: `counting()`, `summingDouble(...)`, `averagingDouble(...)`.
- It works like SQL `GROUP BY`.

**Show**
```java
Map<String, Long> countByCity = people.stream()
    .collect(Collectors.groupingBy(Person::getCity, Collectors.counting()));
Map<String, Double> revenue = orders.stream()
    .collect(Collectors.groupingBy(Order::getCategory,
             Collectors.summingDouble(Order::getTotal)));
```

**Check:** Which collector counts items in each group? *(`Collectors.counting()`.)*

---

## BEG-036-L06 · When not to use a stream (5 min)
**Goal:** keep code readable.

**Key points**
- Prefer a loop when you need to change local state, use many steps with early `break`, or throw checked exceptions.
- Do not write 15-step chains; split into named steps or methods.
- Do not use streams for tiny two-line jobs when a loop is clearer.
- Test: could a teammate read it quickly?

**Show:** one pipeline that is hard to read, next to the same loop that is easy.

**Check:** Name one situation where a loop is clearer. *(Many steps, state changes, or early exit.)*

---

## BEG-036-L07 · Demo: building the sales report pipeline (8 min)
**Goal:** compute a report with streams. Prepares `BEG-036-LAB1`.

**Steps**
1. Create an `Order` record with customer, category, amount, and date.
2. Revenue by category with `groupingBy` and `summingDouble`.
3. Top 3 customers: group by customer, sum, sort the entries, `limit(3)`.
4. **Planned mistake:** call `.stream()` once into a variable and use it twice; Java throws `IllegalStateException`. Fix by creating a new stream each time.
5. Print each result with a clear heading.

---

## BEG-036-L08 · Demo: rewriting an unreadable stream as a loop (8 min)
**Goal:** know when to step back. Prepares exercise `BEG-036-EX06`.

**Steps**
1. Show a long chain with nested lambdas and a side effect inside `map`.
2. Explain why it is hard to read and debug.
3. Rewrite it as a plain loop with named variables.
4. **Planned mistake:** keep the side effect in a stream "because it works"; show it breaking when order or parallelism changes (explain only). Fix by moving it to the loop.
5. Compare both versions for readability.
