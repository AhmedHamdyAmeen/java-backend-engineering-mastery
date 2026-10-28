# Level 1 — Beginner: Interview Preparation

The questions most often asked in internship, trainee, and graduate Java interviews, how to answer them, and exactly where in this course you learned and practiced each one.

**How to use this guide**
1. Read the question and answer it **out loud** before reading the answer. Interviews test explanation, not recognition.
2. If you struggle, go back to the module in **Learned in** and redo the lab in **Practiced in**.
3. Prepare the **Show it** line for every question: interviewers trust what you built more than what you say.

> **About "How often":** frequencies reflect commonly reported interview patterns for entry-level Java roles, not measured statistics. Check them against current job posts in your target market — the same exercise you did in `BEG-004-LAB1` — and update this guide when the market moves.

---

## 1. What the market asks for — and where you proved it

Typical entry-level Java job posts list the skills below. The right-hand columns show where this course taught each one and which artifact proves it.

| Skill employers list | Learned in | Proven by |
| --- | --- | --- |
| Core Java and OOP | BEG-019 … BEG-028 | `BEG-028-LAB1` parking garage, `BEG-CAP` domain model |
| Collections and data structures | BEG-030, BEG-040, BEG-041 | `BEG-041-LAB1` your own hash map |
| Problem solving / algorithms | BEG-016, BEG-017, BEG-039, BEG-044 | `BEG-044-LAB1` technique drills |
| Exceptions and clean error handling | BEG-029 | `BEG-029-LAB1`, `BEG-CAP` borrowing rules |
| SQL and relational databases | BEG-049, BEG-050, BEG-051 | `BEG-050-LAB1` 25 library queries |
| JDBC / connecting Java to a database | BEG-055 | `BEG-055-LAB1` BookRepository |
| Unit testing (JUnit) | BEG-045 | `BEG-045-LAB1`, `BEG-CAP` 25+ tests |
| Git and GitHub | BEG-046, BEG-047 | `BEG-047-LAB1` public portfolio |
| HTTP and REST basics | BEG-052, BEG-053 | `BEG-053-LAB1` Postman collection |
| Build tools (Maven) | BEG-054 | `BEG-054-LAB1` Mavenized project |
| Using AI assistants responsibly | BEG-056, BEG-057 | `BEG-057-LAB1`, `AI-USE.md` in `BEG-CAP` |

**Your portfolio at the end of Level 1:** the Library Management System (`BEG-CAP`) on GitHub with a README, tests, and a class diagram, plus the data-structures project. Pin both on your GitHub profile and link them on your CV.

## 2. How entry-level interviews usually run

| Round | What happens | What they check | Prepare with |
| --- | --- | --- | --- |
| CV / phone screen | 15–30 min call | Motivation, basics, communication | Q23, Q24, your project pitch |
| Online coding test | 2–3 problems, 60–90 min | Correct, readable code under time | Q12–Q15, `BEG-044-LAB1` |
| Technical interview | Java, OOP, SQL questions, small live coding | Depth of understanding | Q1–Q11, Q16–Q22 |
| Project / behavioral | Walk through your project | Ownership, learning ability | Q23, Q24 |

---

## 3. Core Java

### Q1 · What is the difference between the JDK, the JRE, and the JVM?
**How often:** Very common · **Round:** Screen, technical

**How to answer:** define each in one sentence, then show how they nest.
- The **JVM** runs bytecode; it is what makes Java "write once, run anywhere".
- The **JRE** is the JVM plus the standard libraries needed to *run* programs.
- The **JDK** is the JRE plus development tools (`javac`, `jar`, debugger) needed to *build* programs.
- Close with the pipeline: `.java` → `javac` → `.class` bytecode → JVM.

**Common trap:** saying the JVM compiles source code. `javac` compiles; the JVM interprets and JIT-compiles bytecode.

**Learned in:** BEG-007
**Practiced in:** `BEG-007-LAB1`
**Show it:** "I compiled and ran my first program from the terminal before using an IDE, so I know what the IDE does for me."

---

### Q2 · What is the difference between `==` and `equals()`? Why must `hashCode()` be overridden with `equals()`?
**How often:** Very common · **Round:** Technical

**How to answer:**
- `==` compares **references** (same object?) for objects, values for primitives.
- `equals()` compares **logical equality**, as defined by the class.
- Contract: equal objects **must** have equal hash codes. Hash-based collections find the bucket with `hashCode()` first, then compare with `equals()`. Break the contract and `HashSet` stores duplicates and `HashMap.get` misses keys.

```java
record Money(long cents, String currency) {}   // records generate a consistent equals/hashCode
new Money(100, "EUR").equals(new Money(100, "EUR"));  // true
new Money(100, "EUR") == new Money(100, "EUR");       // false: two objects
```

**Common trap:** comparing strings with `==`. It sometimes "works" because of string interning, which makes the bug worse.

**Learned in:** BEG-026, BEG-041
**Practiced in:** `BEG-026-LAB1`, `BEG-041-LAB1`
**Show it:** describe the "broken set" lab where missing `hashCode` caused duplicates.

---

### Q3 · Why are Strings immutable, and when do you use `StringBuilder`?
**How often:** Very common · **Round:** Technical

**How to answer:**
- Immutability makes strings safe to share between threads, cache their hash code, use as map keys, and reuse from the string pool.
- Every "modification" creates a new object, so concatenating in a loop creates many temporary strings (O(n²) copying).
- Use `StringBuilder` when building a string in a loop; use plain `+` for a few fixed pieces (the compiler optimizes it).

**Learned in:** BEG-015
**Practiced in:** `BEG-015-LAB1`
**Show it:** the report printing in the student-grade manager.

---

### Q4 · Explain the four pillars of OOP with an example from your own code.
**How often:** Very common · **Round:** Technical

**How to answer:** one sentence and one concrete example from *your* project for each — generic textbook examples (animals, shapes) score lower.
- **Encapsulation:** `Account` keeps `balance` private and only changes it through `deposit`/`withdraw`, which protect the invariant "balance never negative".
- **Inheritance:** `SavingsAccount extends Account` reuses behavior and adds interest.
- **Polymorphism:** month-end processing calls `account.applyMonthEnd()` on a list of mixed accounts without type checks.
- **Abstraction:** the bank depends on a `Notifier` interface, not on email or SMS details.

**Common trap:** describing encapsulation as "getters and setters". It is about protecting invariants.

**Learned in:** BEG-021, BEG-022, BEG-023, BEG-024
**Practiced in:** `BEG-022-LAB1`, `BEG-023-LAB1`, `BEG-028-LAB1`
**Show it:** open your Bank Accounts or parking-garage code and point to each pillar.

---

### Q5 · Abstract class or interface — how do you choose?
**How often:** Very common · **Round:** Technical

**How to answer:**
- **Interface:** a contract that unrelated classes can implement; a class can implement many. Default methods allow limited shared behavior. Prefer it for capabilities (`Notifier`, `Comparable`).
- **Abstract class:** shared *state* and code for closely related classes; single inheritance only. Use it when subclasses truly are variants of one thing and share fields.
- Rule of thumb: start with an interface; introduce an abstract class only when implementations share state.

**Learned in:** BEG-024
**Practiced in:** `BEG-024-LAB1`
**Show it:** the `Notifier` interface with three implementations.

---

### Q6 · What is the difference between overloading and overriding?
**How often:** Common · **Round:** Technical

**How to answer:**
- **Overloading:** same name, different parameter lists, in the same class; chosen at **compile time** from argument types.
- **Overriding:** a subclass replaces an inherited method with the same signature; chosen at **runtime** from the object's actual type (dynamic dispatch).
- Mention `@Override`: it makes the compiler catch accidental overloading.

**Learned in:** BEG-014, BEG-022, BEG-023
**Practiced in:** `BEG-014-LAB1`, `BEG-023-LAB1`

---

### Q7 · Checked vs unchecked exceptions — and what does try-with-resources do?
**How often:** Very common · **Round:** Technical

**How to answer:**
- **Checked** (`IOException`): the compiler forces you to handle or declare them; used for recoverable conditions outside your control.
- **Unchecked** (`RuntimeException` subclasses): programming errors or business-rule violations; not forced by the compiler.
- **try-with-resources** closes any `AutoCloseable` automatically, even when an exception is thrown, and keeps suppressed exceptions.
- Good practice: catch the narrowest type, never swallow exceptions, keep the cause when wrapping.

```java
try (var reader = Files.newBufferedReader(path)) {
    return reader.lines().map(Contact::parse).toList();
} // reader is closed here, exception or not
```

**Learned in:** BEG-029, BEG-034
**Practiced in:** `BEG-029-LAB1`, `BEG-034-LAB1`
**Show it:** your `InsufficientFundsException` or the capstone's borrowing-rule exceptions.

---

### Q8 · `ArrayList` vs `LinkedList` — which would you use and why?
**How often:** Very common · **Round:** Technical

**How to answer:**
- `ArrayList`: backed by an array; O(1) index access, amortized O(1) append, O(n) insert/remove in the middle; cache-friendly.
- `LinkedList`: O(1) insert/remove *at a known node*, but O(n) to find the position and poor memory locality.
- In practice `ArrayList` (or `ArrayDeque` for queues) wins almost always. Say this, and say you measured it.

**Learned in:** BEG-030, BEG-040
**Practiced in:** `BEG-040-LAB1`
**Show it:** "I implemented both, so I can explain where the costs come from."

---

### Q9 · How does a `HashMap` work internally?
**How often:** Very common · **Round:** Technical

**How to answer:** walk through `put` and `get`.
1. Compute `hashCode()` of the key and map it to a bucket index.
2. Store the entry in that bucket; collisions are chained (Java converts long chains to balanced trees).
3. `get` finds the bucket, then compares keys with `equals()`.
4. When size exceeds capacity × load factor (default 0.75), the table doubles and entries are rehashed.
5. Average O(1), worst case degrades when many keys collide — which is why a good `hashCode` matters.

**Common trap:** forgetting that mutating a key after insertion makes the entry unreachable.

**Learned in:** BEG-041
**Practiced in:** `BEG-041-LAB1`
**Show it:** your `MyHashMap` and the constant-`hashCode` slowdown measurement.

---

### Q10 · What lives on the stack and what lives on the heap? What does the garbage collector do?
**How often:** Common · **Round:** Technical

**How to answer:**
- **Stack:** one frame per method call, holding local variables and references; freed automatically when the method returns.
- **Heap:** all objects; shared between threads.
- An object becomes eligible for garbage collection when no live reference chain reaches it. You do not free memory yourself, and `System.gc()` is only a hint.
- Mention the two errors: `StackOverflowError` (too-deep recursion), `OutOfMemoryError` (heap exhausted).

**Learned in:** BEG-038
**Practiced in:** `BEG-038-LAB1`

---

### Q11 · Use the Stream API to group orders by category and sum their totals.
**How often:** Common · **Round:** Technical, live coding

**How to answer:** write it, then explain each step.

```java
Map<String, Double> revenueByCategory = orders.stream()
    .collect(Collectors.groupingBy(Order::category,
             Collectors.summingDouble(Order::total)));
```

- Mention laziness (nothing runs until the terminal operation) and that streams should not have side effects.
- Bonus: say you would use `BigDecimal` for real money, and that a plain loop is fine when it is clearer.

**Learned in:** BEG-035, BEG-036
**Practiced in:** `BEG-036-LAB1`

---

## 4. Coding problems

For every problem: **clarify** inputs and edge cases → state a **brute-force** idea and its complexity → **improve** → **code** → **test** with examples out loud. Interviewers grade the process as much as the result (BEG-016).

### Q12 · Check whether a string is a palindrome (ignoring case and non-letters).
**How often:** Very common · **Round:** Online test, live coding

**How to answer:** two pointers from both ends, skipping non-letters. O(n) time, O(1) extra space.

```java
static boolean isPalindrome(String s) {
    int i = 0, j = s.length() - 1;
    while (i < j) {
        if (!Character.isLetterOrDigit(s.charAt(i))) { i++; continue; }
        if (!Character.isLetterOrDigit(s.charAt(j))) { j--; continue; }
        if (Character.toLowerCase(s.charAt(i)) != Character.toLowerCase(s.charAt(j))) return false;
        i++; j--;
    }
    return true;
}
```

**Edge cases to say out loud:** empty string, one character, only punctuation.

**Learned in:** BEG-015, BEG-044
**Practiced in:** `BEG-044-LAB1`

---

### Q13 · Two Sum: find two numbers in an array that add up to a target.
**How often:** Very common · **Round:** Online test, live coding

**How to answer:**
- Brute force: check every pair, O(n²).
- Better: one pass with a `HashMap` from value to index; for each number, check whether `target - number` was already seen. O(n) time, O(n) space.

```java
static int[] twoSum(int[] nums, int target) {
    Map<Integer, Integer> seen = new HashMap<>();
    for (int i = 0; i < nums.length; i++) {
        Integer j = seen.get(target - nums[i]);
        if (j != null) return new int[] {j, i};
        seen.put(nums[i], i);
    }
    return new int[0];
}
```

**Learned in:** BEG-039, BEG-041
**Practiced in:** `BEG-039-LAB1`

---

### Q14 · Implement binary search. When can't you use it?
**How often:** Common · **Round:** Live coding

**How to answer:** only on **sorted** data; O(log n). Use `low + (high - low) / 2` to avoid integer overflow and be precise about loop bounds.

```java
static int binarySearch(int[] a, int key) {
    int low = 0, high = a.length - 1;
    while (low <= high) {
        int mid = low + (high - low) / 2;
        if (a[mid] < key) low = mid + 1;
        else if (a[mid] > key) high = mid - 1;
        else return mid;
    }
    return -1;
}
```

**Learned in:** BEG-017, BEG-039
**Practiced in:** `BEG-017-LAB1`

---

### Q15 · Find the first non-repeating character in a string.
**How often:** Common · **Round:** Online test

**How to answer:** two passes: count characters (a `LinkedHashMap` or an `int[]` for ASCII), then return the first with count 1. O(n) time.

```java
static Optional<Character> firstUnique(String s) {
    Map<Character, Integer> counts = new LinkedHashMap<>();
    for (char c : s.toCharArray()) counts.merge(c, 1, Integer::sum);
    return counts.entrySet().stream().filter(e -> e.getValue() == 1).map(Map.Entry::getKey).findFirst();
}
```

**Learned in:** BEG-030, BEG-037
**Practiced in:** `BEG-030-LAB1`

---

## 5. SQL and databases

### Q16 · Find the second-highest salary (or: the top earner in each department).
**How often:** Very common · **Round:** Online test, technical

**How to answer:** give a simple version, then handle ties and missing values.

```sql
-- Second-highest distinct salary (NULL if there is none)
SELECT MAX(salary) FROM employee
WHERE salary < (SELECT MAX(salary) FROM employee);

-- Highest salary per department
SELECT department_id, MAX(salary) FROM employee GROUP BY department_id;
```

Mention that window functions (`DENSE_RANK`) solve "top N per group" more generally — you will master them in MID-011.

**Learned in:** BEG-050
**Practiced in:** `BEG-050-LAB1`

---

### Q17 · What is the difference between an INNER JOIN and a LEFT JOIN?
**How often:** Very common · **Round:** Technical

**How to answer:**
- **INNER JOIN** returns only rows with a match on both sides.
- **LEFT JOIN** returns all rows from the left table, with `NULL`s where the right side has no match.
- Give the classic use: "members with no loans" = `LEFT JOIN loan ... WHERE loan.id IS NULL`.
- Trap to mention: a `WHERE` condition on the right table silently turns a LEFT JOIN into an INNER JOIN; put it in the `ON` clause instead.

**Learned in:** BEG-050
**Practiced in:** `BEG-050-LAB1`

---

### Q18 · What are primary and foreign keys, and why normalize a database?
**How often:** Common · **Round:** Technical

**How to answer:**
- **Primary key:** uniquely identifies a row; never null.
- **Foreign key:** references another table's primary key and enforces that the referenced row exists.
- **Normalization** removes duplicated data so each fact lives in one place, which prevents update, insert, and delete anomalies. Explain with your library schema: authors in their own table, a junction table for book–author.

**Learned in:** BEG-049, BEG-051
**Practiced in:** `BEG-049-LAB1`, `BEG-051-LAB1`

---

### Q19 · What is SQL injection and how do you prevent it in Java?
**How often:** Very common · **Round:** Technical

**How to answer:**
- Injection happens when user input is concatenated into SQL, letting the input change the query's structure (`' OR '1'='1`).
- Prevent it with **parameterized queries** (`PreparedStatement` with `?`), which send the query and data separately. Never build SQL with `+` from user input.
- For things that cannot be parameters (e.g., sort column), use an allow-list.

```java
var sql = "SELECT id, title FROM book WHERE title = ?";
try (var ps = connection.prepareStatement(sql)) {
    ps.setString(1, userInput);
    ...
}
```

**Learned in:** BEG-055
**Practiced in:** `BEG-055-LAB1`
**Show it:** "In my course I first exploited my own code with injection, then fixed it."

---

## 6. Web, tools, and workflow

### Q20 · What happens when you type a URL into the browser and press Enter?
**How often:** Very common · **Round:** Screen, technical

**How to answer:** a clear sequence with the right names, at the depth the interviewer wants.
1. The browser parses the URL; DNS resolves the domain to an IP address.
2. It opens a TCP connection (and a TLS handshake for HTTPS).
3. It sends an HTTP request (method, path, headers).
4. The server processes it — often a backend querying a database — and returns a response with a status code and body.
5. The browser renders HTML and makes further requests for CSS, JS, and images.

**Learned in:** BEG-003, BEG-052
**Practiced in:** `BEG-003-LAB1`, `BEG-052-LAB1`

---

### Q21 · Explain GET vs POST and the main HTTP status code families.
**How often:** Very common · **Round:** Technical

**How to answer:**
- **GET** reads data, has no body by convention, is safe and idempotent, and can be cached. **POST** creates or triggers processing and is not idempotent.
- **2xx** success (200, 201 Created, 204 No Content), **3xx** redirection, **4xx** client error (400, 401, 403, 404, 409), **5xx** server error (500, 503).
- Bonus: explain 401 vs 403.

**Learned in:** BEG-052, BEG-053
**Practiced in:** `BEG-052-LAB1`, `BEG-053-LAB1`

---

### Q22 · How do you resolve a Git merge conflict? What is a pull request for?
**How often:** Common · **Round:** Technical, behavioral

**How to answer:**
- A conflict happens when two branches change the same lines. Open the file, read both versions between the markers, decide the correct combined result, remove the markers, run the tests, then `git add` and commit.
- A **pull request** proposes merging a branch so others can review the change, discuss it, and run checks before it reaches `main`.
- Mention small commits with clear messages and never committing secrets or build output.

**Learned in:** BEG-046, BEG-047
**Practiced in:** `BEG-046-LAB1`, `BEG-047-LAB1`

---

## 7. Your project and behavior

### Q23 · Walk me through a project you built.
**How often:** Asked in almost every interview · **Round:** Screen, project

**How to answer (3–4 minutes):**
1. **Problem:** one sentence on what it does and for whom.
2. **Design:** main classes and why responsibilities sit where they do; show the class diagram.
3. **Technical choices:** PostgreSQL via JDBC, parameterized queries, Maven, JUnit — and why.
4. **Hardest part:** a concrete difficulty (e.g., enforcing "no loan if overdue") and how you solved it.
5. **Quality:** how many tests, which rules they cover.
6. **Next:** what you would improve (e.g., a REST API with Spring Boot — Level 2).

**Learned in:** BEG-028, BEG-047
**Practiced in:** `BEG-CAP`
**Show it:** have the repository open; be ready to change something live.

---

### Q24 · Tell me about a bug you found and fixed.
**How often:** Very common · **Round:** Behavioral, technical

**How to answer:** use the debugging method, not a story of luck.
- **Situation:** what was wrong and how you noticed it (failing test, wrong output).
- **Approach:** reproduced it, formed a hypothesis, used breakpoints or a stack trace to find the line.
- **Fix and proof:** the change and the regression test you added.
- **Lesson:** what you do differently now.

**Learned in:** BEG-018, BEG-045
**Practiced in:** `BEG-018-LAB1`, `BEG-045-LAB1`

---

## 8. AI questions

### Q25 · Do you use AI tools like ChatGPT or Copilot when you code? How do you make sure the code is right?
**How often:** Very common · **Round:** Screen, technical

**How to answer:** say yes honestly, then show discipline — interviewers worry about candidates who paste code they cannot explain.
- I try first, then ask the assistant to **explain** an error or concept, not just to write the solution.
- I treat every suggestion as untrusted: I read it line by line, trace it with a small input, and run tests — including edge cases the assistant did not mention.
- I never paste secrets, passwords, or private company code into a public tool.
- Give a concrete example of a suggestion you rejected and why (e.g., it used `==` on strings, or ignored an empty list).

**Common trap:** "I always use AI so I don't need to understand the details." Interviews still test whether you understand the code yourself.

**Learned in:** BEG-056, BEG-057
**Practiced in:** `BEG-056-LAB1`, `BEG-057-LAB1`, `BEG-CAP`
**Show it:** your capstone's `AI-USE.md` with the suggestion you corrected.

---

### Q26 · What is a "hallucination" in an AI assistant, and why does it happen?
**How often:** Common · **Round:** Screen

**How to answer:**
- A language model predicts likely next words from patterns in its training data; it does not look facts up or run your code.
- So it can produce confident, plausible, but wrong answers — invented methods, wrong API names, outdated syntax.
- The defense is verification: compile, run, test, and check the official documentation.

**Learned in:** BEG-056
**Practiced in:** `BEG-056-LAB1`

---

## 9. Four-week preparation plan

| Week | Focus | Do this |
| --- | --- | --- |
| 1 | Core Java and OOP | Answer Q1–Q11 out loud; redo `BEG-026-LAB1` and `BEG-041-LAB1` without notes |
| 2 | Coding problems | 3 problems a day in the style of Q12–Q15, timed; explain each solution aloud |
| 3 | SQL, web, Git | Redo `BEG-050-LAB1` timed; Q16–Q22; read your capstone's SQL and JDBC code |
| 4 | Project and mocks | Rehearse Q23–Q24; two mock interviews with a peer using the Level 1 interview simulation |

**Ready when:** you can answer every question here without notes, solve an unseen easy coding problem in 25 minutes while talking, and change your capstone live in front of someone.
