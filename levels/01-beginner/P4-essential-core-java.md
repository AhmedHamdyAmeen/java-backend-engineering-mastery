# BEG-P4 — Essential Core Java

**Phase goal:** the learner uses the standard library productively — exceptions, collections, generics, time, files, and functional-style streams — and has a correct mental model of references and memory.

**Phase practice:** a *Contacts & Events* console app built across the phase, persisting to a text file and querying with streams.

**Phase total:** ~8.9 h video · ~28.5 h practice

---

### BEG-029 · Exceptions
`n: 29` · **Video:** 71 min · **Practice:** 4 h

**Prerequisites:** BEG-022

**Learning outcomes** — the learner can:
1. Distinguish checked exceptions, unchecked exceptions, and errors, and explain the hierarchy.
2. Handle exceptions with `try`/`catch`/`finally` and multi-catch, catching the narrowest useful type.
3. Throw exceptions with meaningful messages and declare them with `throws`.
4. Create a custom exception for a business rule violation.
5. Release resources with try-with-resources.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-029-L01 | What goes wrong at runtime | 8 |
| BEG-029-L02 | The exception hierarchy | 10 |
| BEG-029-L03 | `try`, `catch`, `finally` | 10 |
| BEG-029-L04 | Throwing and declaring | 8 |
| BEG-029-L05 | Custom exceptions | 9 |
| BEG-029-L06 | try-with-resources | 10 |
| BEG-029-L07 | Demo: InsufficientFundsException end to end | 8 |
| BEG-029-L08 | Demo: finding a swallowed exception | 8 |

**Lab** — `BEG-029-LAB1` *Bank with rules:* `InsufficientFundsException` on overdraw; input parsing with retry on `NumberFormatException`. Acceptance: no empty catch blocks; messages helpful to the user.

**Common mistakes:** `catch (Exception e) {}`; using exceptions for normal control flow; losing the original cause.

**Assessment:** 5 exercises plus a "fix the swallowed exception" review.

**Career relevance:** API error handling (JNR-015) and transaction rollback rules (JNR-031).

---

### BEG-030 · Collections
`n: 30` · **Video:** 81 min · **Practice:** 5 h

**Prerequisites:** BEG-024, BEG-026 · **Co-requisite:** BEG-031 (type parameters are used informally here, explained there)

**Learning outcomes** — the learner can:
1. Use `List`, `Set`, `Map`, and `Queue` and choose the right one for a task.
2. Choose between `ArrayList`/`LinkedList`, `HashSet`/`TreeSet`, `HashMap`/`TreeMap` based on ordering and access needs.
3. Iterate safely, including removing elements during iteration.
4. Declare variables by interface type (`List<String> x = new ArrayList<>()`).

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-030-L01 | Beyond arrays: the Collections Framework | 8 |
| BEG-030-L02 | Lists | 12 |
| BEG-030-L03 | Sets | 10 |
| BEG-030-L04 | Maps | 15 |
| BEG-030-L05 | Queues and deques | 8 |
| BEG-030-L06 | Choosing a collection: decision chart | 7 |
| BEG-030-L07 | Iteration and `ConcurrentModificationException` | 5 |
| BEG-030-L08 | Demo: word frequency with Map | 8 |
| BEG-030-L09 | Demo: the wrong collection, measured | 8 |

**Lab** — `BEG-030-LAB1` *Word frequency:* read a paragraph, count word frequencies with a `Map`, list unique words alphabetically, show the top 10. Acceptance: correct counts; justified collection choices.

**Common mistakes:** `List` where a `Set` or `Map` is needed (O(n) lookups); modifying a list while iterating.

**Assessment:** 6 exercises plus a collection-choice quiz.

**Career relevance:** used in every Java program; internals in BEG-040/041.

---

### BEG-031 · Generics
`n: 31` · **Video:** 48 min · **Practice:** 3 h

**Prerequisites:** BEG-030

**Learning outcomes** — the learner can:
1. Explain why generics exist (type safety without casts).
2. Write a generic class (`Box<T>`, `Pair<A, B>`) and a generic method.
3. Read signatures with bounded types and wildcards (`<T extends Comparable<T>>`, `List<? extends Number>`).

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-031-L01 | Life before generics | 7 |
| BEG-031-L02 | Generic classes | 10 |
| BEG-031-L03 | Generic methods | 8 |
| BEG-031-L04 | Bounded types | 8 |
| BEG-031-L05 | Wildcards: reading the JDK's signatures | 7 |
| BEG-031-L06 | Demo: building a generic in-memory repository | 8 |

**Lab** — `BEG-031-LAB1` *Generic repository:* `InMemoryRepository<T, ID>` with save, findById, findAll, delete; use it for two types. Acceptance: no casts; compile-time type safety demonstrated.

**Common mistakes:** raw types; trying `new T()`.

**Assessment:** 4 exercises.

**Career relevance:** Spring Data's `JpaRepository<T, ID>` (JNR-029) is exactly this pattern.

---

### BEG-032 · Sorting and comparison
`n: 32` · **Video:** 38 min · **Practice:** 2 h

**Prerequisites:** BEG-024, BEG-030

**Learning outcomes** — the learner can:
1. Implement `Comparable` for a natural ordering.
2. Build `Comparator`s, including multi-key ones with `comparing` and `thenComparing`.
3. Sort lists and use sorted collections (`TreeMap`, `TreeSet`) with custom ordering.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-032-L01 | Natural ordering with Comparable | 10 |
| BEG-032-L02 | Comparators | 10 |
| BEG-032-L03 | Multi-key sorting | 10 |
| BEG-032-L04 | Demo: a leaderboard with multi-key comparators | 8 |

**Lab** — `BEG-032-LAB1` *Leaderboard:* sort players by score desc, then name asc; show top N. Acceptance: ties ordered correctly.

**Common mistakes:** subtraction-based compare (overflow); ordering inconsistent with `equals`.

**Assessment:** 3 exercises.

**Career relevance:** sorting in APIs (JNR-019) and SQL `ORDER BY` (BEG-050).

---

### BEG-033 · Date and time
`n: 33` · **Video:** 48 min · **Practice:** 2 h

**Prerequisites:** BEG-020

**Learning outcomes** — the learner can:
1. Choose between `LocalDate`, `LocalDateTime`, `Instant`, and `ZonedDateTime` for a requirement.
2. Do date arithmetic with `Duration` and `Period`.
3. Parse and format dates with `DateTimeFormatter`.
4. Explain why timestamps should be stored in UTC and converted for display.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-033-L01 | Why time is hard | 8 |
| BEG-033-L02 | Local dates and times | 10 |
| BEG-033-L03 | Instants and time zones | 12 |
| BEG-033-L04 | Durations, periods, formatting | 10 |
| BEG-033-L05 | Demo: a meeting across time zones and a daylight-saving change | 8 |

**Lab** — `BEG-033-LAB1` *Meeting planner:* schedule a meeting in one time zone and show it in three others; compute days until a deadline. Acceptance: correct across a daylight-saving change.

**Common mistakes:** `LocalDateTime` for events in multiple time zones; legacy `Date`.

**Assessment:** 3 exercises.

**Career relevance:** timestamps in databases (JNR-028) and distributed clocks (MID-023).

---

### BEG-034 · Files and I/O
`n: 34` · **Video:** 53 min · **Practice:** 3 h

**Prerequisites:** BEG-006, BEG-029

**Learning outcomes** — the learner can:
1. Build and resolve paths with `Path` and check existence with `Files`.
2. Read and write text files with `Files.readAllLines`, `Files.writeString`, and buffered readers/writers.
3. Explain the difference between byte streams and character streams and when encoding matters.
4. Handle I/O errors and always close resources.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-034-L01 | Paths and the Files API | 10 |
| BEG-034-L02 | Reading and writing text | 12 |
| BEG-034-L03 | Streams, readers, and buffering | 12 |
| BEG-034-L04 | Character encoding (UTF-8) | 6 |
| BEG-034-L05 | A simple CSV format | 5 |
| BEG-034-L06 | Demo: saving and loading contacts as CSV | 8 |

**Lab** — `BEG-034-LAB1` *Contacts persistence:* save contacts to CSV on exit and load on start; survive a missing or corrupt file. Acceptance: data survives restarts; bad lines reported, not fatal.

**Common mistakes:** hard-coded absolute paths; platform-default encoding; unclosed files.

**Assessment:** 3 exercises.

**Career relevance:** file uploads (JNR-023) and logs (JNR-006).

---

### BEG-035 · Functional basics
`n: 35` · **Video:** 48 min · **Practice:** 2.5 h

**Prerequisites:** BEG-024

**Learning outcomes** — the learner can:
1. Write lambda expressions and explain them as implementations of a functional interface.
2. Use `Predicate`, `Function`, `Consumer`, `Supplier`, and `BiFunction`.
3. Replace lambdas with method references where clearer.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-035-L01 | Passing behavior as a value | 10 |
| BEG-035-L02 | Lambda syntax | 10 |
| BEG-035-L03 | The standard functional interfaces | 12 |
| BEG-035-L04 | Method references | 8 |
| BEG-035-L05 | Demo: replacing anonymous classes with lambdas | 8 |

**Lab** — `BEG-035-LAB1` *Filters:* rewrite anonymous `Comparator` classes and custom filter loops using lambdas and method references. Acceptance: same behavior, less code.

**Common mistakes:** multi-line lambdas that should be methods; modifying captured variables.

**Assessment:** 4 exercises.

**Career relevance:** streams (BEG-036), `CompletableFuture` (MID-006), Spring configuration.

---

### BEG-036 · Stream API
`n: 36` · **Video:** 71 min · **Practice:** 4 h

**Prerequisites:** BEG-030, BEG-035

**Learning outcomes** — the learner can:
1. Build pipelines with `filter`, `map`, `flatMap`, `sorted`, `distinct`, and `limit`.
2. Terminate streams with `collect`, `reduce`, `count`, `anyMatch`, and `findFirst`.
3. Group and aggregate with `Collectors.groupingBy`, `counting`, and `summingDouble`.
4. Decide when a plain loop is clearer than a stream.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-036-L01 | Streams vs loops | 8 |
| BEG-036-L02 | Intermediate operations | 12 |
| BEG-036-L03 | Terminal operations and laziness | 10 |
| BEG-036-L04 | `flatMap` | 8 |
| BEG-036-L05 | Collectors and grouping | 12 |
| BEG-036-L06 | When not to use a stream | 5 |
| BEG-036-L07 | Demo: building the sales report pipeline | 8 |
| BEG-036-L08 | Demo: rewriting an unreadable stream as a loop | 8 |

**Lab** — `BEG-036-LAB1` *Sales report:* from a list of orders, compute revenue by category, top customers, and average order value per month. Acceptance: correct results, readable pipelines.

**Common mistakes:** side effects inside `map`; reusing a consumed stream; unreadable 15-step chains.

**Assessment:** 6 exercises.

**Career relevance:** everyday Java; analogous to SQL `GROUP BY` (BEG-050).

---

### BEG-037 · Optional
`n: 37` · **Video:** 33 min · **Practice:** 1.5 h

**Prerequisites:** BEG-035

**Learning outcomes** — the learner can:
1. Return `Optional` from a method that may not find a result.
2. Transform and unwrap with `map`, `filter`, `orElse`, `orElseGet`, `orElseThrow`.
3. State where `Optional` should not be used (fields, parameters, collections).

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-037-L01 | The billion-dollar mistake: null | 8 |
| BEG-037-L02 | Using Optional well | 10 |
| BEG-037-L03 | Optional anti-patterns | 7 |
| BEG-037-L04 | Demo: making `findById` return Optional | 8 |

**Lab** — `BEG-037-LAB1` *Safe lookups:* change `findById` in the generic repository to return `Optional` and update callers. Acceptance: no `.get()` without a check.

**Common mistakes:** `optional.get()` unconditionally; `Optional` fields.

**Assessment:** 3 exercises.

**Career relevance:** Spring Data return types (JNR-029).

---

### BEG-038 · Java memory basics
`n: 38` · **Video:** 43 min · **Practice:** 1.5 h

**Prerequisites:** BEG-014, BEG-020

**Learning outcomes** — the learner can:
1. Draw the stack and heap for a short program, showing frames, local variables, and objects.
2. Explain why two variables can refer to the same object and what that implies for mutation.
3. Explain at a high level when an object becomes eligible for garbage collection.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-038-L01 | Stack and heap: a picture | 12 |
| BEG-038-L02 | References and aliasing | 10 |
| BEG-038-L03 | Garbage collection, gently | 8 |
| BEG-038-L04 | `OutOfMemoryError` and `StackOverflowError` | 5 |
| BEG-038-L05 | Demo: drawing stack and heap, then checking in the debugger | 8 |

**Lab** — `BEG-038-LAB1` *Draw it:* draw memory diagrams for four programs, then confirm with the debugger. Acceptance: diagrams match observed values.

**Common mistakes:** thinking objects are copied on assignment; believing `System.gc()` frees memory on demand.

**Assessment:** diagram quiz.

**Career relevance:** JVM memory management (MID-002) and leak diagnosis (MID-008).
