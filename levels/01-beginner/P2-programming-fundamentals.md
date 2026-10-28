# BEG-P2 — Programming Fundamentals with Java

**Phase goal:** the learner writes, traces, and debugs small procedural Java programs and solves simple problems systematically.

**Phase practice:** 40–60 progressive exercises (`BEG-0xx-EXnn`), ending with three mini-projects: command-line calculator, number guessing game, and student-grade manager.

**Phase total:** ~11.2 h video · ~45 h practice

---

### BEG-008 · First Java program
`n: 8` · **Video:** 48 min · **Practice:** 2 h

**Prerequisites:** BEG-007

**Learning outcomes** — the learner can:
1. Identify the parts of a minimal Java program: class declaration, `main` method signature, statements, braces.
2. Print text and simple values with `System.out.println` and `System.out.print`.
3. Write single-line, multi-line, and Javadoc comments, and explain when a comment is useful.
4. Fix the five most common beginner syntax errors from the compiler message alone.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-008-L01 | Anatomy of Hello World | 10 |
| BEG-008-L02 | Statements, semicolons, and blocks | 8 |
| BEG-008-L03 | Printing output | 8 |
| BEG-008-L04 | Comments | 6 |
| BEG-008-L05 | Reading compiler errors | 8 |
| BEG-008-L06 | Demo: fixing five broken programs from compiler messages | 8 |

**Lab** — `BEG-008-LAB1` *Business card:* print a formatted multi-line business card. Then fix five provided broken programs using only the compiler messages. Acceptance: all five compile and print the expected output.

**Common mistakes:** case sensitivity (`system.out`), missing semicolons, mismatched braces, misspelling `main`'s signature.

**Assessment:** 5 exercises (`BEG-008-EX01..05`).

**Career relevance:** reading compiler and tool output is a daily skill at every level.

---

### BEG-009 · Variables and data types
`n: 9` · **Video:** 63 min · **Practice:** 4 h

**Prerequisites:** BEG-008

**Learning outcomes** — the learner can:
1. Declare and initialize variables of each primitive type and of `String`, choosing an appropriate type for given data.
2. Explain the difference between primitive and reference types at a conceptual level.
3. Apply Java naming conventions and use `final` for constants.
4. Perform widening and narrowing conversions and predict data loss, including integer overflow.
5. Use `var` for local variables where the type is obvious.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-009-L01 | Variables as labeled boxes | 8 |
| BEG-009-L02 | The eight primitive types | 12 |
| BEG-009-L03 | Strings and reference types | 8 |
| BEG-009-L04 | Literals, constants, and naming | 8 |
| BEG-009-L05 | Type conversion and casting | 12 |
| BEG-009-L06 | Local type inference with `var` | 7 |
| BEG-009-L07 | Demo: unit converter and an integer overflow | 8 |

**Lab** — `BEG-009-LAB1` *Unit converter (fixed values):* convert hard-coded temperatures, distances, and currencies, printing results with correct types. Include one deliberate overflow and explain it in a comment. Acceptance: correct output; overflow explained.

**Common mistakes:** `int` division where decimals were expected; using `double` for money; `==` on strings (flagged here, explained in BEG-026).

**Assessment:** 6 exercises plus a quiz on type selection.

**Career relevance:** type choice for money returns in JNR-028 (`BigDecimal`/`numeric`) and data modeling.

---

### BEG-010 · Operators
`n: 10` · **Video:** 48 min · **Practice:** 3 h

**Prerequisites:** BEG-009

**Learning outcomes** — the learner can:
1. Evaluate expressions using arithmetic, comparison, logical, and assignment operators.
2. Predict results involving integer division, modulo, and operator precedence.
3. Explain the difference between prefix and postfix increment.
4. Use short-circuit evaluation (`&&`, `||`) to avoid errors.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-010-L01 | Arithmetic operators and integer division | 10 |
| BEG-010-L02 | Comparison and logical operators | 10 |
| BEG-010-L03 | Assignment and compound assignment | 6 |
| BEG-010-L04 | Increment, decrement, and precedence | 8 |
| BEG-010-L05 | Short-circuit evaluation | 6 |
| BEG-010-L06 | Demo: predict-then-run expression challenge | 8 |

**Lab** — `BEG-010-LAB1` *Expression predictor:* predict the output of 20 expressions on paper, then verify in code. Acceptance: predictions recorded before running; each mismatch explained.

**Common mistakes:** `=` vs `==`; `5/2` returning 2; chaining comparisons like `1 < x < 10`.

**Assessment:** 6 exercises.

**Career relevance:** exact reasoning about expressions underpins debugging (BEG-018) and test boundaries (BEG-045).

---

### BEG-011 · Input and output
`n: 11` · **Video:** 48 min · **Practice:** 3 h

**Prerequisites:** BEG-010

**Learning outcomes** — the learner can:
1. Read text and numbers from the console with `Scanner`.
2. Parse strings to numbers and handle input that is not a number (looping until valid, without exceptions yet).
3. Format output with `printf`/`String.format` (width, decimals, alignment).
4. Explain why user input must never be trusted.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-011-L01 | Reading input with Scanner | 10 |
| BEG-011-L02 | The `nextInt` / `nextLine` trap | 8 |
| BEG-011-L03 | Parsing strings into numbers | 8 |
| BEG-011-L04 | Formatting output | 8 |
| BEG-011-L05 | Validating input: never trust the user | 6 |
| BEG-011-L06 | Demo: building the receipt printer with input validation | 8 |

**Lab** — `BEG-011-LAB1` *Receipt printer:* read item names, quantities, and prices; print an aligned receipt with totals and tax. Reject invalid quantities. Acceptance: aligned output; invalid input re-prompted.

**Common mistakes:** skipped input after `nextInt`; crashing on non-numeric input; misaligned columns.

**Assessment:** 5 exercises.

**Career relevance:** input validation is the seed of JNR-014 (Bean Validation) and JNR-041 (injection).

---

### BEG-012 · Conditions
`n: 12` · **Video:** 52 min · **Practice:** 4 h

**Prerequisites:** BEG-010

**Learning outcomes** — the learner can:
1. Write `if`/`else if`/`else` chains that cover every case, including boundaries.
2. Choose between an `if` chain, a `switch` statement, and a switch expression.
3. Simplify nested conditions using logical operators and early exits.
4. Identify unreachable or overlapping branches.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-012-L01 | Making decisions with `if` | 10 |
| BEG-012-L02 | `else if` chains and boundary values | 8 |
| BEG-012-L03 | Classic `switch` and fall-through | 8 |
| BEG-012-L04 | Switch expressions (modern Java) | 8 |
| BEG-012-L05 | Taming nested conditions | 10 |
| BEG-012-L06 | Demo: shipping cost rules and their boundaries | 8 |

**Lab** — `BEG-012-LAB1` *Shipping cost calculator:* compute cost from weight, zone, and membership with clear rules; test every boundary by hand. Acceptance: a table of at least 10 test inputs with expected and actual results.

**Common mistakes:** missing `break` in classic switch; gaps or overlaps at boundaries (`<` vs `<=`); deep nesting.

**Assessment:** 6 exercises.

**Career relevance:** business rules in every service; switch expressions return with sealed types in JNR-001.

---

### BEG-013 · Loops
`n: 13` · **Video:** 58 min · **Practice:** 5 h

**Prerequisites:** BEG-012

**Learning outcomes** — the learner can:
1. Choose `for`, `while`, or `do-while` for a given task and justify the choice.
2. Write loops with correct start, condition, and update, avoiding off-by-one and infinite loops.
3. Use `break` and `continue` appropriately.
4. Write nested loops for grid-style problems and estimate how many times the body runs.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-013-L01 | Why loops: repetition without copy-paste | 6 |
| BEG-013-L02 | The `for` loop | 10 |
| BEG-013-L03 | `while` and `do-while` | 10 |
| BEG-013-L04 | `break`, `continue`, and loop control | 8 |
| BEG-013-L05 | Nested loops | 10 |
| BEG-013-L06 | Off-by-one errors and infinite loops | 6 |
| BEG-013-L07 | Demo: number guessing game, stepping through the loop in the debugger | 8 |

**Lab** — `BEG-013-LAB1` *Number guessing game* (mini-project 1 of 3): random target, limited attempts, higher/lower hints, replay option. Acceptance: handles invalid input, reports attempts, replay works.

**Common mistakes:** off-by-one boundaries; modifying the loop variable in the body; forgetting to update the `while` condition.

**Assessment:** 7 exercises plus the guessing game.

**Career relevance:** iteration cost leads into complexity (BEG-039).

---

### BEG-014 · Methods
`n: 14` · **Video:** 72 min · **Practice:** 5 h

**Prerequisites:** BEG-013

**Learning outcomes** — the learner can:
1. Extract repeated or named logic into a method with clear parameters and a return type.
2. Explain pass-by-value for primitives and for references.
3. Overload methods and explain how Java picks one.
4. Describe the call stack and trace a sequence of method calls.
5. Write a simple recursive method with a correct base case (factorial, sum of digits).

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-014-L01 | Why methods: naming and reuse | 8 |
| BEG-014-L02 | Parameters and return values | 10 |
| BEG-014-L03 | Method signatures and overloading | 8 |
| BEG-014-L04 | Scope: where variables live | 8 |
| BEG-014-L05 | The call stack | 10 |
| BEG-014-L06 | Recursion basics | 12 |
| BEG-014-L07 | Demo: building the calculator one method at a time | 8 |
| BEG-014-L08 | Demo: tracing recursion on the call stack | 8 |

**Lab** — `BEG-014-LAB1` *Command-line calculator* (mini-project 2 of 3): menu-driven calculator where each operation is its own method; includes power and factorial (recursive). Acceptance: no duplicated logic; division by zero handled; recursion has a base case.

**Common mistakes:** methods that both compute and print; missing base case (stack overflow); expecting a method to change a caller's primitive.

**Assessment:** 6 exercises plus the calculator.

**Career relevance:** method design is the unit of clean code (JNR-003) and testing (BEG-045).

---

### BEG-015 · Arrays and strings
`n: 15` · **Video:** 74 min · **Practice:** 5 h

**Prerequisites:** BEG-013, BEG-014

**Learning outcomes** — the learner can:
1. Create, fill, iterate, and copy one- and two-dimensional arrays.
2. Use common `String` methods (length, charAt, substring, indexOf, split, equals, trim, toUpperCase).
3. Explain string immutability and use `StringBuilder` for repeated concatenation.
4. Avoid `ArrayIndexOutOfBoundsException` by reasoning about valid indices.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-015-L01 | Arrays: fixed-size lists | 10 |
| BEG-015-L02 | Iterating and enhanced for | 8 |
| BEG-015-L03 | Two-dimensional arrays | 10 |
| BEG-015-L04 | Working with Strings | 12 |
| BEG-015-L05 | Immutability and StringBuilder | 10 |
| BEG-015-L06 | `Arrays` utility class | 8 |
| BEG-015-L07 | Demo: student-grade manager with arrays | 8 |
| BEG-015-L08 | Demo: string bugs: `==`, off-by-one, and slow concatenation | 8 |

**Lab** — `BEG-015-LAB1` *Student-grade manager* (mini-project 3 of 3): store names and grades in arrays; compute average, highest, lowest, letter grade; search by name; print a report. Acceptance: correct statistics; case-insensitive search; handles empty class.

**Common mistakes:** comparing strings with `==`; off-by-one on `length`; concatenating in loops.

**Assessment:** 7 exercises plus the grade manager.

**Career relevance:** arrays underpin collections (BEG-030) and data structures (BEG-040).

---

### BEG-016 · Problem-solving
`n: 16` · **Video:** 53 min · **Practice:** 5 h

**Prerequisites:** BEG-015

**Learning outcomes** — the learner can:
1. Restate a problem in their own words and identify inputs, outputs, and constraints.
2. Decompose a problem into steps and express them as pseudocode or a flowchart before coding.
3. Trace a program by hand with a variable table.
4. List edge cases (empty, one element, maximum, negative, invalid) before writing code.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-016-L01 | Understanding the problem first | 8 |
| BEG-016-L02 | Decomposition | 8 |
| BEG-016-L03 | Pseudocode and flowcharts | 10 |
| BEG-016-L04 | Hand-tracing with a variable table | 10 |
| BEG-016-L05 | Thinking in edge cases | 9 |
| BEG-016-L06 | Demo: plan before code on an unseen problem | 8 |

**Lab** — `BEG-016-LAB1` *Plan before code:* for three unseen problems, submit pseudocode and an edge-case list *before* the code. Acceptance: plan and code match; all listed edge cases handled.

**Common mistakes:** coding before understanding; testing only the happy path.

**Assessment:** unseen problem solved with a plan, graded on the plan as much as the code.

**Career relevance:** the habit behind requirement clarification (MID-064) and requirements engineering (SRC-001).

---

### BEG-017 · Introductory algorithms
`n: 17` · **Video:** 63 min · **Practice:** 4 h

**Prerequisites:** BEG-015, BEG-016

**Learning outcomes** — the learner can:
1. Implement linear search and binary search and state when binary search applies.
2. Implement bubble sort and selection sort and trace them on a small array.
3. Count the operations of each algorithm for small inputs and compare growth informally.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-017-L01 | What an algorithm is | 6 |
| BEG-017-L02 | Linear search | 8 |
| BEG-017-L03 | Binary search | 12 |
| BEG-017-L04 | Bubble sort | 10 |
| BEG-017-L05 | Selection sort | 10 |
| BEG-017-L06 | Counting steps: a first look at efficiency | 9 |
| BEG-017-L07 | Demo: racing linear and binary search | 8 |

**Lab** — `BEG-017-LAB1` *Race the algorithms:* time linear vs binary search on arrays of 1,000 / 100,000 / 10,000,000 elements and plot the results in a table. Acceptance: correct implementations; written explanation of the trend.

**Common mistakes:** binary search on unsorted data; integer overflow in `(low + high) / 2` (mention); off-by-one in loop bounds.

**Assessment:** 5 exercises including tracing a sort by hand.

**Career relevance:** formalized in BEG-039; interview staple at Junior level.

---

### BEG-018 · Debugging
`n: 18` · **Video:** 53 min · **Practice:** 3 h

**Prerequisites:** BEG-014

**Learning outcomes** — the learner can:
1. Set breakpoints (including conditional ones) and step into, over, and out in IntelliJ.
2. Inspect and watch variables to find where actual behavior diverges from expected.
3. Read a stack trace and navigate to the failing line.
4. Apply a systematic process: reproduce, isolate, hypothesize, test, fix, verify.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-018-L01 | A method for debugging | 8 |
| BEG-018-L02 | Breakpoints and stepping | 12 |
| BEG-018-L03 | Variables, watches, and evaluate expression | 8 |
| BEG-018-L04 | Reading stack traces | 10 |
| BEG-018-L05 | A catalog of common runtime errors | 7 |
| BEG-018-L06 | Demo: a full bug hunt from report to fix | 8 |

**Lab** — `BEG-018-LAB1` *Bug hunt:* five programs with one logic bug each. For each, record reproduction steps, hypothesis, the line found with the debugger, and the fix. Acceptance: all five fixed with a written trail.

**Common mistakes:** changing code at random; adding print statements everywhere instead of breakpoints; fixing the symptom, not the cause.

**Assessment:** live debugging demonstration (also part of the BEG graduation gate).

**Career relevance:** grows into troubleshooting (JNR-054), profiling (MID-008), and incident handling (MID-050).

> **Teaching note:** introduce the debugger briefly in BEG-013 (step through a loop) so learners use it before this module formalizes it.

---

### BEG-056 · AI coding assistants for learners
`n: new (added in v2.0)` · **Video:** 42 min · **Practice:** 2 h

**Prerequisites:** BEG-016, BEG-018

**Learning outcomes** — the learner can:
1. Explain at a conceptual level how a large language model produces text (tokens, next-token prediction, training data) and why that makes it fluent but not always correct.
2. Recognize hallucinations: invented methods, wrong APIs, confident but incorrect explanations.
3. Ask an assistant a good question: the goal, the code, the exact error, and what was already tried.
4. Use an assistant to explain an error or a concept *after* trying first, and turn the answer into their own understanding.
5. Follow safe-use rules: never paste passwords, keys, or personal data; follow course and employer policies.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-056-L01 | What an AI coding assistant actually is | 8 |
| BEG-056-L02 | Why assistants sound right and are sometimes wrong | 10 |
| BEG-056-L03 | Asking good questions: goal, code, error, attempts | 8 |
| BEG-056-L04 | Learning with AI without skipping the learning | 8 |
| BEG-056-L05 | Demo: using an assistant to understand a stack trace, then checking it | 8 |

**Lab** — `BEG-056-LAB1` *Explain, don't copy:* for three bugs from the `BEG-018-LAB1` bug hunt, first write your own hypothesis, then ask an assistant, then confirm or reject its answer with the debugger. Record one case where the assistant was wrong or incomplete. Acceptance: written log per bug with your hypothesis, the assistant's answer, and the evidence that settled it.

**Common mistakes:** asking before trying; pasting whole projects without the error; trusting an answer because it is confident; pasting secrets into a chat.

**Assessment:** short quiz on how LLMs work and safe use, plus the lab log.

**Career relevance:** the habit of verifying AI output is expected from the first day of a junior role; it deepens in JNR-055 and MID-072.
