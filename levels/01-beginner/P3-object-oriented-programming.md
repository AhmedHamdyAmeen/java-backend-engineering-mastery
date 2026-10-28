# BEG-P3 — Object-Oriented Programming

**Phase goal:** the learner models a small real-world domain as cooperating classes with clear responsibilities, using encapsulation, inheritance, interfaces, and composition appropriately.

**Phase practice:** a running exercise that grows across the phase — a *Bank Accounts* model (accounts, customers, transactions) refactored module by module.

**Phase total:** ~8.6 h video · ~30.5 h practice

---

### BEG-019 · OOP introduction
`n: 19` · **Video:** 43 min · **Practice:** 1.5 h

**Prerequisites:** BEG-014

**Learning outcomes** — the learner can:
1. Contrast a procedural solution with an object-oriented one for the same problem.
2. Identify objects, their state, and their behavior in a plain-language description.
3. Explain the difference between a class and an object.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-019-L01 | When procedural code stops scaling | 10 |
| BEG-019-L02 | Objects: state + behavior | 10 |
| BEG-019-L03 | Classes as blueprints | 7 |
| BEG-019-L04 | Finding objects in a problem description | 8 |
| BEG-019-L05 | Demo: rewriting a procedural bank as objects | 8 |

**Lab** — `BEG-019-LAB1` *Noun and verb hunt:* from a one-page description of a bank, list candidate classes (nouns), their state, and their behaviors (verbs). Acceptance: reasonable candidates with justification.

**Common mistakes:** a class per noun, including irrelevant ones; behavior separated from the data it acts on.

**Assessment:** quiz plus the noun/verb analysis.

**Career relevance:** the start of domain modeling (MID-060, SRA-003).

---

### BEG-020 · Classes and objects
`n: 20` · **Video:** 66 min · **Practice:** 4 h

**Prerequisites:** BEG-019

**Learning outcomes** — the learner can:
1. Write a class with fields, constructors (including overloaded ones), and instance methods.
2. Create objects with `new` and call their methods.
3. Use `this` to refer to fields and to chain constructors.
4. Explain the difference between instance and `static` members and choose correctly.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-020-L01 | Writing your first class | 10 |
| BEG-020-L02 | Constructors | 10 |
| BEG-020-L03 | Instance methods and `this` | 10 |
| BEG-020-L04 | Creating and using objects | 8 |
| BEG-020-L05 | `static`: belonging to the class | 12 |
| BEG-020-L06 | Demo: Bank Accounts v1 from an empty file | 8 |
| BEG-020-L07 | Demo: static vs instance, seen in the debugger | 8 |

**Lab** — `BEG-020-LAB1` *Bank Accounts v1:* `Account` with owner, number, balance; deposit and withdraw; create several accounts in `main`. Acceptance: compiles, works, no logic in `main` beyond wiring.

**Common mistakes:** everything `static`; constructors that do heavy work; shadowing fields without `this`.

**Assessment:** 5 exercises plus Bank Accounts v1.

**Career relevance:** every Spring bean (JNR-009) and entity (JNR-028) is a class.

---

### BEG-021 · Encapsulation
`n: 21` · **Video:** 53 min · **Practice:** 3 h

**Prerequisites:** BEG-020

**Learning outcomes** — the learner can:
1. Apply `private`, package-private, `protected`, and `public` correctly.
2. Protect invariants (e.g., balance never negative) inside the class, not in its callers.
3. Decide when a getter or setter is appropriate and when a behavior method is better.
4. Create an immutable class (final fields, no setters, defensive copies).

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-021-L01 | Why hide data | 8 |
| BEG-021-L02 | Access modifiers | 10 |
| BEG-021-L03 | Invariants: rules the object guarantees | 10 |
| BEG-021-L04 | Getters, setters, and "tell, don't ask" | 8 |
| BEG-021-L05 | Immutable objects | 9 |
| BEG-021-L06 | Demo: protecting the balance invariant | 8 |

**Lab** — `BEG-021-LAB1` *Bank Accounts v2:* make fields private, enforce invariants in `withdraw`, replace `setBalance` with behavior methods, add an immutable `Money` class. Acceptance: no way to reach an invalid state from outside the class.

**Common mistakes:** generating getters/setters for every field by reflex; returning internal mutable arrays.

**Assessment:** code review exercise: find encapsulation violations in a provided class.

**Career relevance:** value objects (MID-060) and safe APIs (JNR-020).

---

### BEG-022 · Inheritance
`n: 22` · **Video:** 66 min · **Practice:** 3 h

**Prerequisites:** BEG-021

**Learning outcomes** — the learner can:
1. Create a subclass with `extends`, call superclass constructors with `super(...)`, and override methods with `@Override`.
2. Explain what is and is not inherited.
3. Apply the "is-a" test and choose composition when inheritance does not fit.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-022-L01 | Reusing behavior with `extends` | 10 |
| BEG-022-L02 | Constructors and `super` | 10 |
| BEG-022-L03 | Overriding methods | 10 |
| BEG-022-L04 | `final` classes and methods | 6 |
| BEG-022-L05 | Composition over inheritance | 14 |
| BEG-022-L06 | Demo: savings and checking accounts with `extends` | 8 |
| BEG-022-L07 | Demo: refactoring bad inheritance into composition | 8 |

**Lab** — `BEG-022-LAB1` *Bank Accounts v3:* `SavingsAccount` (interest) and `CheckingAccount` (overdraft) extend `Account`. Then refactor a provided bad inheritance hierarchy into composition. Acceptance: overrides correct; refactor explained.

**Common mistakes:** inheritance for code reuse only; deep hierarchies; forgetting `@Override`.

**Assessment:** 4 exercises plus a written "is-a or has-a?" quiz.

**Career relevance:** framework extension points (JNR-008) and design patterns (JNR-005).

---

### BEG-023 · Polymorphism
`n: 23` · **Video:** 48 min · **Practice:** 3 h

**Prerequisites:** BEG-022

**Learning outcomes** — the learner can:
1. Explain dynamic dispatch and predict which method runs for a given reference and object type.
2. Use a superclass or interface reference to treat different objects uniformly.
3. Replace a type-checking `if`/`switch` chain with polymorphic method calls.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-023-L01 | One call, many behaviors | 10 |
| BEG-023-L02 | Upcasting, downcasting, and `instanceof` | 10 |
| BEG-023-L03 | Dynamic dispatch under the hood (conceptual) | 8 |
| BEG-023-L04 | Replacing conditionals with polymorphism | 12 |
| BEG-023-L05 | Demo: month-end processing without a single type check | 8 |

**Lab** — `BEG-023-LAB1` *Month-end processing:* apply month-end rules to a mixed list of accounts with a single loop and no type checks. Acceptance: adding a new account type requires no change to the loop.

**Common mistakes:** downcasting everywhere; confusing overloading with overriding.

**Assessment:** "predict the output" quiz on 8 snippets.

**Career relevance:** Strategy pattern (JNR-005) and dependency inversion (JNR-004).

---

### BEG-024 · Abstract classes and interfaces
`n: 24` · **Video:** 53 min · **Practice:** 3 h

**Prerequisites:** BEG-023

**Learning outcomes** — the learner can:
1. Declare an interface as a contract and implement it in several classes.
2. Write an abstract class with shared state and abstract methods.
3. Choose between an interface and an abstract class for a given scenario.
4. Use default methods and explain their purpose and risks.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-024-L01 | Interfaces as contracts | 12 |
| BEG-024-L02 | Abstract classes | 10 |
| BEG-024-L03 | Interface vs abstract class: decision guide | 10 |
| BEG-024-L04 | Default and static interface methods | 8 |
| BEG-024-L05 | Programming to an interface | 5 |
| BEG-024-L06 | Demo: pluggable notification channels | 8 |

**Lab** — `BEG-024-LAB1` *Notification channels:* `Notifier` interface with Email, SMS, and Console implementations; the bank sends statements through any `Notifier`. Acceptance: the bank class depends only on the interface.

**Common mistakes:** interfaces with a single "god" method; abstract classes used where an interface suffices.

**Assessment:** 4 exercises plus a design question.

**Career relevance:** every Spring repository and service boundary (JNR-009, JNR-029) is an interface.

---

### BEG-025 · Relationships
`n: 25` · **Video:** 43 min · **Practice:** 2 h

**Prerequisites:** BEG-020, BEG-022

**Learning outcomes** — the learner can:
1. Distinguish association, aggregation, composition, and dependency, with Java examples.
2. Draw a simple UML class diagram showing relationships and multiplicities.
3. Implement one-to-many relationships in code.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-025-L01 | How objects know each other | 8 |
| BEG-025-L02 | Association, aggregation, composition | 12 |
| BEG-025-L03 | Dependency | 5 |
| BEG-025-L04 | UML class diagrams, the useful 20% | 10 |
| BEG-025-L05 | Demo: drawing the UML, then coding Customer and Account | 8 |

**Lab** — `BEG-025-LAB1` *Bank Accounts v4:* `Customer` owns many `Account`s; `Account` has many `Transaction`s (composition). Draw the UML diagram first. Acceptance: diagram matches code.

**Common mistakes:** bidirectional links that are never kept in sync; UML with every field listed.

**Assessment:** diagram-from-description exercise.

**Career relevance:** entity relationships (JNR-030) and relational modeling (BEG-049).

---

### BEG-026 · Java object model
`n: 26` · **Video:** 53 min · **Practice:** 3 h

**Prerequisites:** BEG-022

**Learning outcomes** — the learner can:
1. Explain that every class extends `Object` and name its key methods.
2. Distinguish identity (`==`) from equality (`equals`) and fix string comparison bugs.
3. Implement `equals` and `hashCode` consistently and explain the contract.
4. Override `toString` for useful logging and debugging.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-026-L01 | The `Object` class | 8 |
| BEG-026-L02 | Identity vs equality | 10 |
| BEG-026-L03 | The `equals`/`hashCode` contract | 15 |
| BEG-026-L04 | `toString` | 5 |
| BEG-026-L05 | Records as a preview: equality for free | 7 |
| BEG-026-L06 | Demo: the broken HashSet and the equals/hashCode fix | 8 |

**Lab** — `BEG-026-LAB1` *Broken set:* put `Money` objects into a `HashSet` (shown as a black box) with and without `hashCode`; observe and explain the duplicates. Acceptance: correct implementation and explanation.

**Common mistakes:** overriding `equals` without `hashCode`; using mutable fields in `hashCode`.

**Assessment:** contract quiz plus implementation exercise.

**Career relevance:** essential for collections (BEG-030), hashing (BEG-041), and JPA entities (JNR-028).

---

### BEG-027 · Packages and organization
`n: 27` · **Video:** 38 min · **Practice:** 2 h

**Prerequisites:** BEG-021

**Learning outcomes** — the learner can:
1. Organize classes into packages that match folder structure and use imports correctly.
2. Use package-private visibility to hide implementation classes.
3. Group classes by feature rather than by technical type, and justify it.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-027-L01 | Packages and folders | 8 |
| BEG-027-L02 | Imports and name clashes | 7 |
| BEG-027-L03 | Package-private: the forgotten modifier | 7 |
| BEG-027-L04 | Package by feature vs by layer | 8 |
| BEG-027-L05 | Demo: reorganizing Bank Accounts into feature packages | 8 |

**Lab** — `BEG-027-LAB1` *Bank Accounts v5:* reorganize into feature packages with a minimal public surface. Acceptance: only intended classes are `public`.

**Common mistakes:** one giant default package; everything `public`.

**Assessment:** refactoring exercise.

**Career relevance:** modular monoliths (MID-059) start here.

---

### BEG-028 · OOP design practice
`n: 28` · **Video:** 53 min · **Practice:** 6 h

**Prerequisites:** BEG-024, BEG-025, BEG-027

**Learning outcomes** — the learner can:
1. Model a new domain (e.g., a parking garage) from a written description into classes, interfaces, and relationships.
2. Assign each responsibility to the class that has the information to fulfil it.
3. Spot and split a "god class".
4. Explain their design trade-offs to a reviewer.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-028-L01 | From requirements to classes: worked example | 15 |
| BEG-028-L02 | Assigning responsibilities | 10 |
| BEG-028-L03 | Recognizing and splitting god classes | 10 |
| BEG-028-L04 | Explaining a design | 10 |
| BEG-028-L05 | Demo: modeling the parking garage from requirements | 8 |

**Lab** — `BEG-028-LAB1` *Parking garage:* model and implement a garage with levels, spot sizes, vehicles, tickets, and fees. Acceptance: UML + code + a half-page design rationale; peer review completed.

**Common mistakes:** anemic classes with all logic in one manager; premature inheritance.

**Assessment:** design review using the rubric in `assessment/framework.md` (design dimension).

**Career relevance:** design reviews (MID-066) and DDD (MID-060).
