# Course Outline — levels, phases, modules, topics, and lectures

<!-- Generated one-off from catalog/modules.yaml and the phase files. Not maintained by tools/build.py. -->

Version 2.0 · 321 modules · 8 levels

## Level 1 — Beginner — Foundations (`BEG`)

- **Audience:** Someone with no programming, computer science, or IT background.
- **Graduation outcome:** Writes Java console applications, solves basic programming problems, uses Git, understands relational databases, and explains how a web application works.
- **Study hours:** 180–250 · **Video hours:** 40–55 · **Lessons:** 140–190
- **Capstone:** `BEG-CAP` Library Management System: Java console application using OOP, collections, file handling, and PostgreSQL via JDBC.
- **Graduation gate:** Explain the program's architecture, demonstrate debugging, write SQL queries, and extend the application with a new requirement.

### BEG-P1 — Introduction to Computers and Software Engineering

#### BEG-001 · Understanding computers
*58 min video · 2 h practice* · Prerequisites: none

**Topics:** What computers do; hardware vs software; CPU, RAM, SSD; storage; input/output; binary and bits; operating systems; processes and applications

**Lessons:**
- `BEG-001-L01` What a computer actually does: input, processing, storage, output (10 min)
- `BEG-001-L02` CPU, RAM, and storage: the kitchen analogy (10 min)
- `BEG-001-L03` Bits, bytes, and binary numbers (12 min)
- `BEG-001-L04` The operating system's job (8 min)
- `BEG-001-L05` Applications and processes: Task Manager / Activity Monitor tour (10 min)
- `BEG-001-L06` Demo: watching RAM and CPU while opening apps (8 min)

#### BEG-002 · Understanding software
*48 min video · 1 h practice* · Prerequisites: BEG-001

**Topics:** What software is; desktop, mobile, web, backend, embedded; programs vs services; software lifecycle

**Lessons:**
- `BEG-002-L01` What software is: instructions, data, and behavior (8 min)
- `BEG-002-L02` Kinds of software, with everyday examples (10 min)
- `BEG-002-L03` Programs vs services: why a backend never "finishes" (10 min)
- `BEG-002-L04` The software lifecycle (12 min)
- `BEG-002-L05` Demo: one app, many pieces: mobile app, website, and backend (8 min)

#### BEG-003 · The internet
*63 min video · 1.5 h practice* · Prerequisites: BEG-001

**Topics:** Internet vs web; IP addresses; domains; DNS; browsers; clients and servers; requests and responses; HTTP vs HTTPS

**Lessons:**
- `BEG-003-L01` Internet vs web (8 min)
- `BEG-003-L02` IP addresses and ports (10 min)
- `BEG-003-L03` Domains and DNS (10 min)
- `BEG-003-L04` Clients, servers, requests, and responses (12 min)
- `BEG-003-L05` HTTP vs HTTPS: what encryption protects (8 min)
- `BEG-003-L06` Watching a request in the browser's developer tools (7 min)
- `BEG-003-L07` Demo: following a URL with `nslookup` and the Network tab (8 min)

#### BEG-004 · Introduction to engineering
*48 min video · 1 h practice* · Prerequisites: BEG-002

**Topics:** Developer vs software engineer; frontend vs backend vs full-stack; QA, DevOps, SRE, architect; how teams collaborate

**Lessons:**
- `BEG-004-L01` Developer vs software engineer (8 min)
- `BEG-004-L02` Roles in an engineering team (12 min)
- `BEG-004-L03` How a feature travels from idea to production (10 min)
- `BEG-004-L04` Your career map: the eight levels of this course (10 min)
- `BEG-004-L05` Demo: a day in a backend engineer's workflow, walked through (8 min)

#### BEG-005 · Development environment
*58 min video · 2 h practice* · Prerequisites: BEG-001

**Topics:** OS basics; installing the JDK; IntelliJ IDEA; VS Code; file extensions; environment variables; PATH

**Lessons:**
- `BEG-005-L01` Files, folders, and extensions on Windows, macOS, and Linux (8 min)
- `BEG-005-L02` Installing the JDK (all three operating systems) (12 min)
- `BEG-005-L03` Environment variables and PATH (10 min)
- `BEG-005-L04` Installing and tour of IntelliJ IDEA (12 min)
- `BEG-005-L05` VS Code as an alternative (8 min)
- `BEG-005-L06` Demo: installing the JDK and fixing a broken PATH (8 min)

#### BEG-006 · Command line
*68 min video · 3 h practice* · Prerequisites: BEG-005

**Topics:** Terminal, shell, directories, file commands, paths, permissions, environment variables, pipes, redirection, basic Bash/PowerShell

**Lessons:**
- `BEG-006-L01` Terminal, shell, and prompt (8 min)
- `BEG-006-L02` Paths: absolute, relative, home, `.` and `..` (10 min)
- `BEG-006-L03` Working with files and folders (12 min)
- `BEG-006-L04` Pipes and redirection (10 min)
- `BEG-006-L05` Environment variables in the shell (8 min)
- `BEG-006-L06` Permissions basics (7 min)
- `BEG-006-L07` Bash vs PowerShell cheat sheet (5 min)
- `BEG-006-L08` Demo: setting up a project folder using only the terminal (8 min)

#### BEG-007 · How code runs
*48 min video · 1.5 h practice* · Prerequisites: BEG-002, BEG-006

**Topics:** Source code, compilation, bytecode, execution, runtime errors; Java compiler, JVM, JRE, JDK

**Lessons:**
- `BEG-007-L01` From text to execution: compilers and interpreters (10 min)
- `BEG-007-L02` Java's approach: bytecode and the JVM (10 min)
- `BEG-007-L03` JDK vs JRE vs JVM (8 min)
- `BEG-007-L04` Compile and run from the terminal (12 min)
- `BEG-007-L05` Demo: compile, run, break, and fix Hello World in the terminal (8 min)

### BEG-P2 — Programming Fundamentals with Java

#### BEG-008 · First Java program
*48 min video · 2 h practice* · Prerequisites: BEG-007

**Topics:** Java syntax, main(), classes, statements, comments, console output

**Lessons:**
- `BEG-008-L01` Anatomy of Hello World (10 min)
- `BEG-008-L02` Statements, semicolons, and blocks (8 min)
- `BEG-008-L03` Printing output (8 min)
- `BEG-008-L04` Comments (6 min)
- `BEG-008-L05` Reading compiler errors (8 min)
- `BEG-008-L06` Demo: fixing five broken programs from compiler messages (8 min)

#### BEG-009 · Variables and data types
*63 min video · 4 h practice* · Prerequisites: BEG-008

**Topics:** Primitives, reference types, variables, literals, constants, naming conventions, type conversion

**Lessons:**
- `BEG-009-L01` Variables as labeled boxes (8 min)
- `BEG-009-L02` The eight primitive types (12 min)
- `BEG-009-L03` Strings and reference types (8 min)
- `BEG-009-L04` Literals, constants, and naming (8 min)
- `BEG-009-L05` Type conversion and casting (12 min)
- `BEG-009-L06` Local type inference with `var` (7 min)
- `BEG-009-L07` Demo: unit converter and an integer overflow (8 min)

#### BEG-010 · Operators
*48 min video · 3 h practice* · Prerequisites: BEG-009

**Topics:** Arithmetic, comparison, logical, assignment, precedence, increment/decrement

**Lessons:**
- `BEG-010-L01` Arithmetic operators and integer division (10 min)
- `BEG-010-L02` Comparison and logical operators (10 min)
- `BEG-010-L03` Assignment and compound assignment (6 min)
- `BEG-010-L04` Increment, decrement, and precedence (8 min)
- `BEG-010-L05` Short-circuit evaluation (6 min)
- `BEG-010-L06` Demo: predict-then-run expression challenge (8 min)

#### BEG-011 · Input and output
*48 min video · 3 h practice* · Prerequisites: BEG-010

**Topics:** Scanner, console input, formatting, parsing, input validation

**Lessons:**
- `BEG-011-L01` Reading input with Scanner (10 min)
- `BEG-011-L02` The `nextInt` / `nextLine` trap (8 min)
- `BEG-011-L03` Parsing strings into numbers (8 min)
- `BEG-011-L04` Formatting output (8 min)
- `BEG-011-L05` Validating input: never trust the user (6 min)
- `BEG-011-L06` Demo: building the receipt printer with input validation (8 min)

#### BEG-012 · Conditions
*52 min video · 4 h practice* · Prerequisites: BEG-010

**Topics:** if, else, else if, switch, switch expressions, nested conditions

**Lessons:**
- `BEG-012-L01` Making decisions with `if` (10 min)
- `BEG-012-L02` `else if` chains and boundary values (8 min)
- `BEG-012-L03` Classic `switch` and fall-through (8 min)
- `BEG-012-L04` Switch expressions (modern Java) (8 min)
- `BEG-012-L05` Taming nested conditions (10 min)
- `BEG-012-L06` Demo: shipping cost rules and their boundaries (8 min)

#### BEG-013 · Loops
*58 min video · 5 h practice* · Prerequisites: BEG-012

**Topics:** for, enhanced for, while, do-while, break, continue, nested loops

**Lessons:**
- `BEG-013-L01` Why loops: repetition without copy-paste (6 min)
- `BEG-013-L02` The `for` loop (10 min)
- `BEG-013-L03` `while` and `do-while` (10 min)
- `BEG-013-L04` `break`, `continue`, and loop control (8 min)
- `BEG-013-L05` Nested loops (10 min)
- `BEG-013-L06` Off-by-one errors and infinite loops (6 min)
- `BEG-013-L07` Demo: number guessing game, stepping through the loop in the debugger (8 min)

#### BEG-014 · Methods
*72 min video · 5 h practice* · Prerequisites: BEG-013

**Topics:** Parameters, return values, signatures, overloading, scope, call stack, recursion basics

**Lessons:**
- `BEG-014-L01` Why methods: naming and reuse (8 min)
- `BEG-014-L02` Parameters and return values (10 min)
- `BEG-014-L03` Method signatures and overloading (8 min)
- `BEG-014-L04` Scope: where variables live (8 min)
- `BEG-014-L05` The call stack (10 min)
- `BEG-014-L06` Recursion basics (12 min)
- `BEG-014-L07` Demo: building the calculator one method at a time (8 min)
- `BEG-014-L08` Demo: tracing recursion on the call stack (8 min)

#### BEG-015 · Arrays and strings
*74 min video · 5 h practice* · Prerequisites: BEG-013, BEG-014

**Topics:** One-dimensional/multidimensional arrays, String, StringBuilder, common operations

**Lessons:**
- `BEG-015-L01` Arrays: fixed-size lists (10 min)
- `BEG-015-L02` Iterating and enhanced for (8 min)
- `BEG-015-L03` Two-dimensional arrays (10 min)
- `BEG-015-L04` Working with Strings (12 min)
- `BEG-015-L05` Immutability and StringBuilder (10 min)
- `BEG-015-L06` `Arrays` utility class (8 min)
- `BEG-015-L07` Demo: student-grade manager with arrays (8 min)
- `BEG-015-L08` Demo: string bugs: `==`, off-by-one, and slow concatenation (8 min)

#### BEG-016 · Problem-solving
*53 min video · 5 h practice* · Prerequisites: BEG-015

**Topics:** Decomposition, pseudocode, flowcharts, tracing, debugging, edge cases

**Lessons:**
- `BEG-016-L01` Understanding the problem first (8 min)
- `BEG-016-L02` Decomposition (8 min)
- `BEG-016-L03` Pseudocode and flowcharts (10 min)
- `BEG-016-L04` Hand-tracing with a variable table (10 min)
- `BEG-016-L05` Thinking in edge cases (9 min)
- `BEG-016-L06` Demo: plan before code on an unseen problem (8 min)

#### BEG-017 · Introductory algorithms
*63 min video · 4 h practice* · Prerequisites: BEG-015, BEG-016

**Topics:** Linear search, binary search, bubble sort, selection sort, basic time complexity

**Lessons:**
- `BEG-017-L01` What an algorithm is (6 min)
- `BEG-017-L02` Linear search (8 min)
- `BEG-017-L03` Binary search (12 min)
- `BEG-017-L04` Bubble sort (10 min)
- `BEG-017-L05` Selection sort (10 min)
- `BEG-017-L06` Counting steps: a first look at efficiency (9 min)
- `BEG-017-L07` Demo: racing linear and binary search (8 min)

#### BEG-018 · Debugging
*53 min video · 3 h practice* · Prerequisites: BEG-014

**Topics:** Breakpoints, step into/over/out, variable inspection, stack traces, common errors

**Lessons:**
- `BEG-018-L01` A method for debugging (8 min)
- `BEG-018-L02` Breakpoints and stepping (12 min)
- `BEG-018-L03` Variables, watches, and evaluate expression (8 min)
- `BEG-018-L04` Reading stack traces (10 min)
- `BEG-018-L05` A catalog of common runtime errors (7 min)
- `BEG-018-L06` Demo: a full bug hunt from report to fix (8 min)

#### BEG-056 · AI coding assistants for learners
*42 min video · 2 h practice* · Prerequisites: BEG-016, BEG-018 · added in v2.0

**Topics:** How LLMs work conceptually, tokens and prediction, hallucination, asking good questions, explaining errors, never pasting secrets, try-first learning rules

**Lessons:**
- `BEG-056-L01` What an AI coding assistant actually is (8 min)
- `BEG-056-L02` Why assistants sound right and are sometimes wrong (10 min)
- `BEG-056-L03` Asking good questions: goal, code, error, attempts (8 min)
- `BEG-056-L04` Learning with AI without skipping the learning (8 min)
- `BEG-056-L05` Demo: using an assistant to understand a stack trace, then checking it (8 min)

### BEG-P3 — Object-Oriented Programming

#### BEG-019 · OOP introduction
*43 min video · 1.5 h practice* · Prerequisites: BEG-014

**Topics:** Procedural vs object-oriented programming, objects, classes, state, behavior

**Lessons:**
- `BEG-019-L01` When procedural code stops scaling (10 min)
- `BEG-019-L02` Objects: state + behavior (10 min)
- `BEG-019-L03` Classes as blueprints (7 min)
- `BEG-019-L04` Finding objects in a problem description (8 min)
- `BEG-019-L05` Demo: rewriting a procedural bank as objects (8 min)

#### BEG-020 · Classes and objects
*66 min video · 4 h practice* · Prerequisites: BEG-019

**Topics:** Fields, constructors, methods, this, object creation

**Lessons:**
- `BEG-020-L01` Writing your first class (10 min)
- `BEG-020-L02` Constructors (10 min)
- `BEG-020-L03` Instance methods and `this` (10 min)
- `BEG-020-L04` Creating and using objects (8 min)
- `BEG-020-L05` `static`: belonging to the class (12 min)
- `BEG-020-L06` Demo: Bank Accounts v1 from an empty file (8 min)
- `BEG-020-L07` Demo: static vs instance, seen in the debugger (8 min)

#### BEG-021 · Encapsulation
*53 min video · 3 h practice* · Prerequisites: BEG-020

**Topics:** Access modifiers, getters/setters, invariants, immutability

**Lessons:**
- `BEG-021-L01` Why hide data (8 min)
- `BEG-021-L02` Access modifiers (10 min)
- `BEG-021-L03` Invariants: rules the object guarantees (10 min)
- `BEG-021-L04` Getters, setters, and "tell, don't ask" (8 min)
- `BEG-021-L05` Immutable objects (9 min)
- `BEG-021-L06` Demo: protecting the balance invariant (8 min)

#### BEG-022 · Inheritance
*66 min video · 3 h practice* · Prerequisites: BEG-021

**Topics:** extends, superclass/subclass, overriding, super, composition vs inheritance

**Lessons:**
- `BEG-022-L01` Reusing behavior with `extends` (10 min)
- `BEG-022-L02` Constructors and `super` (10 min)
- `BEG-022-L03` Overriding methods (10 min)
- `BEG-022-L04` `final` classes and methods (6 min)
- `BEG-022-L05` Composition over inheritance (14 min)
- `BEG-022-L06` Demo: savings and checking accounts with `extends` (8 min)
- `BEG-022-L07` Demo: refactoring bad inheritance into composition (8 min)

#### BEG-023 · Polymorphism
*48 min video · 3 h practice* · Prerequisites: BEG-022

**Topics:** Dynamic dispatch, upcasting, interfaces, abstraction

**Lessons:**
- `BEG-023-L01` One call, many behaviors (10 min)
- `BEG-023-L02` Upcasting, downcasting, and `instanceof` (10 min)
- `BEG-023-L03` Dynamic dispatch under the hood (conceptual) (8 min)
- `BEG-023-L04` Replacing conditionals with polymorphism (12 min)
- `BEG-023-L05` Demo: month-end processing without a single type check (8 min)

#### BEG-024 · Abstract classes and interfaces
*53 min video · 3 h practice* · Prerequisites: BEG-023

**Topics:** Abstract methods, interface contracts, default methods

**Lessons:**
- `BEG-024-L01` Interfaces as contracts (12 min)
- `BEG-024-L02` Abstract classes (10 min)
- `BEG-024-L03` Interface vs abstract class: decision guide (10 min)
- `BEG-024-L04` Default and static interface methods (8 min)
- `BEG-024-L05` Programming to an interface (5 min)
- `BEG-024-L06` Demo: pluggable notification channels (8 min)

#### BEG-025 · Relationships
*43 min video · 2 h practice* · Prerequisites: BEG-020, BEG-022

**Topics:** Association, aggregation, composition, dependency

**Lessons:**
- `BEG-025-L01` How objects know each other (8 min)
- `BEG-025-L02` Association, aggregation, composition (12 min)
- `BEG-025-L03` Dependency (5 min)
- `BEG-025-L04` UML class diagrams, the useful 20% (10 min)
- `BEG-025-L05` Demo: drawing the UML, then coding Customer and Account (8 min)

#### BEG-026 · Java object model
*53 min video · 3 h practice* · Prerequisites: BEG-022

**Topics:** Object, equals(), hashCode(), toString(), identity vs equality

**Lessons:**
- `BEG-026-L01` The `Object` class (8 min)
- `BEG-026-L02` Identity vs equality (10 min)
- `BEG-026-L03` The `equals`/`hashCode` contract (15 min)
- `BEG-026-L04` `toString` (5 min)
- `BEG-026-L05` Records as a preview: equality for free (7 min)
- `BEG-026-L06` Demo: the broken HashSet and the equals/hashCode fix (8 min)

#### BEG-027 · Packages and organization
*38 min video · 2 h practice* · Prerequisites: BEG-021

**Topics:** Packages, imports, visibility, cohesive class design

**Lessons:**
- `BEG-027-L01` Packages and folders (8 min)
- `BEG-027-L02` Imports and name clashes (7 min)
- `BEG-027-L03` Package-private: the forgotten modifier (7 min)
- `BEG-027-L04` Package by feature vs by layer (8 min)
- `BEG-027-L05` Demo: reorganizing Bank Accounts into feature packages (8 min)

#### BEG-028 · OOP design practice
*53 min video · 6 h practice* · Prerequisites: BEG-024, BEG-025, BEG-027

**Topics:** Modeling real-world domains, identifying responsibilities, avoiding god classes

**Lessons:**
- `BEG-028-L01` From requirements to classes: worked example (15 min)
- `BEG-028-L02` Assigning responsibilities (10 min)
- `BEG-028-L03` Recognizing and splitting god classes (10 min)
- `BEG-028-L04` Explaining a design (10 min)
- `BEG-028-L05` Demo: modeling the parking garage from requirements (8 min)

### BEG-P4 — Essential Core Java

#### BEG-029 · Exceptions
*71 min video · 4 h practice* · Prerequisites: BEG-022

**Topics:** Checked vs unchecked, try/catch/finally, throw/throws, custom exceptions, try-with-resources

**Lessons:**
- `BEG-029-L01` What goes wrong at runtime (8 min)
- `BEG-029-L02` The exception hierarchy (10 min)
- `BEG-029-L03` `try`, `catch`, `finally` (10 min)
- `BEG-029-L04` Throwing and declaring (8 min)
- `BEG-029-L05` Custom exceptions (9 min)
- `BEG-029-L06` try-with-resources (10 min)
- `BEG-029-L07` Demo: InsufficientFundsException end to end (8 min)
- `BEG-029-L08` Demo: finding a swallowed exception (8 min)

#### BEG-030 · Collections
*81 min video · 5 h practice* · Prerequisites: BEG-024, BEG-026

**Topics:** List, Set, Map, Queue, ArrayList, LinkedList, HashSet, HashMap, TreeMap

**Lessons:**
- `BEG-030-L01` Beyond arrays: the Collections Framework (8 min)
- `BEG-030-L02` Lists (12 min)
- `BEG-030-L03` Sets (10 min)
- `BEG-030-L04` Maps (15 min)
- `BEG-030-L05` Queues and deques (8 min)
- `BEG-030-L06` Choosing a collection: decision chart (7 min)
- `BEG-030-L07` Iteration and `ConcurrentModificationException` (5 min)
- `BEG-030-L08` Demo: word frequency with Map (8 min)
- `BEG-030-L09` Demo: the wrong collection, measured (8 min)

#### BEG-031 · Generics
*48 min video · 3 h practice* · Prerequisites: BEG-030

**Topics:** Generic classes, methods, type parameters, wildcards basics

**Lessons:**
- `BEG-031-L01` Life before generics (7 min)
- `BEG-031-L02` Generic classes (10 min)
- `BEG-031-L03` Generic methods (8 min)
- `BEG-031-L04` Bounded types (8 min)
- `BEG-031-L05` Wildcards: reading the JDK's signatures (7 min)
- `BEG-031-L06` Demo: building a generic in-memory repository (8 min)

#### BEG-032 · Sorting and comparison
*38 min video · 2 h practice* · Prerequisites: BEG-024, BEG-030

**Topics:** Comparable, Comparator, sorting collections

**Lessons:**
- `BEG-032-L01` Natural ordering with Comparable (10 min)
- `BEG-032-L02` Comparators (10 min)
- `BEG-032-L03` Multi-key sorting (10 min)
- `BEG-032-L04` Demo: a leaderboard with multi-key comparators (8 min)

#### BEG-033 · Date and time
*48 min video · 2 h practice* · Prerequisites: BEG-020

**Topics:** LocalDate, LocalDateTime, Instant, Duration, ZonedDateTime, time zones

**Lessons:**
- `BEG-033-L01` Why time is hard (8 min)
- `BEG-033-L02` Local dates and times (10 min)
- `BEG-033-L03` Instants and time zones (12 min)
- `BEG-033-L04` Durations, periods, formatting (10 min)
- `BEG-033-L05` Demo: a meeting across time zones and a daylight-saving change (8 min)

#### BEG-034 · Files and I/O
*53 min video · 3 h practice* · Prerequisites: BEG-006, BEG-029

**Topics:** Paths, Files API, reading/writing text, streams, buffered I/O

**Lessons:**
- `BEG-034-L01` Paths and the Files API (10 min)
- `BEG-034-L02` Reading and writing text (12 min)
- `BEG-034-L03` Streams, readers, and buffering (12 min)
- `BEG-034-L04` Character encoding (UTF-8) (6 min)
- `BEG-034-L05` A simple CSV format (5 min)
- `BEG-034-L06` Demo: saving and loading contacts as CSV (8 min)

#### BEG-035 · Functional basics
*48 min video · 2.5 h practice* · Prerequisites: BEG-024

**Topics:** Lambda expressions, functional interfaces, method references

**Lessons:**
- `BEG-035-L01` Passing behavior as a value (10 min)
- `BEG-035-L02` Lambda syntax (10 min)
- `BEG-035-L03` The standard functional interfaces (12 min)
- `BEG-035-L04` Method references (8 min)
- `BEG-035-L05` Demo: replacing anonymous classes with lambdas (8 min)

#### BEG-036 · Stream API
*71 min video · 4 h practice* · Prerequisites: BEG-030, BEG-035

**Topics:** filter, map, flatMap, reduce, collectors, grouping

**Lessons:**
- `BEG-036-L01` Streams vs loops (8 min)
- `BEG-036-L02` Intermediate operations (12 min)
- `BEG-036-L03` Terminal operations and laziness (10 min)
- `BEG-036-L04` `flatMap` (8 min)
- `BEG-036-L05` Collectors and grouping (12 min)
- `BEG-036-L06` When not to use a stream (5 min)
- `BEG-036-L07` Demo: building the sales report pipeline (8 min)
- `BEG-036-L08` Demo: rewriting an unreadable stream as a loop (8 min)

#### BEG-037 · Optional
*33 min video · 1.5 h practice* · Prerequisites: BEG-035

**Topics:** Optional creation, transformations, appropriate usage

**Lessons:**
- `BEG-037-L01` The billion-dollar mistake: null (8 min)
- `BEG-037-L02` Using Optional well (10 min)
- `BEG-037-L03` Optional anti-patterns (7 min)
- `BEG-037-L04` Demo: making `findById` return Optional (8 min)

#### BEG-038 · Java memory basics
*43 min video · 1.5 h practice* · Prerequisites: BEG-014, BEG-020

**Topics:** Stack and heap conceptual model, object references, garbage collection introduction

**Lessons:**
- `BEG-038-L01` Stack and heap: a picture (12 min)
- `BEG-038-L02` References and aliasing (10 min)
- `BEG-038-L03` Garbage collection, gently (8 min)
- `BEG-038-L04` `OutOfMemoryError` and `StackOverflowError` (5 min)
- `BEG-038-L05` Demo: drawing stack and heap, then checking in the debugger (8 min)

### BEG-P5 — Computer Science Foundations

#### BEG-039 · Algorithms and complexity
*58 min video · 3 h practice* · Prerequisites: BEG-017

**Topics:** Big O, time vs space complexity, best/average/worst cases

**Lessons:**
- `BEG-039-L01` Why we measure growth, not seconds (8 min)
- `BEG-039-L02` Big O notation (12 min)
- `BEG-039-L03` Analyzing loops and nested loops (12 min)
- `BEG-039-L04` Space complexity (8 min)
- `BEG-039-L05` Best, average, worst (10 min)
- `BEG-039-L06` Demo: turning an O(n²) solution into O(n) (8 min)

#### BEG-040 · Linear data structures
*68 min video · 5 h practice* · Prerequisites: BEG-031, BEG-039

**Topics:** Arrays, dynamic arrays, linked lists, stacks, queues

**Lessons:**
- `BEG-040-L01` Arrays in memory (8 min)
- `BEG-040-L02` Dynamic arrays and resizing (12 min)
- `BEG-040-L03` Linked lists (15 min)
- `BEG-040-L04` Stacks (10 min)
- `BEG-040-L05` Queues (10 min)
- `BEG-040-L06` Choosing: ArrayList vs LinkedList vs ArrayDeque (5 min)
- `BEG-040-L07` Demo: building MyArrayList and watching it resize (8 min)

#### BEG-041 · Hashing
*53 min video · 3 h practice* · Prerequisites: BEG-026, BEG-040

**Topics:** Hash functions, hash tables, collisions, hash-based collections

**Lessons:**
- `BEG-041-L01` Hash functions (10 min)
- `BEG-041-L02` Hash tables and buckets (12 min)
- `BEG-041-L03` Collisions and resizing (12 min)
- `BEG-041-L04` Inside HashMap and HashSet (11 min)
- `BEG-041-L05` Demo: MyHashMap and the constant-hashCode slowdown (8 min)

#### BEG-042 · Trees
*63 min video · 4 h practice* · Prerequisites: BEG-014, BEG-040

**Topics:** Binary trees, BST, traversal, heap fundamentals

**Lessons:**
- `BEG-042-L01` Trees and terminology (8 min)
- `BEG-042-L02` Binary search trees (15 min)
- `BEG-042-L03` Traversals (12 min)
- `BEG-042-L04` Balance (concept only) (8 min)
- `BEG-042-L05` Heaps and PriorityQueue (12 min)
- `BEG-042-L06` Demo: BST insert and traversals, step by step (8 min)

#### BEG-043 · Graph basics
*53 min video · 3 h practice* · Prerequisites: BEG-030, BEG-042

**Topics:** Vertices, edges, BFS, DFS, common applications

**Lessons:**
- `BEG-043-L01` Graphs everywhere (8 min)
- `BEG-043-L02` Representing graphs (10 min)
- `BEG-043-L03` Breadth-first search (12 min)
- `BEG-043-L04` Depth-first search (10 min)
- `BEG-043-L05` Applications: dependencies and cycles (5 min)
- `BEG-043-L06` Demo: metro route finder with BFS (8 min)

#### BEG-044 · Algorithmic techniques
*53 min video · 4 h practice* · Prerequisites: BEG-015, BEG-039

**Topics:** Two pointers, sliding window, recursion, basic backtracking

**Lessons:**
- `BEG-044-L01` Two pointers (12 min)
- `BEG-044-L02` Sliding window (12 min)
- `BEG-044-L03` Thinking recursively (10 min)
- `BEG-044-L04` Backtracking (11 min)
- `BEG-044-L05` Demo: solving a problem with a sliding window (8 min)

#### BEG-045 · Testing fundamentals
*58 min video · 4 h practice* · Prerequisites: BEG-024, BEG-029

**Topics:** What testing is, test cases, assertions, boundary conditions, JUnit introduction

**Lessons:**
- `BEG-045-L01` Why test automatically (8 min)
- `BEG-045-L02` Anatomy of a test case (8 min)
- `BEG-045-L03` First JUnit 5 tests (12 min)
- `BEG-045-L04` Testing exceptions (7 min)
- `BEG-045-L05` Boundaries and equivalence classes (10 min)
- `BEG-045-L06` Reading test failures (5 min)
- `BEG-045-L07` Demo: test-first on the bank's withdraw method (8 min)

#### BEG-057 · Verifying AI-generated code
*40 min video · 2.5 h practice* · Prerequisites: BEG-045, BEG-056 · added in v2.0

**Topics:** Reading and tracing generated code, testing it, plausible-but-wrong code, licensing and academic integrity

**Lessons:**
- `BEG-057-L01` Generated code is a draft, not an answer (8 min)
- `BEG-057-L02` Reading and tracing code you did not write (10 min)
- `BEG-057-L03` Testing generated code against the requirement (8 min)
- `BEG-057-L04` Licensing, integrity, and disclosure (6 min)
- `BEG-057-L05` Demo: catching a subtle bug in generated binary search with tests (8 min)

### BEG-P6 — Git, SQL, and Web Foundations

#### BEG-046 · Version control
*71 min video · 3 h practice* · Prerequisites: BEG-006

**Topics:** Repository, commits, staging, branches, merges, conflicts, .gitignore

**Lessons:**
- `BEG-046-L01` Why version control (7 min)
- `BEG-046-L02` Repositories, staging, and commits (12 min)
- `BEG-046-L03` History and diffs (8 min)
- `BEG-046-L04` Branches (10 min)
- `BEG-046-L05` Merging and conflicts (12 min)
- `BEG-046-L06` `.gitignore` (6 min)
- `BEG-046-L07` Demo: putting Bank Accounts under Git (8 min)
- `BEG-046-L08` Demo: creating and resolving a merge conflict (8 min)

#### BEG-047 · GitHub
*48 min video · 2 h practice* · Prerequisites: BEG-046

**Topics:** Remote repositories, push/pull, pull requests, README, Markdown

**Lessons:**
- `BEG-047-L01` Remotes, push, and pull (10 min)
- `BEG-047-L02` Authentication with GitHub (SSH keys or tokens) (8 min)
- `BEG-047-L03` Pull requests and reviews (12 min)
- `BEG-047-L04` Markdown and a good README (10 min)
- `BEG-047-L05` Demo: publishing a project and reviewing a pull request (8 min)

#### BEG-048 · Data fundamentals
*38 min video · 1 h practice* · Prerequisites: BEG-002

**Topics:** Structured data, relational vs nonrelational databases, DBMS, schemas

**Lessons:**
- `BEG-048-L01` Why databases (8 min)
- `BEG-048-L02` Structured vs unstructured data (7 min)
- `BEG-048-L03` Relational vs nonrelational (8 min)
- `BEG-048-L04` DBMS and schemas (7 min)
- `BEG-048-L05` Demo: why the contacts CSV breaks at scale (8 min)

#### BEG-049 · Relational modeling
*58 min video · 3 h practice* · Prerequisites: BEG-048

**Topics:** Tables, columns, rows, primary/foreign keys, relationships, normalization basics

**Lessons:**
- `BEG-049-L01` Tables, rows, and columns (8 min)
- `BEG-049-L02` Primary keys (8 min)
- `BEG-049-L03` Foreign keys and relationships (12 min)
- `BEG-049-L04` Many-to-many (8 min)
- `BEG-049-L05` Normalization in practice (14 min)
- `BEG-049-L06` Demo: normalizing a library spreadsheet into tables (8 min)

#### BEG-050 · SQL foundations
*91 min video · 6 h practice* · Prerequisites: BEG-049

**Topics:** DDL, DML, SELECT, WHERE, ORDER BY, GROUP BY, HAVING, JOINs, subqueries

**Lessons:**
- `BEG-050-L01` SQL overview: DDL vs DML (7 min)
- `BEG-050-L02` `CREATE` and `ALTER` (10 min)
- `BEG-050-L03` `INSERT`, `UPDATE`, `DELETE` (10 min)
- `BEG-050-L04` `SELECT`, `WHERE`, `ORDER BY` (10 min)
- `BEG-050-L05` Aggregates, `GROUP BY`, `HAVING` (12 min)
- `BEG-050-L06` Joins (15 min)
- `BEG-050-L07` Subqueries (11 min)
- `BEG-050-L08` Demo: answering library questions with SQL (8 min)
- `BEG-050-L09` Demo: joins that silently drop rows (8 min)

#### BEG-051 · PostgreSQL basics
*53 min video · 3 h practice* · Prerequisites: BEG-005, BEG-050

**Topics:** Installation, pgAdmin/DBeaver, schemas, constraints, CRUD, transactions introduction

**Lessons:**
- `BEG-051-L01` Installing PostgreSQL (10 min)
- `BEG-051-L02` `psql` and a GUI client (10 min)
- `BEG-051-L03` Databases, schemas, and users (8 min)
- `BEG-051-L04` Constraints that protect data (10 min)
- `BEG-051-L05` First look at transactions (7 min)
- `BEG-051-L06` Demo: creating the Library database with constraints (8 min)

#### BEG-052 · Web fundamentals
*58 min video · 2 h practice* · Prerequisites: BEG-003

**Topics:** HTTP methods, status codes, headers, JSON, URLs, query parameters, request body

**Lessons:**
- `BEG-052-L01` Anatomy of an HTTP request (10 min)
- `BEG-052-L02` Methods: GET, POST, PUT, PATCH, DELETE (10 min)
- `BEG-052-L03` Status codes (8 min)
- `BEG-052-L04` Headers (7 min)
- `BEG-052-L05` JSON (8 min)
- `BEG-052-L06` URLs and query parameters (7 min)
- `BEG-052-L07` Demo: reading real HTTP traffic in the browser (8 min)

#### BEG-053 · API fundamentals
*48 min video · 2 h practice* · Prerequisites: BEG-052

**Topics:** REST concepts, endpoint design, Postman, request/response examples

**Lessons:**
- `BEG-053-L01` What an API is (8 min)
- `BEG-053-L02` REST in plain language (10 min)
- `BEG-053-L03` Postman tour (10 min)
- `BEG-053-L04` `curl` from the terminal (6 min)
- `BEG-053-L05` Sketching endpoints for a resource (6 min)
- `BEG-053-L06` Demo: exploring a public API with Postman and curl (8 min)

#### BEG-054 · Build tools
*53 min video · 2.5 h practice* · Prerequisites: BEG-006, BEG-045

**Topics:** Maven basics, pom.xml, dependencies, build lifecycle, running tests

**Lessons:**
- `BEG-054-L01` Why build tools (7 min)
- `BEG-054-L02` Project structure and `pom.xml` (12 min)
- `BEG-054-L03` Dependencies and Maven Central (10 min)
- `BEG-054-L04` The build lifecycle (10 min)
- `BEG-054-L05` Running tests with Maven (6 min)
- `BEG-054-L06` Demo: converting a project to Maven (8 min)

#### BEG-055 · JDBC essentials
*66 min video · 3 h practice* · Prerequisites: BEG-029, BEG-051, BEG-054 · added in v2.0

**Topics:** Driver dependency, DriverManager, Connection, PreparedStatement, ResultSet, try-with-resources, SQL injection

**Lessons:**
- `BEG-055-L01` How Java talks to a database (8 min)
- `BEG-055-L02` Connecting: driver, URL, credentials from environment variables (10 min)
- `BEG-055-L03` Querying and mapping rows to objects (12 min)
- `BEG-055-L04` SQL injection, live (10 min)
- `BEG-055-L05` Transactions from Java (10 min)
- `BEG-055-L06` Demo: building the BookRepository with JDBC (8 min)
- `BEG-055-L07` Demo: SQL injection, then the PreparedStatement fix (8 min)

---

## Level 2 — Junior Java Backend Engineer (`JNR`)

- **Audience:** Graduates of Level 1 or self-taught programmers who pass the Level 2 diagnostic.
- **Graduation outcome:** Implements, tests, secures, and deploys a maintainable backend application within an existing architecture, collaborates using Git, and handles straightforward production defects with guidance.
- **Study hours:** 250–350 · **Video hours:** 50–70 · **Lessons:** 160–210
- **Capstone:** `JNR-CAP` E-Commerce Backend API: Modular layered monolith with registration, login, catalog, inventory, cart, orders, mock payments, administration; OpenAPI, migrations, tests, Docker Compose, CI, deployment, structured logs.
- **Graduation gate:** Given a feature request, implements it independently within the established architecture, writes meaningful tests, explains the database changes, and delivers a reviewable pull request.

### JNR-P1 — Professional Java Development

#### JNR-001 · Modern Java
*80 min video · 4 h · `version:` current LTS practice* · Prerequisites: BEG-012, BEG-024, BEG-026

**Topics:** Release cadence, LTS versions, records, sealed classes, switch expressions, text blocks, pattern matching

**Lessons:**
- `JNR-001-L01` Java's release model and LTS versions (8 min)
- `JNR-001-L02` Records (12 min)
- `JNR-001-L03` Sealed classes and interfaces (10 min)
- `JNR-001-L04` Switch expressions and pattern matching (15 min)
- `JNR-001-L05` Record patterns (10 min)
- `JNR-001-L06` Text blocks and other small wins (7 min)
- `JNR-001-L07` What changed since the last LTS (updated per release) (8 min)
- `JNR-001-L08` Demo: modernizing a legacy Java class step by step (10 min)

#### JNR-002 · Maven in depth
*70 min video · 3 h practice* · Prerequisites: BEG-054

**Topics:** Dependency scopes, transitive dependencies, BOMs, plugins, multi-module basics, reproducible builds

**Lessons:**
- `JNR-002-L01` Dependency scopes (8 min)
- `JNR-002-L02` Transitive dependencies and `dependency:tree` (10 min)
- `JNR-002-L03` Version conflicts and dependency management (10 min)
- `JNR-002-L04` BOMs (7 min)
- `JNR-002-L05` Plugins and the build lifecycle revisited (10 min)
- `JNR-002-L06` Multi-module projects (10 min)
- `JNR-002-L07` Reproducible builds and the Maven Wrapper (5 min)
- `JNR-002-L08` Demo: untangling a dependency conflict with `dependency:tree` (10 min)

#### JNR-003 · Code quality
*65 min video · 3 h practice* · Prerequisites: BEG-028

**Topics:** Naming, cohesion, coupling, DRY, KISS, YAGNI, code smells

**Lessons:**
- `JNR-003-L01` Code is read more than written (6 min)
- `JNR-003-L02` Naming (10 min)
- `JNR-003-L03` Cohesion and coupling (10 min)
- `JNR-003-L04` DRY, KISS, YAGNI — and their limits (9 min)
- `JNR-003-L05` A catalog of code smells (12 min)
- `JNR-003-L06` Safe refactoring with the IDE (8 min)
- `JNR-003-L07` Demo: refactoring a long method under green tests (10 min)

#### JNR-055 · AI-assisted development workflow
*62 min video · 2.5 h practice* · Prerequisites: BEG-057, JNR-003 · added in v2.0

**Topics:** IDE assistants, context-rich prompts, generating tests and boilerplate, reviewing AI code in pull requests, protecting proprietary code, team policy

**Lessons:**
- `JNR-055-L01` Assistants in the professional workflow (10 min)
- `JNR-055-L02` Prompts with context: code, constraints, conventions (12 min)
- `JNR-055-L03` AI for tests and boilerplate, and how to review it (10 min)
- `JNR-055-L04` Reviewing AI-assisted pull requests (10 min)
- `JNR-055-L05` Team policies: code privacy, secrets, licenses (8 min)
- `JNR-055-L06` Demo: refactoring a long method with an assistant under green tests (12 min)

#### JNR-004 · SOLID principles
*70 min video · 3 h practice* · Prerequisites: BEG-024, JNR-003

**Topics:** SRP, OCP, LSP, ISP, DIP with practical Java examples

**Lessons:**
- `JNR-004-L01` Single Responsibility (12 min)
- `JNR-004-L02` Open/Closed (10 min)
- `JNR-004-L03` Liskov Substitution (10 min)
- `JNR-004-L04` Interface Segregation (8 min)
- `JNR-004-L05` Dependency Inversion (12 min)
- `JNR-004-L06` SOLID with judgment (8 min)
- `JNR-004-L07` Demo: dependency inversion for a payment provider (10 min)

#### JNR-005 · Design patterns introduction
*85 min video · 4 h practice* · Prerequisites: JNR-004

**Topics:** Factory, Builder, Strategy, Adapter, Decorator, Observer, Repository

**Lessons:**
- `JNR-005-L01` What patterns are (and are not) (6 min)
- `JNR-005-L02` Factory (9 min)
- `JNR-005-L03` Builder (9 min)
- `JNR-005-L04` Strategy (10 min)
- `JNR-005-L05` Adapter (9 min)
- `JNR-005-L06` Decorator (10 min)
- `JNR-005-L07` Observer (10 min)
- `JNR-005-L08` Repository (7 min)
- `JNR-005-L09` Spotting patterns in Spring (5 min)
- `JNR-005-L10` Demo: replacing a type switch with Strategy (10 min)

#### JNR-006 · Logging
*55 min video · 2 h practice* · Prerequisites: BEG-029, JNR-002

**Topics:** SLF4J, Logback, log levels, structured messages, avoiding sensitive data

**Lessons:**
- `JNR-006-L01` Why `System.out` is not logging (6 min)
- `JNR-006-L02` SLF4J and Logback (10 min)
- `JNR-006-L03` Choosing log levels (8 min)
- `JNR-006-L04` Logging exceptions well (7 min)
- `JNR-006-L05` Sensitive data in logs (7 min)
- `JNR-006-L06` Structured logging (7 min)
- `JNR-006-L07` Demo: from `println` to structured JSON logs (10 min)

#### JNR-007 · Configuration
*50 min video · 2 h practice* · Prerequisites: BEG-006, BEG-034

**Topics:** Properties, YAML, profiles, environment variables, externalized configuration

**Lessons:**
- `JNR-007-L01` Why externalize configuration (7 min)
- `JNR-007-L02` Properties and YAML (10 min)
- `JNR-007-L03` Environment variables and system properties (8 min)
- `JNR-007-L04` Profiles and precedence (8 min)
- `JNR-007-L05` Secrets do not belong in Git (7 min)
- `JNR-007-L06` Demo: one JAR, three environments (10 min)

### JNR-P2 — Spring Framework Fundamentals

#### JNR-008 · Spring ecosystem
*40 min video · 1 h practice* · Prerequisites: JNR-002

**Topics:** Spring Framework vs Spring Boot vs Spring Data vs Spring Security

**Lessons:**
- `JNR-008-L01` Why frameworks exist (7 min)
- `JNR-008-L02` The Spring family (10 min)
- `JNR-008-L03` Spring Initializr walkthrough (8 min)
- `JNR-008-L04` Reading Spring's documentation (5 min)
- `JNR-008-L05` Demo: first Spring Boot app from Initializr to running endpoint (10 min)

#### JNR-009 · IoC and DI
*74 min video · 3 h practice* · Prerequisites: JNR-004, JNR-008

**Topics:** Inversion of Control, dependency injection, constructor injection, bean lifecycle

**Lessons:**
- `JNR-009-L01` Wiring by hand: the problem (8 min)
- `JNR-009-L02` Inversion of control (8 min)
- `JNR-009-L03` Constructor injection (10 min)
- `JNR-009-L04` Multiple implementations (10 min)
- `JNR-009-L05` Bean lifecycle and callbacks (8 min)
- `JNR-009-L06` Circular dependencies and how to avoid them (6 min)
- `JNR-009-L07` Demo: wiring Shop Core by hand, then with Spring (12 min)
- `JNR-009-L08` Demo: diagnosing an ambiguous-bean startup failure (12 min)

#### JNR-010 · Spring container
*55 min video · 2 h practice* · Prerequisites: JNR-009

**Topics:** ApplicationContext, bean scopes, component scanning, stereotypes

**Lessons:**
- `JNR-010-L01` The ApplicationContext (8 min)
- `JNR-010-L02` Component scanning and stereotypes (10 min)
- `JNR-010-L03` `@Configuration` and `@Bean` (10 min)
- `JNR-010-L04` Bean scopes (8 min)
- `JNR-010-L05` Stateless singletons and thread safety (9 min)
- `JNR-010-L06` Demo: injecting a `Clock` to test time-dependent logic (10 min)

#### JNR-011 · Spring Boot
*74 min video · 2 h practice* · Prerequisites: JNR-010

**Topics:** Starters, auto-configuration, project structure, embedded servers

**Lessons:**
- `JNR-011-L01` What Boot adds to Spring (8 min)
- `JNR-011-L02` Starters (7 min)
- `JNR-011-L03` Auto-configuration and conditions (12 min)
- `JNR-011-L04` Overriding defaults (8 min)
- `JNR-011-L05` Embedded servers and executable JARs (8 min)
- `JNR-011-L06` Project structure conventions (7 min)
- `JNR-011-L07` Demo: reading the conditions evaluation report (12 min)
- `JNR-011-L08` Demo: overriding Jackson's auto-configuration (12 min)

#### JNR-012 · Configuration management
*50 min video · 2 h practice* · Prerequisites: JNR-007, JNR-011

**Topics:** application.yml, profiles, @ConfigurationProperties, validation

**Lessons:**
- `JNR-012-L01` `application.yml` and profiles (10 min)
- `JNR-012-L02` Typed configuration with `@ConfigurationProperties` (12 min)
- `JNR-012-L03` Validating configuration (8 min)
- `JNR-012-L04` Property-source precedence (10 min)
- `JNR-012-L05` Demo: typed, validated `ShopProperties` that fail fast (10 min)

#### JNR-013 · Layered architecture
*79 min video · 4 h practice* · Prerequisites: BEG-027, JNR-011

**Topics:** Controller, service, repository, DTO, domain/entity models

**Lessons:**
- `JNR-013-L01` Why layers (8 min)
- `JNR-013-L02` Controllers: the HTTP edge (10 min)
- `JNR-013-L03` Services: business logic and orchestration (10 min)
- `JNR-013-L04` Repositories: data access behind an interface (8 min)
- `JNR-013-L05` DTOs vs domain models (12 min)
- `JNR-013-L06` Package by feature, layer within (7 min)
- `JNR-013-L07` Demo: building the products feature layer by layer (12 min)
- `JNR-013-L08` Demo: separating DTOs from domain models (12 min)

#### JNR-014 · Validation
*50 min video · 2 h practice* · Prerequisites: JNR-013

**Topics:** Jakarta Bean Validation, custom validators, input sanitization

**Lessons:**
- `JNR-014-L01` Validating at the edge (8 min)
- `JNR-014-L02` Built-in constraints (10 min)
- `JNR-014-L03` Custom constraints (10 min)
- `JNR-014-L04` Input validation vs business rules (7 min)
- `JNR-014-L05` Sanitization and why validation is not escaping (5 min)
- `JNR-014-L06` Demo: writing a custom `@ValidSku` constraint (10 min)

#### JNR-015 · Error handling
*50 min video · 2 h practice* · Prerequisites: BEG-029, JNR-013

**Topics:** Custom exceptions, @ControllerAdvice, consistent API error responses

**Lessons:**
- `JNR-015-L01` Errors are part of the API (7 min)
- `JNR-015-L02` Application exception hierarchy (8 min)
- `JNR-015-L03` `@RestControllerAdvice` (10 min)
- `JNR-015-L04` Problem Details (8 min)
- `JNR-015-L05` What not to tell the client (7 min)
- `JNR-015-L06` Demo: centralized Problem Details error handling (10 min)

#### JNR-016 · Spring testing basics
*74 min video · 3 h practice* · Prerequisites: BEG-045, JNR-013

**Topics:** Spring test context, test slices, Mockito, MockMvc

**Lessons:**
- `JNR-016-L01` Testing pyramid for Spring apps (8 min)
- `JNR-016-L02` Plain unit tests for services (8 min)
- `JNR-016-L03` Mockito in five minutes (7 min)
- `JNR-016-L04` `@WebMvcTest` and MockMvc (15 min)
- `JNR-016-L05` `@SpringBootTest` and context caching (12 min)
- `JNR-016-L06` Demo: test-driving a controller with `@WebMvcTest` (12 min)
- `JNR-016-L07` Demo: slice vs full-context tests, timed (12 min)

### JNR-P3 — REST API Engineering

#### JNR-017 · HTTP in depth
*65 min video · 2 h practice* · Prerequisites: BEG-052

**Topics:** Methods, idempotency, safe methods, headers, content negotiation, caching

**Lessons:**
- `JNR-017-L01` Methods revisited: safety and idempotency (12 min)
- `JNR-017-L02` Headers that matter to backend engineers (10 min)
- `JNR-017-L03` Content negotiation (8 min)
- `JNR-017-L04` Caching and conditional requests (15 min)
- `JNR-017-L05` HTTP/1.1, HTTP/2, HTTP/3 in brief (10 min)
- `JNR-017-L06` Demo: conditional GET with ETags and curl (10 min)

#### JNR-018 · RESTful design
*60 min video · 3 h practice* · Prerequisites: BEG-053, JNR-017

**Topics:** Resource modeling, URLs, status codes, request/response contracts

**Lessons:**
- `JNR-018-L01` Resources, not functions (10 min)
- `JNR-018-L02` URL design (10 min)
- `JNR-018-L03` Choosing status codes (10 min)
- `JNR-018-L04` Modeling actions (checkout, cancel) (10 min)
- `JNR-018-L05` Contract-first design (10 min)
- `JNR-018-L06` Demo: designing the Shop API contract on a whiteboard (10 min)

#### JNR-019 · CRUD APIs
*84 min video · 5 h practice* · Prerequisites: JNR-013, JNR-018

**Topics:** Controllers, request bodies, path/query parameters, pagination, sorting

**Lessons:**
- `JNR-019-L01` Create: POST, 201, Location (10 min)
- `JNR-019-L02` Read: single and collection (8 min)
- `JNR-019-L03` Update: PUT vs PATCH (12 min)
- `JNR-019-L04` Delete (6 min)
- `JNR-019-L05` Pagination (12 min)
- `JNR-019-L06` Sorting and its safety limits (12 min)
- `JNR-019-L07` Demo: full CRUD for categories, live (12 min)
- `JNR-019-L08` Demo: safe pagination and sorting (12 min)

#### JNR-020 · API design conventions
*55 min video · 3 h practice* · Prerequisites: JNR-019

**Topics:** DTOs, mapping, consistent errors, filtering, versioning strategies

**Lessons:**
- `JNR-020-L01` Consistency is a feature (7 min)
- `JNR-020-L02` DTO mapping approaches (10 min)
- `JNR-020-L03` Representing money, dates, and enums (10 min)
- `JNR-020-L04` Filtering (8 min)
- `JNR-020-L05` Versioning strategies (10 min)
- `JNR-020-L06` Demo: enforcing the Shop API style guide (10 min)

#### JNR-021 · OpenAPI
*50 min video · 2 h practice* · Prerequisites: JNR-020

**Topics:** Swagger UI, OpenAPI specification, examples, API documentation

**Lessons:**
- `JNR-021-L01` The OpenAPI specification (10 min)
- `JNR-021-L02` Generating docs from Spring (springdoc) (10 min)
- `JNR-021-L03` Examples and error responses (10 min)
- `JNR-021-L04` Code-first vs contract-first (10 min)
- `JNR-021-L05` Demo: from bare springdoc output to a usable API reference (10 min)

#### JNR-022 · API clients
*40 min video · 1.5 h practice* · Prerequisites: BEG-053, JNR-019

**Topics:** Postman, curl, API collections, environment variables

**Lessons:**
- `JNR-022-L01` Postman collections and environments (8 min)
- `JNR-022-L02` Scripts and chained requests (8 min)
- `JNR-022-L03` `curl` fluency (6 min)
- `JNR-022-L04` Calling other APIs from Spring (8 min)
- `JNR-022-L05` Demo: a chained Postman collection with environments (10 min)

#### JNR-056 · Calling LLMs from Spring
*74 min video · 3 h · `version:` current Spring AI practice* · Prerequisites: JNR-012, JNR-022 · added in v2.0

**Topics:** Spring AI ChatClient, system prompts, structured output to records, streaming, timeouts and retries, token cost, API key handling, testing with a fake model

**Lessons:**
- `JNR-056-L01` What happens in an LLM API call (10 min)
- `JNR-056-L02` Spring AI concepts: ChatClient, prompts, advisors (12 min)
- `JNR-056-L03` Structured output to records, and validating it (12 min)
- `JNR-056-L04` Streaming responses (10 min)
- `JNR-056-L05` Timeouts, retries, and token budgets (10 min)
- `JNR-056-L06` Keys, configuration, and testing with a fake model (8 min)
- `JNR-056-L07` Demo: an AI product-description helper for Shop API (12 min)

#### JNR-023 · File operations
*50 min video · 2 h practice* · Prerequisites: BEG-034, JNR-019

**Topics:** Multipart uploads, downloads, streaming, file-size restrictions

**Lessons:**
- `JNR-023-L01` Multipart uploads (10 min)
- `JNR-023-L02` Limits and validation (8 min)
- `JNR-023-L03` Streaming downloads (10 min)
- `JNR-023-L04` Where to store files (7 min)
- `JNR-023-L05` Upload security (5 min)
- `JNR-023-L06` Demo: product image upload and streaming download (10 min)

#### JNR-024 · API security fundamentals
*55 min video · 1.5 h practice* · Prerequisites: JNR-017

**Topics:** Authentication vs authorization, session vs token, HTTPS, CORS, CSRF concepts

**Lessons:**
- `JNR-024-L01` Who are you vs what may you do (8 min)
- `JNR-024-L02` Sessions vs tokens (10 min)
- `JNR-024-L03` HTTPS for APIs (7 min)
- `JNR-024-L04` CORS demystified (10 min)
- `JNR-024-L05` CSRF and when it applies (10 min)
- `JNR-024-L06` Demo: watching CORS fail and fixing it (10 min)

### JNR-P4 — Database Integration

#### JNR-025 · JDBC
*50 min video · 2 h practice* · Prerequisites: BEG-055

**Topics:** Connections, PreparedStatement, ResultSet, SQL injection prevention (builds on BEG-055)

**Lessons:**
- `JNR-025-L01` From `DriverManager` to `DataSource` (8 min)
- `JNR-025-L02` Generated keys and batching (10 min)
- `JNR-025-L03` Type mapping pitfalls (10 min)
- `JNR-025-L04` Dynamic SQL without injection (12 min)
- `JNR-025-L05` Demo: batch import and timing comparison (10 min)

#### JNR-026 · Spring JDBC
*50 min video · 2.5 h practice* · Prerequisites: JNR-011, JNR-025

**Topics:** JdbcTemplate, parameter binding, mapping query results

**Lessons:**
- `JNR-026-L01` DataSource configuration in Boot (8 min)
- `JNR-026-L02` `JdbcClient` and `JdbcTemplate` (12 min)
- `JNR-026-L03` Mapping rows (10 min)
- `JNR-026-L04` Exception translation (10 min)
- `JNR-026-L05` Demo: replacing the in-memory repository with Spring JDBC (10 min)

#### JNR-027 · ORM fundamentals
*45 min video · 1 h practice* · Prerequisites: JNR-026

**Topics:** Object-relational impedance mismatch, persistence context

**Lessons:**
- `JNR-027-L01` Objects vs tables (10 min)
- `JNR-027-L02` What an ORM does (10 min)
- `JNR-027-L03` The persistence context (15 min)
- `JNR-027-L04` Demo: watching the persistence context with SQL logging (10 min)

#### JNR-028 · JPA and Hibernate
*84 min video · 4 h practice* · Prerequisites: JNR-027

**Topics:** Entities, identifiers, relationships, entity lifecycle, dirty checking

**Lessons:**
- `JNR-028-L01` Mapping an entity (12 min)
- `JNR-028-L02` Identifiers and generation strategies (10 min)
- `JNR-028-L03` Embeddables and value objects (8 min)
- `JNR-028-L04` Entity lifecycle (12 min)
- `JNR-028-L05` Dirty checking and flushing (10 min)
- `JNR-028-L06` Entity equality (8 min)
- `JNR-028-L07` Demo: mapping Shop entities and predicting the SQL (12 min)
- `JNR-028-L08` Demo: entity states in the debugger (12 min)

#### JNR-029 · Spring Data JPA
*74 min video · 3 h practice* · Prerequisites: JNR-028

**Topics:** Repositories, derived queries, JPQL, native queries

**Lessons:**
- `JNR-029-L01` Repository interfaces (10 min)
- `JNR-029-L02` Derived queries (10 min)
- `JNR-029-L03` JPQL with `@Query` (10 min)
- `JNR-029-L04` Native queries (8 min)
- `JNR-029-L05` Projections and paging (12 min)
- `JNR-029-L06` Demo: migrating the catalog to Spring Data JPA (12 min)
- `JNR-029-L07` Demo: projections for paged listings (12 min)

#### JNR-030 · Entity relationships
*79 min video · 4 h practice* · Prerequisites: BEG-049, JNR-029

**Topics:** One-to-one, one-to-many, many-to-one, many-to-many, cascade, orphan removal

**Lessons:**
- `JNR-030-L01` Many-to-one: the default relationship (10 min)
- `JNR-030-L02` One-to-many and the owning side (12 min)
- `JNR-030-L03` One-to-one (7 min)
- `JNR-030-L04` Many-to-many and join entities (10 min)
- `JNR-030-L05` Cascades and orphan removal (10 min)
- `JNR-030-L06` Unidirectional by default (6 min)
- `JNR-030-L07` Demo: mapping Order and OrderLine as an aggregate (12 min)
- `JNR-030-L08` Demo: cascade and orphan-removal surprises (12 min)

#### JNR-031 · Transactions
*79 min video · 3 h practice* · Prerequisites: BEG-051, JNR-029

**Topics:** ACID, transaction boundaries, @Transactional, rollback rules

**Lessons:**
- `JNR-031-L01` ACID by example (10 min)
- `JNR-031-L02` Transaction boundaries (10 min)
- `JNR-031-L03` `@Transactional` and proxies (12 min)
- `JNR-031-L04` Rollback rules (8 min)
- `JNR-031-L05` Propagation basics (8 min)
- `JNR-031-L06` Long transactions and remote calls (7 min)
- `JNR-031-L07` Demo: making checkout atomic (12 min)
- `JNR-031-L08` Demo: finding the self-invocation bug (12 min)

#### JNR-032 · ORM pitfalls
*74 min video · 3 h practice* · Prerequisites: JNR-030

**Topics:** N+1 queries, lazy/eager loading, pagination pitfalls, fetching strategies

**Lessons:**
- `JNR-032-L01` The N+1 problem (12 min)
- `JNR-032-L02` Fetch joins and entity graphs (12 min)
- `JNR-032-L03` Lazy loading and its exception (10 min)
- `JNR-032-L04` Pagination with collections (8 min)
- `JNR-032-L05` Open Session in View: why to turn it off (8 min)
- `JNR-032-L06` Demo: catching N+1 with a query-count test (12 min)
- `JNR-032-L07` Demo: fixing lazy loading without Open Session in View (12 min)

#### JNR-033 · Schema migrations
*50 min video · 2 h practice* · Prerequisites: BEG-051, JNR-028

**Topics:** Flyway or Liquibase, versioned migrations, seed data

**Lessons:**
- `JNR-033-L01` Why the schema needs version control (8 min)
- `JNR-033-L02` Flyway basics (12 min)
- `JNR-033-L03` Writing safe migrations (10 min)
- `JNR-033-L04` Seed data (5 min)
- `JNR-033-L05` Liquibase in brief (5 min)
- `JNR-033-L06` Demo: baselining Shop with Flyway and adding V2 (10 min)

#### JNR-034 · Database constraints
*50 min video · 2 h practice* · Prerequisites: JNR-033

**Topics:** Unique, foreign keys, check constraints, indexes introduction

**Lessons:**
- `JNR-034-L01` The database as the last line of defense (8 min)
- `JNR-034-L02` Unique and check constraints (10 min)
- `JNR-034-L03` Constraint violations to API errors (8 min)
- `JNR-034-L04` Indexes: a first look (14 min)
- `JNR-034-L05` Demo: racing two requests against a unique constraint (10 min)

### JNR-P5 — Authentication and Application Security

#### JNR-035 · Security fundamentals
*50 min video · 1.5 h practice* · Prerequisites: JNR-024

**Topics:** Threats, trust boundaries, least privilege, defense in depth

**Lessons:**
- `JNR-035-L01` Thinking like an attacker (8 min)
- `JNR-035-L02` Confidentiality, integrity, availability (8 min)
- `JNR-035-L03` Trust boundaries (10 min)
- `JNR-035-L04` Least privilege and defense in depth (8 min)
- `JNR-035-L05` A first threat list (6 min)
- `JNR-035-L06` Demo: drawing Shop's trust boundaries (10 min)

#### JNR-036 · Spring Security
*84 min video · 4 h practice* · Prerequisites: JNR-011, JNR-035

**Topics:** SecurityFilterChain, filter chain, request authorization

**Lessons:**
- `JNR-036-L01` Filters and the security filter chain (12 min)
- `JNR-036-L02` Configuring `SecurityFilterChain` (12 min)
- `JNR-036-L03` Users from the database (10 min)
- `JNR-036-L04` 401 vs 403 and error bodies (8 min)
- `JNR-036-L05` Testing security (10 min)
- `JNR-036-L06` Reading Spring Security's debug output (8 min)
- `JNR-036-L07` Demo: securing the Shop API endpoint by endpoint (12 min)
- `JNR-036-L08` Demo: testing the access matrix (12 min)

#### JNR-037 · Password security
*45 min video · 2 h practice* · Prerequisites: JNR-036

**Topics:** Password hashing, salts, adaptive algorithms, account lockout

**Lessons:**
- `JNR-037-L01` How passwords get stolen (8 min)
- `JNR-037-L02` Hashing, salting, and slow hashes (10 min)
- `JNR-037-L03` `PasswordEncoder` and upgrades (7 min)
- `JNR-037-L04` Brute force, lockout, and throttling (10 min)
- `JNR-037-L05` Demo: registration with password hashing and throttling (10 min)

#### JNR-038 · Sessions and tokens
*74 min video · 3 h practice* · Prerequisites: JNR-024, JNR-036

**Topics:** Cookies, sessions, bearer tokens, JWT structure and validation

**Lessons:**
- `JNR-038-L01` Cookies and server sessions (10 min)
- `JNR-038-L02` Bearer tokens (7 min)
- `JNR-038-L03` Inside a JWT (10 min)
- `JNR-038-L04` Validating tokens correctly (12 min)
- `JNR-038-L05` Expiry, refresh, and revocation (11 min)
- `JNR-038-L06` Demo: issuing and validating JWTs (12 min)
- `JNR-038-L07` Demo: attacking token validation (tampering, expiry, audience) (12 min)

#### JNR-039 · OAuth 2.0 and OIDC basics
*74 min video · 2.5 h practice* · Prerequisites: JNR-038

**Topics:** Roles, flows, authorization server, resource server, login vs API authorization

**Lessons:**
- `JNR-039-L01` The problem OAuth solves (8 min)
- `JNR-039-L02` Roles and tokens (8 min)
- `JNR-039-L03` Authorization code + PKCE (12 min)
- `JNR-039-L04` Client credentials (7 min)
- `JNR-039-L05` OIDC: adding login (8 min)
- `JNR-039-L06` Spring as a resource server (7 min)
- `JNR-039-L07` Demo: Keycloak setup and the authorization code + PKCE flow (12 min)
- `JNR-039-L08` Demo: switching Shop to Keycloak-issued tokens (12 min)

#### JNR-040 · Role-based authorization
*64 min video · 2.5 h practice* · Prerequisites: JNR-029, JNR-036

**Topics:** RBAC, method security, ownership checks

**Lessons:**
- `JNR-040-L01` Roles, authorities, permissions (8 min)
- `JNR-040-L02` Method security (10 min)
- `JNR-040-L03` Ownership checks (12 min)
- `JNR-040-L04` IDOR: the most common API bug (10 min)
- `JNR-040-L05` Demo: finding and fixing an IDOR (12 min)
- `JNR-040-L06` Demo: method security with ownership checks (12 min)

#### JNR-041 · Common vulnerabilities
*65 min video · 2.5 h practice* · Prerequisites: JNR-025, JNR-035

**Topics:** OWASP Top 10, injection, broken access control, XSS, CSRF, SSRF introduction

**Lessons:**
- `JNR-041-L01` The OWASP Top 10 tour (12 min)
- `JNR-041-L02` Injection beyond SQL (10 min)
- `JNR-041-L03` Mass assignment (8 min)
- `JNR-041-L04` XSS from the backend's view (8 min)
- `JNR-041-L05` CSRF revisited (7 min)
- `JNR-041-L06` SSRF (10 min)
- `JNR-041-L07` Demo: exploiting and fixing mass assignment and SSRF (10 min)

#### JNR-057 · Securing LLM features
*62 min video · 2.5 h practice* · Prerequisites: JNR-041, JNR-056 · added in v2.0

**Topics:** Prompt injection, untrusted model output, sensitive data leakage, OWASP Top 10 for LLM applications

**Lessons:**
- `JNR-057-L01` Why LLM features need their own threat list (10 min)
- `JNR-057-L02` Prompt injection and the limits of defense (12 min)
- `JNR-057-L03` Model output is untrusted input (10 min)
- `JNR-057-L04` Sensitive data in prompts and logs (10 min)
- `JNR-057-L05` Limiting cost and abuse (8 min)
- `JNR-057-L06` Demo: injecting the Shop helper, then hardening it (12 min)

#### JNR-042 · Secure configuration
*45 min video · 2 h practice* · Prerequisites: JNR-006, JNR-012

**Topics:** Secrets management basics, HTTPS, dependency updates, secure logging

**Lessons:**
- `JNR-042-L01` Secrets management basics (8 min)
- `JNR-042-L02` HTTPS and security headers (8 min)
- `JNR-042-L03` Locking down Actuator (6 min)
- `JNR-042-L04` Vulnerable dependencies (8 min)
- `JNR-042-L05` Secure logging checklist (5 min)
- `JNR-042-L06` Demo: hardening the prod profile (10 min)

### JNR-P6 — Testing and Delivery

#### JNR-043 · Unit testing
*60 min video · 3 h · `version:` current JUnit Jupiter practice* · Prerequisites: BEG-045

**Topics:** JUnit 5, test lifecycle, parameterized tests, assertions

**Lessons:**
- `JNR-043-L01` What a unit is (7 min)
- `JNR-043-L02` Lifecycle and structure (10 min)
- `JNR-043-L03` Parameterized tests (12 min)
- `JNR-043-L04` AssertJ (12 min)
- `JNR-043-L05` Coverage and its limits (9 min)
- `JNR-043-L06` Demo: turning copy-pasted tests into a parameterized table (10 min)

#### JNR-044 · Mocking
*55 min video · 2.5 h practice* · Prerequisites: JNR-009, JNR-043

**Topics:** Mockito, stubs, mocks, spies, interaction verification

**Lessons:**
- `JNR-044-L01` Test doubles taxonomy (8 min)
- `JNR-044-L02` Stubbing with Mockito (10 min)
- `JNR-044-L03` Verifying interactions (8 min)
- `JNR-044-L04` Argument captors (7 min)
- `JNR-044-L05` When not to mock (12 min)
- `JNR-044-L06` Demo: mocking the payment gateway's three outcomes (10 min)

#### JNR-048 · Linux basics
*65 min video · 3 h practice* · Prerequisites: BEG-006

**Topics:** Processes, permissions, SSH, ports, logs, service management

**Lessons:**
- `JNR-048-L01` Linux for backend engineers (7 min)
- `JNR-048-L02` Processes and resources (10 min)
- `JNR-048-L03` Users, permissions, ownership (10 min)
- `JNR-048-L04` SSH and keys (10 min)
- `JNR-048-L05` Ports and networking tools (8 min)
- `JNR-048-L06` Logs and services (10 min)
- `JNR-048-L07` Demo: running Shop as a systemd service (10 min)

#### JNR-049 · Docker fundamentals
*84 min video · 3 h practice* · Prerequisites: JNR-011, JNR-048

**Topics:** Images, containers, Dockerfiles, volumes, networking

**Lessons:**
- `JNR-049-L01` Why containers (8 min)
- `JNR-049-L02` Images, layers, registries (10 min)
- `JNR-049-L03` Running containers (10 min)
- `JNR-049-L04` Writing a Dockerfile for Spring Boot (14 min)
- `JNR-049-L05` Volumes and networks (10 min)
- `JNR-049-L06` Debugging containers (8 min)
- `JNR-049-L07` Demo: writing a multi-stage Dockerfile for Shop (12 min)
- `JNR-049-L08` Demo: debugging a crashing container (12 min)

#### JNR-050 · Docker Compose
*45 min video · 2 h practice* · Prerequisites: BEG-051, JNR-049

**Topics:** Spring Boot + PostgreSQL local environment

**Lessons:**
- `JNR-050-L01` Compose files (10 min)
- `JNR-050-L02` Health checks and startup order (8 min)
- `JNR-050-L03` Environment and secrets (7 min)
- `JNR-050-L04` Spring Boot's Compose integration (10 min)
- `JNR-050-L05` Demo: one-command Shop stack (10 min)

#### JNR-045 · Integration testing
*74 min video · 3 h practice* · Prerequisites: JNR-016, JNR-029, JNR-050

**Topics:** Spring Boot Test, real database testing, Testcontainers

**Lessons:**
- `JNR-045-L01` What integration tests prove (8 min)
- `JNR-045-L02` Testcontainers (12 min)
- `JNR-045-L03` Repository tests with `@DataJpaTest` (10 min)
- `JNR-045-L04` Full-application tests (10 min)
- `JNR-045-L05` Test data isolation (10 min)
- `JNR-045-L06` Demo: Testcontainers integration tests for Shop (12 min)
- `JNR-045-L07` Demo: fixing leaking test data (12 min)

#### JNR-046 · API testing
*50 min video · 2.5 h practice* · Prerequisites: JNR-019, JNR-045

**Topics:** MockMvc, REST Assured, success/failure scenarios

**Lessons:**
- `JNR-046-L01` MockMvc vs real HTTP (8 min)
- `JNR-046-L02` REST Assured (12 min)
- `JNR-046-L03` A scenario matrix for every endpoint (10 min)
- `JNR-046-L04` Testing secured endpoints (10 min)
- `JNR-046-L05` Demo: the checkout journey with REST Assured (10 min)

#### JNR-047 · Testing practices
*50 min video · 2 h practice* · Prerequisites: JNR-045

**Topics:** Arrange-Act-Assert, fixtures, test data, avoiding brittle tests

**Lessons:**
- `JNR-047-L01` Arrange-Act-Assert and naming (8 min)
- `JNR-047-L02` Test data builders (10 min)
- `JNR-047-L03` Flaky and brittle tests (12 min)
- `JNR-047-L04` Shaping a healthy suite (10 min)
- `JNR-047-L05` Demo: hunting a flaky test (10 min)

#### JNR-051 · CI/CD introduction
*69 min video · 3 h practice* · Prerequisites: BEG-047, JNR-045, JNR-049

**Topics:** GitHub Actions or GitLab CI, build/test pipeline, artifacts

**Lessons:**
- `JNR-051-L01` CI, CD, and CD (8 min)
- `JNR-051-L02` GitHub Actions anatomy (12 min)
- `JNR-051-L03` Build and test pipeline (10 min)
- `JNR-051-L04` Artifacts and image publishing (10 min)
- `JNR-051-L05` Branch protection (5 min)
- `JNR-051-L06` Demo: building the Shop pipeline in GitHub Actions (12 min)
- `JNR-051-L07` Demo: publishing a tagged image on merge (12 min)

#### JNR-052 · Deployment basics
*69 min video · 3 h practice* · Prerequisites: JNR-012, JNR-051

**Topics:** Executable JARs, container deployment, configuration, health checks

**Lessons:**
- `JNR-052-L01` From artifact to running service (8 min)
- `JNR-052-L02` Deployment targets compared (10 min)
- `JNR-052-L03` Configuration in deployed environments (8 min)
- `JNR-052-L04` Health checks: liveness vs readiness (10 min)
- `JNR-052-L05` Graceful shutdown and rollback (9 min)
- `JNR-052-L06` Demo: deploying Shop and its database (12 min)
- `JNR-052-L07` Demo: rolling back a bad release (12 min)

#### JNR-053 · Team workflows
*50 min video · 2 h practice* · Prerequisites: BEG-047

**Topics:** Branching, pull requests, code reviews, issue tracking, agile basics

**Lessons:**
- `JNR-053-L01` Branching strategies (8 min)
- `JNR-053-L02` Good pull requests (8 min)
- `JNR-053-L03` Code review as reviewer and author (12 min)
- `JNR-053-L04` Issues, boards, and agile basics (12 min)
- `JNR-053-L05` Demo: a pull request from issue to merge (10 min)

#### JNR-054 · Troubleshooting
*55 min video · 3 h practice* · Prerequisites: BEG-018, JNR-006, JNR-052

**Topics:** Reading logs, reproducing bugs, stack traces, environment differences

**Lessons:**
- `JNR-054-L01` A troubleshooting method (8 min)
- `JNR-054-L02` Logs and stack traces in production (12 min)
- `JNR-054-L03` Environment differences (10 min)
- `JNR-054-L04` From bug to regression test (8 min)
- `JNR-054-L05` Asking for help well (7 min)
- `JNR-054-L06` Demo: diagnosing a production fault from logs (10 min)

---

## Level 3 — Mid-Level Java Backend Engineer (`MID`)

- **Audience:** Working junior engineers or Level 2 graduates.
- **Graduation outcome:** Designs and owns moderately complex services, troubleshoots production issues, reasons about performance and reliability, and makes informed technical trade-offs.
- **Study hours:** 300–450 · **Video hours:** 60–85 · **Lessons:** 180–250
- **Capstone:** `MID-CAP` Distributed Order Processing Platform: Independently deployable services split along domain boundaries: order saga, transactional outbox, idempotent consumers, inventory reservation, Redis caching, tracing, DLQs, load tests, recovery runbooks.
- **Graduation gate:** Diagnoses a simulated production incident, improves a measured performance bottleneck, and defends the architecture's trade-offs.

### MID-P1 — Advanced Java and JVM Internals

#### MID-001 · JVM architecture
*68 min video · 3 h practice* · Prerequisites: BEG-007, BEG-038, JNR-001

**Topics:** Class loading, bytecode, runtime data areas, JIT compilation

**Lessons:**
- `MID-001-L01` From `.class` file to running code (10 min)
- `MID-001-L02` Class loading and class loaders (12 min)
- `MID-001-L03` Reading bytecode with `javap` (12 min)
- `MID-001-L04` Runtime data areas (10 min)
- `MID-001-L05` The JIT compiler and warm-up (12 min)
- `MID-001-L06` Demo: watching the JIT with `-XX:+PrintCompilation` (12 min)

#### MID-002 · Memory management
*82 min video · 4 h practice* · Prerequisites: MID-001

**Topics:** Heap generations, allocation, GC roots, garbage collectors, GC logging

**Lessons:**
- `MID-002-L01` How the JVM allocates objects (10 min)
- `MID-002-L02` Generations, GC roots, and reachability (12 min)
- `MID-002-L03` Collectors: G1, ZGC, Parallel (14 min)
- `MID-002-L04` Reading GC logs (12 min)
- `MID-002-L05` The JVM inside a container (10 min)
- `MID-002-L06` Memory leaks in managed languages (10 min)
- `MID-002-L07` Demo: finding a leak with two heap dumps (14 min)

#### MID-003 · Java concurrency
*76 min video · 4 h practice* · Prerequisites: BEG-030, BEG-035

**Topics:** Threads, Runnable, Callable, ExecutorService, thread pools

**Lessons:**
- `MID-003-L01` Why concurrency: throughput and latency (8 min)
- `MID-003-L02` Threads and their lifecycle (10 min)
- `MID-003-L03` Executors and futures (12 min)
- `MID-003-L04` Thread pools: size, queue, rejection (14 min)
- `MID-003-L05` Shutdown and failure handling (8 min)
- `MID-003-L06` Demo: parallelizing the price-feed import (12 min)
- `MID-003-L07` Demo: a thread pool that silently drops work (12 min)

#### MID-004 · Thread safety
*96 min video · 4 h practice* · Prerequisites: MID-003

**Topics:** Race conditions, synchronization, locks, volatile, atomics

**Lessons:**
- `MID-004-L01` Race conditions (10 min)
- `MID-004-L02` Visibility and happens-before (14 min)
- `MID-004-L03` `synchronized` and intrinsic locks (10 min)
- `MID-004-L04` Explicit locks (10 min)
- `MID-004-L05` `volatile` and atomics (10 min)
- `MID-004-L06` Immutability and confinement (8 min)
- `MID-004-L07` Deadlocks (10 min)
- `MID-004-L08` Demo: reproducing a race with a stress test (12 min)
- `MID-004-L09` Demo: diagnosing a deadlock from a thread dump (12 min)

#### MID-005 · Concurrent collections
*50 min video · 2.5 h practice* · Prerequisites: BEG-041, MID-004

**Topics:** ConcurrentHashMap, blocking queues, copy-on-write structures

**Lessons:**
- `MID-005-L01` Why `synchronizedMap` is not enough (8 min)
- `MID-005-L02` `ConcurrentHashMap` (12 min)
- `MID-005-L03` Blocking queues and producer-consumer (12 min)
- `MID-005-L04` Copy-on-write structures (6 min)
- `MID-005-L05` Demo: a bounded producer-consumer order pipeline (12 min)

#### MID-006 · Async programming
*62 min video · 3 h practice* · Prerequisites: BEG-035, MID-003

**Topics:** CompletableFuture, composition, exception propagation, cancellation

**Lessons:**
- `MID-006-L01` Futures vs CompletableFuture (8 min)
- `MID-006-L02` Composing stages (14 min)
- `MID-006-L03` Errors in async code (10 min)
- `MID-006-L04` Timeouts and cancellation (10 min)
- `MID-006-L05` Which thread runs my stage? (8 min)
- `MID-006-L06` Demo: fan-out to three services with a deadline (12 min)

#### MID-007 · Virtual threads
*58 min video · 2.5 h · `version:` current LTS practice* · Prerequisites: MID-004, MID-006

**Topics:** Project Loom, virtual threads, pinning considerations, blocking I/O

**Lessons:**
- `MID-007-L01` The thread-per-request problem (8 min)
- `MID-007-L02` Virtual threads explained (12 min)
- `MID-007-L03` Virtual threads in Spring Boot (8 min)
- `MID-007-L04` Pinning and other pitfalls (10 min)
- `MID-007-L05` Structured concurrency (preview status) (8 min)
- `MID-007-L06` Demo: platform vs virtual threads under load (12 min)

#### MID-008 · Performance profiling
*90 min video · 4 h practice* · Prerequisites: MID-002, MID-004

**Topics:** JFR, JDK Mission Control, heap dumps, thread dumps, CPU profiling

**Lessons:**
- `MID-008-L01` Measure before you optimize (8 min)
- `MID-008-L02` Java Flight Recorder (12 min)
- `MID-008-L03` JDK Mission Control tour (12 min)
- `MID-008-L04` CPU profiling and flame graphs (12 min)
- `MID-008-L05` Thread dumps (10 min)
- `MID-008-L06` Heap dumps (10 min)
- `MID-008-L07` Demo: finding a slow endpoint's hot spot with JFR (14 min)
- `MID-008-L08` Demo: thread starvation in a live service (12 min)

#### MID-009 · Advanced generics and reflection
*60 min video · 2.5 h practice* · Prerequisites: BEG-031, JNR-009

**Topics:** Type erasure, reflection, annotations, dynamic proxies

**Lessons:**
- `MID-009-L01` Type erasure (10 min)
- `MID-009-L02` Wildcards and PECS (10 min)
- `MID-009-L03` Reflection (10 min)
- `MID-009-L04` Custom annotations (8 min)
- `MID-009-L05` Dynamic proxies (10 min)
- `MID-009-L06` Demo: building a mini `@Timed` with a proxy (12 min)

#### MID-010 · Java module system
*43 min video · 1.5 h practice* · Prerequisites: BEG-027, JNR-002

**Topics:** JPMS fundamentals, classpath vs module path

**Lessons:**
- `MID-010-L01` Classpath problems JPMS solves (8 min)
- `MID-010-L02` Writing module descriptors (10 min)
- `MID-010-L03` Reflection and `opens` (7 min)
- `MID-010-L04` JPMS in practice for backend services (8 min)
- `MID-010-L05` Demo: enforcing boundaries with ArchUnit (10 min)

### MID-P2 — Advanced PostgreSQL and Data Access

#### MID-011 · SQL mastery
*72 min video · 5 h practice* · Prerequisites: BEG-050, JNR-029

**Topics:** CTEs, recursive queries, window functions, advanced joins, set operations

**Lessons:**
- `MID-011-L01` CTEs for readable queries (10 min)
- `MID-011-L02` Recursive CTEs (10 min)
- `MID-011-L03` Window functions (15 min)
- `MID-011-L04` Advanced joins and LATERAL (10 min)
- `MID-011-L05` Set operations and FILTER (8 min)
- `MID-011-L06` Upserts (7 min)
- `MID-011-L07` Demo: building the monthly sales report in SQL (12 min)

#### MID-012 · Index internals
*62 min video · 3 h practice* · Prerequisites: BEG-042, JNR-034

**Topics:** B-tree, hash, GIN, GiST, BRIN, composite, partial, covering indexes

**Lessons:**
- `MID-012-L01` How a B-tree index works (12 min)
- `MID-012-L02` Composite indexes and column order (10 min)
- `MID-012-L03` GIN, GiST, BRIN, hash (12 min)
- `MID-012-L04` Partial and covering indexes (10 min)
- `MID-012-L05` The cost of indexes (6 min)
- `MID-012-L06` Demo: one query, five indexes, five plans (12 min)

#### MID-013 · Query optimization
*89 min video · 4 h practice* · Prerequisites: MID-012

**Topics:** EXPLAIN ANALYZE, execution plans, selectivity, statistics

**Lessons:**
- `MID-013-L01` How the planner thinks (10 min)
- `MID-013-L02` Reading EXPLAIN ANALYZE (15 min)
- `MID-013-L03` Join algorithms (10 min)
- `MID-013-L04` Statistics and estimates (10 min)
- `MID-013-L05` Finding slow queries with `pg_stat_statements` (8 min)
- `MID-013-L06` Query rewrites that help (10 min)
- `MID-013-L07` Demo: from 4 seconds to 40 ms (14 min)
- `MID-013-L08` Demo: a bad estimate and how statistics fix it (12 min)

#### MID-014 · MVCC
*54 min video · 2 h practice* · Prerequisites: JNR-031

**Topics:** Snapshots, row versions, vacuum, bloat, visibility

**Lessons:**
- `MID-014-L01` Readers don't block writers (10 min)
- `MID-014-L02` Row versions and snapshots (12 min)
- `MID-014-L03` Vacuum and autovacuum (10 min)
- `MID-014-L04` Bloat and long transactions (10 min)
- `MID-014-L05` Demo: an idle transaction blocking vacuum (12 min)

#### MID-015 · Isolation and locking
*76 min video · 3 h practice* · Prerequisites: MID-014

**Topics:** Read committed, repeatable read, serializable, deadlocks, row locks

**Lessons:**
- `MID-015-L01` Concurrency anomalies (12 min)
- `MID-015-L02` Isolation levels in PostgreSQL (12 min)
- `MID-015-L03` Row-level locks (10 min)
- `MID-015-L04` `SKIP LOCKED` job queues (8 min)
- `MID-015-L05` Deadlocks (10 min)
- `MID-015-L06` Demo: lost update in two terminals (12 min)
- `MID-015-L07` Demo: write skew under serializable (12 min)

#### MID-016 · Advanced transactions
*74 min video · 3 h practice* · Prerequisites: JNR-031, MID-015

**Topics:** Optimistic/pessimistic locking, retry behavior, transaction propagation

**Lessons:**
- `MID-016-L01` Optimistic locking (12 min)
- `MID-016-L02` Pessimistic locking from JPA (8 min)
- `MID-016-L03` Choosing a locking strategy (8 min)
- `MID-016-L04` Propagation in depth (12 min)
- `MID-016-L05` Retrying transactions safely (10 min)
- `MID-016-L06` Demo: concurrent edits with `@Version` (12 min)
- `MID-016-L07` Demo: the `REQUIRES_NEW` audit-log trap (12 min)

#### MID-017 · Connection pooling
*50 min video · 2.5 h practice* · Prerequisites: JNR-026, MID-003

**Topics:** HikariCP, pool sizing, saturation, timeouts

**Lessons:**
- `MID-017-L01` The cost of a database connection (8 min)
- `MID-017-L02` HikariCP internals (10 min)
- `MID-017-L03` Sizing a pool (12 min)
- `MID-017-L04` Timeouts and leak detection (8 min)
- `MID-017-L05` Demo: pool exhaustion under load (12 min)

#### MID-018 · Database operations
*62 min video · 3 h practice* · Prerequisites: BEG-051, JNR-048

**Topics:** Backups, restore, replication basics, monitoring, maintenance

**Lessons:**
- `MID-018-L01` Backups: logical vs physical (10 min)
- `MID-018-L02` Restore drills (8 min)
- `MID-018-L03` WAL and point-in-time recovery (12 min)
- `MID-018-L04` Replication and read replicas (12 min)
- `MID-018-L05` What to monitor (8 min)
- `MID-018-L06` Demo: restoring to five minutes before a bad `DELETE` (12 min)

#### MID-019 · Data modeling at scale
*58 min video · 2.5 h practice* · Prerequisites: MID-013

**Topics:** Normalization trade-offs, denormalization, partitioning

**Lessons:**
- `MID-019-L01` Normalization trade-offs (10 min)
- `MID-019-L02` Denormalization patterns (10 min)
- `MID-019-L03` Table partitioning (12 min)
- `MID-019-L04` `jsonb`: when and how (8 min)
- `MID-019-L05` Retention and archiving (6 min)
- `MID-019-L06` Demo: partitioning the order history by month (12 min)

#### MID-020 · Database migrations
*60 min video · 2.5 h practice* · Prerequisites: JNR-033, MID-015

**Topics:** Expand-contract, zero-downtime schema changes, rollback strategies

**Lessons:**
- `MID-020-L01` Why migrations cause outages (8 min)
- `MID-020-L02` Expand and contract (12 min)
- `MID-020-L03` Lock-safe DDL (10 min)
- `MID-020-L04` Batched backfills (8 min)
- `MID-020-L05` Rollback strategies (8 min)
- `MID-020-L06` Demo: renaming a column under live traffic (14 min)

#### MID-021 · Advanced Hibernate
*58 min video · 3 h practice* · Prerequisites: JNR-032, MID-016

**Topics:** Fetch plans, batching, first/second-level cache, entity states

**Lessons:**
- `MID-021-L01` Fetch plans per use case (10 min)
- `MID-021-L02` Batching inserts and updates (10 min)
- `MID-021-L03` Second-level and query caches (12 min)
- `MID-021-L04` Entity states revisited: merge vs persist (8 min)
- `MID-021-L05` Hibernate statistics (6 min)
- `MID-021-L06` Demo: 10× faster bulk updates with batching (12 min)

#### MID-022 · Alternative persistence
*52 min video · 2.5 h practice* · Prerequisites: JNR-026, MID-011

**Topics:** jOOQ, JDBC vs JPA trade-offs, CQRS read models

**Lessons:**
- `MID-022-L01` When JPA is the wrong tool (8 min)
- `MID-022-L02` jOOQ in practice (14 min)
- `MID-022-L03` Choosing a persistence approach (8 min)
- `MID-022-L04` Read models and CQRS-lite (10 min)
- `MID-022-L05` Demo: rewriting the sales report with jOOQ (12 min)

### MID-P3 — Distributed Systems Foundations

#### MID-059 · Architectural styles
*64 min video · 3 h practice* · Prerequisites: JNR-004, JNR-013

**Topics:** Layered, hexagonal, clean architecture, modular monolith

**Lessons:**
- `MID-059-L01` What architecture is for (8 min)
- `MID-059-L02` Layered architecture and its limits (8 min)
- `MID-059-L03` Hexagonal architecture (14 min)
- `MID-059-L04` Clean architecture (8 min)
- `MID-059-L05` The modular monolith (12 min)
- `MID-059-L06` Demo: turning Shop into ports and adapters (14 min)

#### MID-060 · DDD introduction
*70 min video · 3 h practice* · Prerequisites: JNR-030, MID-059

**Topics:** Entities, value objects, aggregates, repositories, domain services

**Lessons:**
- `MID-060-L01` Why domain-driven design (8 min)
- `MID-060-L02` Ubiquitous language (8 min)
- `MID-060-L03` Entities and value objects (10 min)
- `MID-060-L04` Aggregates and invariants (14 min)
- `MID-060-L05` Repositories and domain services (8 min)
- `MID-060-L06` Domain events (8 min)
- `MID-060-L07` Demo: redesigning the Order aggregate (14 min)

#### MID-061 · Microservices introduction
*50 min video · 2 h practice* · Prerequisites: MID-060

**Topics:** Benefits, costs, service boundaries, deployment independence

**Lessons:**
- `MID-061-L01` What microservices promise (8 min)
- `MID-061-L02` What they cost (12 min)
- `MID-061-L03` The distributed monolith (8 min)
- `MID-061-L04` Criteria for extracting a service (10 min)
- `MID-061-L05` Demo: walking through the decision for each Shop module (12 min)

#### MID-023 · Distributed computing
*62 min video · 2 h practice* · Prerequisites: BEG-003, JNR-022

**Topics:** Nodes, network latency, partial failures, clocks, failure models

**Lessons:**
- `MID-023-L01` The eight fallacies (12 min)
- `MID-023-L02` Latency numbers every engineer should know (8 min)
- `MID-023-L03` Partial failure (12 min)
- `MID-023-L04` Clocks and ordering (12 min)
- `MID-023-L05` Failure models (6 min)
- `MID-023-L06` Demo: injecting latency and packet loss with Toxiproxy (12 min)

#### MID-024 · Communication models
*60 min video · 2.5 h practice* · Prerequisites: JNR-018, MID-023

**Topics:** Synchronous vs asynchronous, REST vs gRPC, request/reply

**Lessons:**
- `MID-024-L01` Sync vs async (10 min)
- `MID-024-L02` Temporal coupling (8 min)
- `MID-024-L03` REST vs gRPC (10 min)
- `MID-024-L04` gRPC and Protocol Buffers (12 min)
- `MID-024-L05` Request/reply over messaging (8 min)
- `MID-024-L06` Demo: the same call in REST and gRPC (12 min)

#### MID-025 · Service boundaries
*62 min video · 3 h practice* · Prerequisites: MID-060, MID-061

**Topics:** Cohesion, bounded contexts, data ownership

**Lessons:**
- `MID-025-L01` Bounded contexts (12 min)
- `MID-025-L02` One concept, several models (8 min)
- `MID-025-L03` Data ownership (10 min)
- `MID-025-L04` Life without cross-service joins (10 min)
- `MID-025-L05` Evaluating a boundary (8 min)
- `MID-025-L06` Demo: splitting Shop's shared database (14 min)

#### MID-026 · Messaging fundamentals
*58 min video · 2 h practice* · Prerequisites: MID-024

**Topics:** Queues, topics, producers, consumers, delivery semantics

**Lessons:**
- `MID-026-L01` Why messaging (8 min)
- `MID-026-L02` Queues vs topics (10 min)
- `MID-026-L03` Commands vs events (8 min)
- `MID-026-L04` Delivery semantics (12 min)
- `MID-026-L05` Designing event payloads (10 min)
- `MID-026-L06` Demo: one event, three consumers (10 min)

#### MID-027 · RabbitMQ
*60 min video · 2.5 h practice* · Prerequisites: JNR-050, MID-026

**Topics:** Exchanges, routing, acknowledgments, dead-letter queues

**Lessons:**
- `MID-027-L01` RabbitMQ's model (10 min)
- `MID-027-L02` Exchanges and routing (10 min)
- `MID-027-L03` Acknowledgments and prefetch (10 min)
- `MID-027-L04` Dead-letter queues and delayed retry (10 min)
- `MID-027-L05` RabbitMQ or Kafka? (8 min)
- `MID-027-L06` Demo: notification routing with a topic exchange (12 min)

#### MID-028 · Apache Kafka
*100 min video · 4 h practice* · Prerequisites: JNR-050, MID-026

**Topics:** Brokers, topics, partitions, consumer groups, offsets, ordering

**Lessons:**
- `MID-028-L01` Kafka as a distributed log (10 min)
- `MID-028-L02` Topics, partitions, replicas (12 min)
- `MID-028-L03` Keys and ordering (10 min)
- `MID-028-L04` Consumer groups and offsets (12 min)
- `MID-028-L05` Spring for Apache Kafka (12 min)
- `MID-028-L06` Error handling and dead-letter topics (10 min)
- `MID-028-L07` Producer durability settings (8 min)
- `MID-028-L08` Demo: order events end to end (14 min)
- `MID-028-L09` Demo: what a rebalance does to in-flight messages (12 min)

#### MID-029 · Reliable messaging
*80 min video · 4 h practice* · Prerequisites: JNR-031, MID-028

**Topics:** Transactional outbox, inbox, retries, deduplication, idempotency

**Lessons:**
- `MID-029-L01` The dual-write problem (10 min)
- `MID-029-L02` Transactional outbox (14 min)
- `MID-029-L03` Outbox relays: polling vs CDC (10 min)
- `MID-029-L04` Idempotent consumers and the inbox (12 min)
- `MID-029-L05` Retries, backoff, and DLQs (10 min)
- `MID-029-L06` Demo: losing an event without an outbox (12 min)
- `MID-029-L07` Demo: processing the same message twice, safely (12 min)

#### MID-030 · Distributed consistency
*52 min video · 2 h practice* · Prerequisites: MID-023, MID-029

**Topics:** Strong vs eventual consistency, CAP and PACELC, consistency trade-offs

**Lessons:**
- `MID-030-L01` Consistency models (12 min)
- `MID-030-L02` CAP, correctly (10 min)
- `MID-030-L03` PACELC (8 min)
- `MID-030-L04` Designing for eventual consistency (10 min)
- `MID-030-L05` Demo: read-your-writes across services (12 min)

#### MID-031 · Distributed workflows
*88 min video · 4 h practice* · Prerequisites: MID-025, MID-029

**Topics:** Sagas, choreography vs orchestration, compensation

**Lessons:**
- `MID-031-L01` Why distributed transactions don't scale (10 min)
- `MID-031-L02` Sagas (12 min)
- `MID-031-L03` Choreography (10 min)
- `MID-031-L04` Orchestration (10 min)
- `MID-031-L05` Compensation design (10 min)
- `MID-031-L06` Saga state, timeouts, and stuck sagas (10 min)
- `MID-031-L07` Demo: the order saga, happy path (14 min)
- `MID-031-L08` Demo: payment declined, compensations run (12 min)

#### MID-032 · Distributed coordination
*48 min video · 2 h practice* · Prerequisites: MID-030

**Topics:** Leases, leader election concepts, fencing tokens

**Lessons:**
- `MID-032-L01` When only one instance may act (8 min)
- `MID-032-L02` Leases and leader election (10 min)
- `MID-032-L03` Distributed locks and their limits (10 min)
- `MID-032-L04` Fencing tokens (8 min)
- `MID-032-L05` Demo: a nightly job running once across three replicas (12 min)

#### MID-033 · Resilience
*82 min video · 3 h practice* · Prerequisites: JNR-022, MID-024

**Topics:** Timeouts, retries with backoff, circuit breakers, bulkheads

**Lessons:**
- `MID-033-L01` How failures cascade (10 min)
- `MID-033-L02` Timeouts and latency budgets (10 min)
- `MID-033-L03` Retries, backoff, and jitter (10 min)
- `MID-033-L04` Circuit breakers (10 min)
- `MID-033-L05` Bulkheads (8 min)
- `MID-033-L06` Fallbacks and degradation (8 min)
- `MID-033-L07` Demo: a cascading failure, then the fix (14 min)
- `MID-033-L08` Demo: retry storms and jitter (12 min)

#### MID-034 · Rate limiting
*52 min video · 2 h practice* · Prerequisites: MID-033

**Topics:** Token bucket, leaky bucket, quotas, client throttling

**Lessons:**
- `MID-034-L01` Why limit (6 min)
- `MID-034-L02` Token and leaky buckets (10 min)
- `MID-034-L03` Distributed rate limiting (10 min)
- `MID-034-L04` Quotas and load shedding (8 min)
- `MID-034-L05` Being a good client (6 min)
- `MID-034-L06` Demo: per-customer limits at the edge (12 min)

#### MID-035 · API gateways
*56 min video · 2.5 h practice* · Prerequisites: JNR-039, MID-024

**Topics:** Routing, authentication integration, gateway responsibilities

**Lessons:**
- `MID-035-L01` Why a gateway (8 min)
- `MID-035-L02` Routing and filters (10 min)
- `MID-035-L03` Authentication at the edge (10 min)
- `MID-035-L04` What not to put in a gateway (8 min)
- `MID-035-L05` Backend for frontend (8 min)
- `MID-035-L06` Demo: one entry point for four services (12 min)

#### MID-036 · Service discovery
*42 min video · 1.5 h practice* · Prerequisites: JNR-049, MID-035

**Topics:** DNS-based discovery, platform-native discovery, load balancing

**Lessons:**
- `MID-036-L01` Finding services (8 min)
- `MID-036-L02` DNS-based discovery (8 min)
- `MID-036-L03` Platform-native discovery (8 min)
- `MID-036-L04` Load-balancing strategies (8 min)
- `MID-036-L05` Demo: scaling inventory to three replicas (10 min)

### MID-P4 — Caching and Nonrelational Data

#### MID-037 · Caching fundamentals
*44 min video · 1.5 h practice* · Prerequisites: MID-023

**Topics:** Local vs distributed, hit ratio, eviction, TTL

**Lessons:**
- `MID-037-L01` Why and where to cache (10 min)
- `MID-037-L02` Local vs distributed caches (8 min)
- `MID-037-L03` Hit ratio and what it hides (8 min)
- `MID-037-L04` Eviction and TTL (8 min)
- `MID-037-L05` Demo: a local Caffeine cache with metrics (10 min)

#### MID-038 · Redis
*76 min video · 3 h practice* · Prerequisites: JNR-050, MID-037

**Topics:** Strings, hashes, sets, sorted sets, key design

**Lessons:**
- `MID-038-L01` Redis in one picture (8 min)
- `MID-038-L02` Data structures and their uses (14 min)
- `MID-038-L03` Key design (8 min)
- `MID-038-L04` Redis from Spring (12 min)
- `MID-038-L05` Persistence, memory, and eviction (10 min)
- `MID-038-L06` Demo: a leaderboard with sorted sets (12 min)
- `MID-038-L07` Demo: caching product details with `@Cacheable` (12 min)

#### MID-039 · Caching patterns
*50 min video · 2.5 h practice* · Prerequisites: MID-038

**Topics:** Cache-aside, write-through, write-behind, invalidation

**Lessons:**
- `MID-039-L01` Cache-aside (10 min)
- `MID-039-L02` Read-through and write-through (10 min)
- `MID-039-L03` Write-behind (8 min)
- `MID-039-L04` Invalidation strategies (10 min)
- `MID-039-L05` Demo: event-driven invalidation from `ProductUpdated` (12 min)

#### MID-040 · Cache consistency
*50 min video · 2 h practice* · Prerequisites: MID-030, MID-039

**Topics:** Stampedes, stale data, invalidation races, hot keys

**Lessons:**
- `MID-040-L01` Stampedes (10 min)
- `MID-040-L02` Invalidation races (12 min)
- `MID-040-L03` Hot keys (8 min)
- `MID-040-L04` Staleness budgets (8 min)
- `MID-040-L05` Demo: a stampede after cache expiry, then the fix (12 min)

#### MID-041 · NoSQL fundamentals
*54 min video · 1.5 h practice* · Prerequisites: BEG-048, MID-030

**Topics:** Key-value, document, column-family, graph databases

**Lessons:**
- `MID-041-L01` Why NoSQL exists (8 min)
- `MID-041-L02` Key-value and document stores (10 min)
- `MID-041-L03` Wide-column stores (8 min)
- `MID-041-L04` Graph databases (8 min)
- `MID-041-L05` Modeling for queries (8 min)
- `MID-041-L06` Demo: the same data in four models (12 min)

#### MID-042 · MongoDB
*68 min video · 2.5 h practice* · Prerequisites: MID-041

**Topics:** Document modeling, indexing, aggregation, transactions, use cases

**Lessons:**
- `MID-042-L01` Documents and collections (8 min)
- `MID-042-L02` Embedding vs referencing (12 min)
- `MID-042-L03` Indexes and explain (10 min)
- `MID-042-L04` Aggregation pipelines (12 min)
- `MID-042-L05` Transactions (6 min)
- `MID-042-L06` Spring Data MongoDB (8 min)
- `MID-042-L07` Demo: building the reviews service on MongoDB (12 min)

#### MID-043 · Search systems
*62 min video · 2.5 h practice* · Prerequisites: MID-012, MID-041

**Topics:** Full-text search, inverted indexes, Elasticsearch/OpenSearch basics

**Lessons:**
- `MID-043-L01` How search engines find things (10 min)
- `MID-043-L02` Analyzers and relevance (10 min)
- `MID-043-L03` Queries, filters, and facets (12 min)
- `MID-043-L04` Keeping the index in sync (10 min)
- `MID-043-L05` PostgreSQL full-text vs a search engine (8 min)
- `MID-043-L06` Demo: product search with typo tolerance and facets (12 min)

#### MID-067 · Embeddings and vector search
*65 min video · 3 h · `version:` embedding models and pgvector releases change — verify before recording practice* · Prerequisites: JNR-056, MID-043 · added in v2.0

**Topics:** Embeddings, similarity metrics, pgvector, HNSW and IVFFlat indexes, hybrid keyword plus vector search

**Lessons:**
- `MID-067-L01` What embeddings are (10 min)
- `MID-067-L02` Similarity measures (8 min)
- `MID-067-L03` pgvector: storing and querying vectors (12 min)
- `MID-067-L04` Approximate indexes: HNSW and IVFFlat (12 min)
- `MID-067-L05` Hybrid search: keywords plus vectors (10 min)
- `MID-067-L06` Demo: semantic search over Shop's help-center articles (13 min)

#### MID-068 · Retrieval-augmented generation
*80 min video · 3.5 h practice* · Prerequisites: MID-067 · added in v2.0

**Topics:** Chunking, retrieval, context assembly, citations, keeping the index fresh with events, retrieval quality

**Lessons:**
- `MID-068-L01` Why RAG, and its limits (8 min)
- `MID-068-L02` Chunking strategies (10 min)
- `MID-068-L03` Retrieval, filters, and re-ranking (10 min)
- `MID-068-L04` Context assembly and citations (10 min)
- `MID-068-L05` Freshness: re-indexing on events (8 min)
- `MID-068-L06` Evaluating retrieval separately from generation (9 min)
- `MID-068-L07` Demo: the order-support assistant answers with citations (13 min)
- `MID-068-L08` Demo: a stale policy answer fixed by event-driven re-indexing (12 min)

#### MID-044 · Data selection
*40 min video · 2 h practice* · Prerequisites: MID-038, MID-042, MID-043

**Topics:** PostgreSQL vs Redis vs MongoDB vs search engines; workload-driven decisions

**Lessons:**
- `MID-044-L01` Characterizing a workload (10 min)
- `MID-044-L02` PostgreSQL first, and when not (10 min)
- `MID-044-L03` The operational cost of another database (8 min)
- `MID-044-L04` Demo: writing the reviews datastore ADR (12 min)

### MID-P5 — Production Engineering and Security

#### MID-069 · Tool calling and agents
*80 min video · 3.5 h · `version:` tool-calling APIs and the Model Context Protocol evolve quickly — verify before recording practice* · Prerequisites: MID-033, MID-068 · added in v2.0

**Topics:** Function calling, safe tool design, side effects and idempotency, authorization, human approval, agent loops, Model Context Protocol concept

**Lessons:**
- `MID-069-L01` From answering to acting (8 min)
- `MID-069-L02` How tool calling works (12 min)
- `MID-069-L03` Designing safe tools (10 min)
- `MID-069-L04` Authorization and identity for tool calls (10 min)
- `MID-069-L05` Side effects, idempotency, and human approval (8 min)
- `MID-069-L06` Agent loops and their limits; MCP as a concept (7 min)
- `MID-069-L07` Demo: an order-status tool that respects ownership (12 min)
- `MID-069-L08` Demo: a refund request routed to human approval (13 min)

#### MID-045 · Advanced testing
*64 min video · 3 h practice* · Prerequisites: JNR-046, MID-029

**Topics:** Contract testing, consumer-driven contracts, property-based testing

**Lessons:**
- `MID-045-L01` Testing distributed systems (10 min)
- `MID-045-L02` Consumer-driven contracts (12 min)
- `MID-045-L03` Contracts for messages (10 min)
- `MID-045-L04` Contracts in CI (8 min)
- `MID-045-L05` Property-based testing (12 min)
- `MID-045-L06` Demo: a breaking API change caught by a contract (12 min)

#### MID-046 · Performance testing
*64 min video · 3 h practice* · Prerequisites: MID-008, MID-017

**Topics:** k6 or Gatling, load, stress, spike, soak testing

**Lessons:**
- `MID-046-L01` Kinds of performance tests (10 min)
- `MID-046-L02` Writing k6 scenarios (12 min)
- `MID-046-L03` Workload models (10 min)
- `MID-046-L04` Percentiles and coordinated omission (10 min)
- `MID-046-L05` From test result to bottleneck (10 min)
- `MID-046-L06` Demo: a soak test that finds a slow leak (12 min)

#### MID-047 · Observability
*94 min video · 3.5 h practice* · Prerequisites: JNR-006, MID-031

**Topics:** Logs, metrics, traces, correlation IDs, OpenTelemetry

**Lessons:**
- `MID-047-L01` Monitoring vs observability (8 min)
- `MID-047-L02` Logs, metrics, traces (10 min)
- `MID-047-L03` OpenTelemetry concepts (12 min)
- `MID-047-L04` Instrumenting Spring services (12 min)
- `MID-047-L05` Context propagation through Kafka (10 min)
- `MID-047-L06` Correlating logs and traces (8 min)
- `MID-047-L07` Custom metrics with Micrometer (8 min)
- `MID-047-L08` Demo: following one order through four services (14 min)
- `MID-047-L09` Demo: finding a slow span in a saga (12 min)

#### MID-048 · Monitoring
*54 min video · 2.5 h practice* · Prerequisites: MID-047

**Topics:** Prometheus, Grafana, dashboards, alerting

**Lessons:**
- `MID-048-L01` Prometheus model (10 min)
- `MID-048-L02` PromQL essentials (12 min)
- `MID-048-L03` Dashboards: RED and USE (10 min)
- `MID-048-L04` Alerting that people trust (10 min)
- `MID-048-L05` Demo: a service dashboard from scratch (12 min)

#### MID-070 · LLM evaluation and observability
*67 min video · 3 h practice* · Prerequisites: MID-047, MID-068 · added in v2.0

**Topics:** Evaluation sets in CI, LLM-as-judge caveats, regression detection, token, latency, and cost tracing

**Lessons:**
- `MID-070-L01` Why LLM features need evaluations (8 min)
- `MID-070-L02` Building an evaluation set (10 min)
- `MID-070-L03` Metrics: recall, groundedness, refusals (10 min)
- `MID-070-L04` LLM-as-judge and its caveats (8 min)
- `MID-070-L05` Evaluations in CI (8 min)
- `MID-070-L06` Tracing tokens, latency, and cost (10 min)
- `MID-070-L07` Demo: an evaluation run catching a prompt regression (13 min)

#### MID-049 · Reliability
*60 min video · 2 h practice* · Prerequisites: MID-048

**Topics:** SLIs, SLOs, error budgets, availability, latency percentiles

**Lessons:**
- `MID-049-L01` What reliability means to users (8 min)
- `MID-049-L02` SLIs (10 min)
- `MID-049-L03` SLOs and error budgets (12 min)
- `MID-049-L04` Burn-rate alerts (10 min)
- `MID-049-L05` Using the budget (8 min)
- `MID-049-L06` Demo: SLO dashboard and burn-rate alert for checkout (12 min)

#### MID-050 · Incident handling
*60 min video · 2.5 h practice* · Prerequisites: JNR-054, MID-049

**Topics:** Triage, severity, escalation, incident timeline, postmortems

**Lessons:**
- `MID-050-L01` Anatomy of an incident (8 min)
- `MID-050-L02` Triage and severity (10 min)
- `MID-050-L03` Mitigate first (10 min)
- `MID-050-L04` Roles and communication (8 min)
- `MID-050-L05` Blameless postmortems (10 min)
- `MID-050-L06` Demo: a simulated incident, start to finish (14 min)

#### MID-051 · Advanced API security
*54 min video · 2.5 h practice* · Prerequisites: JNR-039, MID-035

**Topics:** OAuth 2.0 flows, OIDC, token validation, authorization design

**Lessons:**
- `MID-051-L01` OAuth flows revisited (10 min)
- `MID-051-L02` Token validation everywhere (10 min)
- `MID-051-L03` Scopes, claims, and authorization design (12 min)
- `MID-051-L04` Service-to-service identity (10 min)
- `MID-051-L05` Demo: propagating identity from gateway to inventory (12 min)

#### MID-052 · Application threats
*56 min video · 2.5 h practice* · Prerequisites: JNR-041, MID-051

**Topics:** Threat modeling, OWASP API Security Top 10, abuse prevention

**Lessons:**
- `MID-052-L01` Threat modeling with STRIDE (12 min)
- `MID-052-L02` OWASP API Security Top 10 (14 min)
- `MID-052-L03` Business-logic abuse (10 min)
- `MID-052-L04` From threats to tests (8 min)
- `MID-052-L05` Demo: threat-modeling the checkout flow (12 min)

#### MID-071 · AI application threats
*61 min video · 2.5 h · `version:` follows the current OWASP Top 10 for LLM Applications — verify before recording practice* · Prerequisites: MID-052, MID-069 · added in v2.0

**Topics:** Indirect prompt injection through retrieved content, excessive agency, data exfiltration, cost abuse, mitigations

**Lessons:**
- `MID-071-L01` The LLM threat landscape (12 min)
- `MID-071-L02` Indirect prompt injection through retrieved content (10 min)
- `MID-071-L03` Excessive agency and improper output handling (10 min)
- `MID-071-L04` Sensitive data disclosure and system prompt leakage (8 min)
- `MID-071-L05` Unbounded consumption and cost abuse (8 min)
- `MID-071-L06` Demo: a poisoned help article hijacks the assistant, then the fix (13 min)

#### MID-053 · Dependency security
*56 min video · 2 h practice* · Prerequisites: JNR-042, JNR-051

**Topics:** SCA, SBOM, vulnerability scanning, secure builds

**Lessons:**
- `MID-053-L01` Your code is mostly other people's code (8 min)
- `MID-053-L02` SCA and triage (10 min)
- `MID-053-L03` SBOMs (8 min)
- `MID-053-L04` Image scanning (8 min)
- `MID-053-L05` Supply-chain security (10 min)
- `MID-053-L06` Demo: triaging a critical CVE (12 min)

#### MID-054 · Secrets and cryptography
*62 min video · 2 h practice* · Prerequisites: JNR-042

**Topics:** Encryption in transit/at rest, key management concepts, rotation

**Lessons:**
- `MID-054-L01` Cryptography for engineers (12 min)
- `MID-054-L02` TLS in practice (10 min)
- `MID-054-L03` Encryption at rest (8 min)
- `MID-054-L04` Key management and envelope encryption (10 min)
- `MID-054-L05` Secrets managers and rotation (10 min)
- `MID-054-L06` Demo: rotating a database password without downtime (12 min)

#### MID-055 · CI/CD advanced
*60 min video · 2.5 h practice* · Prerequisites: JNR-051, JNR-052

**Topics:** Deployment environments, automated quality gates, rollback

**Lessons:**
- `MID-055-L01` Build once, promote everywhere (10 min)
- `MID-055-L02` Environments and approvals (8 min)
- `MID-055-L03` Quality gates (10 min)
- `MID-055-L04` Deployment strategies (12 min)
- `MID-055-L05` Feature flags (8 min)
- `MID-055-L06` Demo: an automated rollback on a failed health check (12 min)

#### MID-056 · Cloud fundamentals
*72 min video · 3 h practice* · Prerequisites: JNR-048, JNR-052

**Topics:** IAM, VPCs, subnets, load balancers, managed databases, object storage

**Lessons:**
- `MID-056-L01` Cloud building blocks (10 min)
- `MID-056-L02` Regions and availability zones (8 min)
- `MID-056-L03` Identity and access management (12 min)
- `MID-056-L04` Networking: VPCs and subnets (12 min)
- `MID-056-L05` Managed databases, load balancers, object storage (12 min)
- `MID-056-L06` Reading a cloud bill (6 min)
- `MID-056-L07` Demo: a private database reachable only from the app (12 min)

#### MID-057 · Kubernetes foundations
*106 min video · 4 h practice* · Prerequisites: JNR-049, MID-056

**Topics:** Pods, Deployments, Services, ConfigMaps, Secrets, probes, autoscaling

**Lessons:**
- `MID-057-L01` Why Kubernetes (8 min)
- `MID-057-L02` Architecture and desired state (10 min)
- `MID-057-L03` Pods and Deployments (12 min)
- `MID-057-L04` Services and Ingress (10 min)
- `MID-057-L05` ConfigMaps and Secrets (8 min)
- `MID-057-L06` Probes for JVM services (10 min)
- `MID-057-L07` Requests, limits, and autoscaling (12 min)
- `MID-057-L08` Debugging pods (10 min)
- `MID-057-L09` Demo: deploying Shop Platform to a cluster (14 min)
- `MID-057-L10` Demo: a crash-looping pod, diagnosed (12 min)

#### MID-058 · Infrastructure as Code
*62 min video · 3 h practice* · Prerequisites: MID-056

**Topics:** Terraform fundamentals, state, modules, reviewable changes

**Lessons:**
- `MID-058-L01` Why infrastructure as code (8 min)
- `MID-058-L02` Terraform basics (12 min)
- `MID-058-L03` State and drift (10 min)
- `MID-058-L04` Modules and environments (10 min)
- `MID-058-L05` Terraform in CI (8 min)
- `MID-058-L06` Demo: rebuilding the clicked infrastructure as code (14 min)

### MID-P6 — API Evolution and Professional Ownership

#### MID-062 · API evolution
*58 min video · 2.5 h practice* · Prerequisites: JNR-020, MID-045

**Topics:** Backward compatibility, schema evolution, deprecation

**Lessons:**
- `MID-062-L01` What counts as a breaking change (10 min)
- `MID-062-L02` Evolving REST APIs (10 min)
- `MID-062-L03` Schema registries and compatibility modes (12 min)
- `MID-062-L04` Tolerant readers (6 min)
- `MID-062-L05` Deprecation done properly (8 min)
- `MID-062-L06` Demo: changing `OrderPlaced` without breaking consumers (12 min)

#### MID-063 · Technical documentation
*68 min video · 3 h practice* · Prerequisites: MID-061

**Topics:** ADRs, RFCs, sequence diagrams, C4 diagrams

**Lessons:**
- `MID-063-L01` Documentation that gets read (8 min)
- `MID-063-L02` Architecture decision records (10 min)
- `MID-063-L03` RFCs and design docs (10 min)
- `MID-063-L04` C4 diagrams (12 min)
- `MID-063-L05` Sequence diagrams (8 min)
- `MID-063-L06` Runbooks (8 min)
- `MID-063-L07` Demo: C4 diagrams of Shop Platform as code (12 min)

#### MID-064 · Estimation and delivery
*56 min video · 2 h practice* · Prerequisites: JNR-053

**Topics:** Requirement clarification, decomposition, risk identification

**Lessons:**
- `MID-064-L01` Clarifying requirements (10 min)
- `MID-064-L02` Slicing work vertically (10 min)
- `MID-064-L03` Estimating with ranges (10 min)
- `MID-064-L04` Risk first: spikes and prototypes (8 min)
- `MID-064-L05` Reporting progress honestly (6 min)
- `MID-064-L06` Demo: breaking "returns and refunds" into slices (12 min)

#### MID-065 · Engineering ownership
*56 min video · 2 h practice* · Prerequisites: MID-050

**Topics:** Operational responsibility, prioritization, communication

**Lessons:**
- `MID-065-L01` You build it, you run it (8 min)
- `MID-065-L02` On-call well (10 min)
- `MID-065-L03` Prioritizing reliability and debt (10 min)
- `MID-065-L04` Production readiness checklist (8 min)
- `MID-065-L05` Communicating as an owner (8 min)
- `MID-065-L06` Demo: a readiness review of the payments service (12 min)

#### MID-066 · Technical collaboration
*56 min video · 2 h practice* · Prerequisites: JNR-053

**Topics:** Reviews, constructive feedback, mentoring junior engineers

**Lessons:**
- `MID-066-L01` Reviewing beyond style (10 min)
- `MID-066-L02` Feedback that lands (8 min)
- `MID-066-L03` Design reviews (8 min)
- `MID-066-L04` Mentoring juniors (10 min)
- `MID-066-L05` Disagreement and decisions (8 min)
- `MID-066-L06` Demo: reviewing a real pull request out loud (12 min)

#### MID-072 · AI-assisted engineering at codebase scale
*60 min video · 2.5 h practice* · Prerequisites: JNR-055, MID-008 · added in v2.0

**Topics:** AI-assisted debugging, refactoring, and test generation on large codebases, review discipline, measuring quality

**Lessons:**
- `MID-072-L01` AI assistants on large codebases (8 min)
- `MID-072-L02` AI-assisted debugging with evidence (10 min)
- `MID-072-L03` Refactoring with AI under a safety net (10 min)
- `MID-072-L04` Generating tests worth keeping (10 min)
- `MID-072-L05` Review discipline and measuring quality (9 min)
- `MID-072-L06` Demo: an AI-assisted refactor of the order saga under green tests (13 min)

---

## Level 4 — Senior Backend Engineer — Grade C (System ownership) (`SRC`)

- **Audience:** Mid-level engineers with production experience.
- **Graduation outcome:** Independently leads the design and delivery of a significant subsystem, makes reliable architecture decisions, manages technical risks, and guides less-experienced engineers.
- **Study hours:** 150–220 plus substantial real-world practice · **Video hours:** 25–35 · **Lessons:** 65–90
- **Capstone:** `SRC-CAP` Reliability and Performance Redesign: Own the order-processing subsystem and redesign it to meet explicit availability, latency, and recovery targets, with architecture docs, performance evidence, failure-injection tests, and an operational handover.
- **Graduation gate:** Scenario-based design review and production-incident simulation.

### SRC-P1 — System Design and Architecture Decisions

#### SRC-001 · Requirements engineering
*81 min video · 4 h practice* · Prerequisites: MID-064

**Topics:** Functional vs nonfunctional requirements, constraints, assumptions

**Lessons:**
- `SRC-001-L01` Why systems fail at the requirements stage (10 min)
- `SRC-001-L02` Functional vs nonfunctional requirements (10 min)
- `SRC-001-L03` Constraints and assumptions (10 min)
- `SRC-001-L04` Stakeholder interviews that surface real needs (12 min)
- `SRC-001-L05` Quality-attribute scenarios (14 min)
- `SRC-001-L06` Conflicts and trade-off conversations (10 min)
- `SRC-001-L07` Demo: turning "orders must never be lost" into testable requirements (15 min)

#### SRC-002 · Quality attributes
*89 min video · 4 h practice* · Prerequisites: MID-049, SRC-001

**Topics:** Availability, scalability, maintainability, reliability, security, operability

**Lessons:**
- `SRC-002-L01` Quality attributes drive architecture (10 min)
- `SRC-002-L02` Availability and reliability, measured (12 min)
- `SRC-002-L03` Scalability and elasticity (10 min)
- `SRC-002-L04` Maintainability and operability (10 min)
- `SRC-002-L05` Security as a quality attribute (8 min)
- `SRC-002-L06` Utility trees and prioritization (12 min)
- `SRC-002-L07` Tactics catalog (12 min)
- `SRC-002-L08` Demo: building the utility tree for the order subsystem (15 min)

#### SRC-003 · Architecture trade-offs
*96 min video · 4 h practice* · Prerequisites: MID-063, SRC-002

**Topics:** Complexity budgets, cost of abstraction, reversible vs irreversible decisions

**Lessons:**
- `SRC-003-L01` Every decision is a trade-off (10 min)
- `SRC-003-L02` One-way and two-way doors (10 min)
- `SRC-003-L03` Complexity budgets (12 min)
- `SRC-003-L04` The cost of abstraction (10 min)
- `SRC-003-L05` Lightweight architecture evaluation (14 min)
- `SRC-003-L06` Risks, sensitivity points, and trade-off points (10 min)
- `SRC-003-L07` Demo: evaluating three designs for order storage (15 min)
- `SRC-003-L08` Demo: an architecture review that changes its mind (15 min)

#### SRC-004 · Capacity planning
*94 min video · 5 h practice* · Prerequisites: MID-046, SRC-002

**Topics:** RPS, concurrency, data growth, throughput, storage estimates

**Lessons:**
- `SRC-004-L01` From business forecast to load (12 min)
- `SRC-004-L02` Peaks, seasonality, and burst factors (10 min)
- `SRC-004-L03` Back-of-the-envelope estimation (14 min)
- `SRC-004-L04` Storage and data growth (10 min)
- `SRC-004-L05` Headroom and saturation points (10 min)
- `SRC-004-L06` Capacity plans people can act on (8 min)
- `SRC-004-L07` Demo: sizing the order subsystem for Black Friday at 10× (15 min)
- `SRC-004-L08` Demo: checking last year's capacity plan against reality (15 min)

#### SRC-005 · Performance modeling
*73 min video · 4 h practice* · Prerequisites: MID-017, SRC-004

**Topics:** Latency budgets, Little's Law, bottleneck analysis, queuing

**Lessons:**
- `SRC-005-L01` Latency budgets (12 min)
- `SRC-005-L02` Little's Law (12 min)
- `SRC-005-L03` Queueing and utilization (14 min)
- `SRC-005-L04` Tail latency and fan-out (10 min)
- `SRC-005-L05` Finding the bottleneck on paper (10 min)
- `SRC-005-L06` Demo: predicting pool sizes with Little's Law, then measuring (15 min)

#### SRC-006 · API and data contracts
*69 min video · 3.5 h practice* · Prerequisites: MID-062

**Topics:** Compatibility, versioning, consumer impact, schema governance

**Lessons:**
- `SRC-006-L01` Contracts as promises between teams (10 min)
- `SRC-006-L02` Compatibility policies (12 min)
- `SRC-006-L03` Measuring consumer impact (10 min)
- `SRC-006-L04` Schema governance that scales (12 min)
- `SRC-006-L05` Coordinating breaking changes (10 min)
- `SRC-006-L06` Demo: splitting `OrderPlaced` into two events across five consumers (15 min)

#### SRC-007 · Database scaling
*104 min video · 4.5 h practice* · Prerequisites: MID-018, MID-019, SRC-004

**Topics:** Read replicas, partitioning, sharding, hot partitions

**Lessons:**
- `SRC-007-L01` The scaling ladder (10 min)
- `SRC-007-L02` Read replicas and lag-aware design (12 min)
- `SRC-007-L03` Partitioning revisited (8 min)
- `SRC-007-L04` Sharding and shard keys (14 min)
- `SRC-007-L05` Hot partitions (10 min)
- `SRC-007-L06` Resharding (10 min)
- `SRC-007-L07` Distributed SQL and managed options (10 min)
- `SRC-007-L08` Demo: choosing a shard key for orders (15 min)
- `SRC-007-L09` Demo: read replicas and the stale-read bug they introduce (15 min)

#### SRC-008 · Architectural decomposition
*92 min video · 4 h practice* · Prerequisites: MID-061, SRC-003

**Topics:** Modular monolith vs services, migration criteria

**Lessons:**
- `SRC-008-L01` Decomposition is a means, not a goal (10 min)
- `SRC-008-L02` Kinds of coupling (12 min)
- `SRC-008-L03` Evidence from change history (10 min)
- `SRC-008-L04` Team topology and boundaries (10 min)
- `SRC-008-L05` When to merge services back (10 min)
- `SRC-008-L06` Migration criteria and exit conditions (10 min)
- `SRC-008-L07` Demo: mining Git history for change coupling (15 min)
- `SRC-008-L08` Demo: making the case to merge two chatty services (15 min)

#### SRC-009 · Failure-mode analysis
*96 min video · 4 h practice* · Prerequisites: MID-033, SRC-002

**Topics:** Failure domains, dependency mapping, graceful degradation

**Lessons:**
- `SRC-009-L01` How real systems fail (12 min)
- `SRC-009-L02` Dependency mapping (10 min)
- `SRC-009-L03` Failure domains and blast radius (10 min)
- `SRC-009-L04` FMEA for software (14 min)
- `SRC-009-L05` Graceful degradation (10 min)
- `SRC-009-L06` From analysis to experiments (10 min)
- `SRC-009-L07` Demo: FMEA of the checkout path (15 min)
- `SRC-009-L08` Demo: a hidden dependency found by failure injection (15 min)

#### SRC-021 · Designing reliable AI features
*88 min video · 4 h practice* · Prerequisites: SRC-005, MID-070 · added in v2.0

**Topics:** Latency and cost budgets, fallbacks, provider outages, model routing, caching, SLOs for non-deterministic features

**Lessons:**
- `SRC-021-L01` What makes AI features different to operate (10 min)
- `SRC-021-L02` Latency and cost budgets for model calls (12 min)
- `SRC-021-L03` Fallbacks and graceful degradation for AI (12 min)
- `SRC-021-L04` Model routing, caching, and streaming (12 min)
- `SRC-021-L05` SLOs for non-deterministic features (12 min)
- `SRC-021-L06` Demo: an order-support assistant surviving a provider outage (15 min)
- `SRC-021-L07` Demo: cutting cost per answer by routing easy questions to a smaller model (15 min)

#### SRC-010 · Architecture documentation
*67 min video · 3.5 h practice* · Prerequisites: MID-063, SRC-008

**Topics:** ADRs, C4, sequence diagrams, operational runbooks

**Lessons:**
- `SRC-010-L01` Documentation for different readers (10 min)
- `SRC-010-L02` C4 at subsystem scale (10 min)
- `SRC-010-L03` Docs as code (8 min)
- `SRC-010-L04` Runbooks under pressure (12 min)
- `SRC-010-L05` Design docs that get decisions (12 min)
- `SRC-010-L06` Demo: reviewing and rewriting a confusing runbook (15 min)

### SRC-P2 — Reliability and Technical Ownership

#### SRC-011 · Production readiness
*94 min video · 4 h practice* · Prerequisites: MID-055, MID-065

**Topics:** Readiness reviews, deployment safety, rollback, runbooks

**Lessons:**
- `SRC-011-L01` Why launches fail (10 min)
- `SRC-011-L02` The readiness review (14 min)
- `SRC-011-L03` Progressive delivery and canaries (12 min)
- `SRC-011-L04` Automated verification and rollback (10 min)
- `SRC-011-L05` Rolling back data (10 min)
- `SRC-011-L06` Go/no-go decisions (8 min)
- `SRC-011-L07` Demo: a canary that catches a regression (15 min)
- `SRC-011-L08` Demo: a readiness review that says no-go (15 min)

#### SRC-012 · SLO engineering
*86 min video · 4 h practice* · Prerequisites: MID-049, SRC-002

**Topics:** Service-level objectives, error-budget policies, alerts

**Lessons:**
- `SRC-012-L01` SLOs from user journeys (12 min)
- `SRC-012-L02` Composing SLOs across dependencies (12 min)
- `SRC-012-L03` Error-budget policies (12 min)
- `SRC-012-L04` Multi-window burn-rate alerting (12 min)
- `SRC-012-L05` Reviewing and evolving SLOs (8 min)
- `SRC-012-L06` Demo: tuning noisy alerts with burn-rate windows (15 min)
- `SRC-012-L07` Demo: negotiating an error-budget policy with product (15 min)

#### SRC-022 · Operating AI in production
*86 min video · 4 h practice* · Prerequisites: SRC-011, SRC-021 · added in v2.0

**Topics:** Prompt and model versioning and rollback, evaluation-gated releases, drift, bad-output incidents, human review

**Lessons:**
- `SRC-022-L01` AI changes are deployments too (10 min)
- `SRC-022-L02` Versioning prompts, models, and retrieval (12 min)
- `SRC-022-L03` Evaluation-gated and progressive releases (12 min)
- `SRC-022-L04` Detecting drift (10 min)
- `SRC-022-L05` Bad-output incidents, kill switches, and human review (12 min)
- `SRC-022-L06` Demo: rolling back a prompt change that broke refund answers (15 min)
- `SRC-022-L07` Demo: an incident where the assistant revealed another customer's order (15 min)

#### SRC-013 · Disaster recovery
*96 min video · 4.5 h practice* · Prerequisites: MID-018, SRC-009

**Topics:** RPO, RTO, backups, failover, recovery exercises

**Lessons:**
- `SRC-013-L01` Disasters that actually happen (10 min)
- `SRC-013-L02` RPO and RTO from business impact (12 min)
- `SRC-013-L03` Backup and replication strategies (12 min)
- `SRC-013-L04` Failover design (12 min)
- `SRC-013-L05` Recovering event streams and derived data (10 min)
- `SRC-013-L06` Recovery exercises (10 min)
- `SRC-013-L07` Demo: recovering the order database within a 15-minute RTO (15 min)
- `SRC-013-L08` Demo: rebuilding derived data after a Kafka cluster loss (15 min)

#### SRC-014 · Data integrity
*84 min video · 4 h practice* · Prerequisites: MID-029, MID-031

**Topics:** Cross-service invariants, reconciliation, exactly-once effects vs guarantees

**Lessons:**
- `SRC-014-L01` Invariants across boundaries (12 min)
- `SRC-014-L02` Exactly-once effects (12 min)
- `SRC-014-L03` Prevent, detect, repair (10 min)
- `SRC-014-L04` Reconciliation design (12 min)
- `SRC-014-L05` Audit trails (8 min)
- `SRC-014-L06` Demo: reconciling orders against the payment provider (15 min)
- `SRC-014-L07` Demo: tracing a double charge to its root cause (15 min)

#### SRC-015 · Advanced troubleshooting
*91 min video · 4.5 h practice* · Prerequisites: MID-008, MID-017, MID-047

**Topics:** Thread starvation, connection exhaustion, deadlocks, cascading failures

**Lessons:**
- `SRC-015-L01` Troubleshooting as hypothesis testing (10 min)
- `SRC-015-L02` Thread starvation (10 min)
- `SRC-015-L03` Connection exhaustion (10 min)
- `SRC-015-L04` Distributed deadlocks and lock convoys (10 min)
- `SRC-015-L05` Cascading and metastable failures (14 min)
- `SRC-015-L06` Cross-layer investigations (10 min)
- `SRC-015-L07` Demo: a retry storm that won't stop by itself (15 min)
- `SRC-015-L08` Demo: latency caused by Kubernetes CPU throttling (12 min)

#### SRC-016 · Performance engineering
*92 min video · 4.5 h practice* · Prerequisites: MID-046, SRC-005

**Topics:** Profiling, benchmark design, bottleneck elimination

**Lessons:**
- `SRC-016-L01` A performance engineering process (10 min)
- `SRC-016-L02` Microbenchmarks with JMH (12 min)
- `SRC-016-L03` System benchmarks that predict production (12 min)
- `SRC-016-L04` Removing bottlenecks in order (10 min)
- `SRC-016-L05` Regression detection in CI (10 min)
- `SRC-016-L06` Reporting results honestly (8 min)
- `SRC-016-L07` Demo: halving checkout p99 with evidence (15 min)
- `SRC-016-L08` Demo: a JMH benchmark that lied, and the fixed version (15 min)

#### SRC-017 · Technical debt
*75 min video · 3.5 h practice* · Prerequisites: MID-065

**Topics:** Classification, prioritization, incremental remediation

**Lessons:**
- `SRC-017-L01` What technical debt is and isn't (10 min)
- `SRC-017-L02` Measuring the interest (12 min)
- `SRC-017-L03` A debt register (8 min)
- `SRC-017-L04` Prioritizing by cost of delay (10 min)
- `SRC-017-L05` Incremental remediation (10 min)
- `SRC-017-L06` Making the case (10 min)
- `SRC-017-L07` Demo: turning a vague complaint into a funded debt item (15 min)

#### SRC-018 · Security reviews
*67 min video · 3.5 h practice* · Prerequisites: MID-052, SRC-010

**Topics:** Threat modeling, authorization boundaries, secure design reviews

**Lessons:**
- `SRC-018-L01` Security reviews engineers run themselves (10 min)
- `SRC-018-L02` Threat modeling at subsystem scale (12 min)
- `SRC-018-L03` Authorization boundaries end to end (12 min)
- `SRC-018-L04` Risk rating and acceptance (10 min)
- `SRC-018-L05` Working with security teams (8 min)
- `SRC-018-L06` Demo: reviewing the redesigned order subsystem (15 min)

#### SRC-019 · Incident leadership
*71 min video · 3.5 h practice* · Prerequisites: MID-050

**Topics:** Coordination, communications, blameless postmortems

**Lessons:**
- `SRC-019-L01` The incident commander role (12 min)
- `SRC-019-L02` Running the response (12 min)
- `SRC-019-L03` Stakeholder communication (10 min)
- `SRC-019-L04` Decisions under uncertainty (10 min)
- `SRC-019-L05` Facilitating postmortems (12 min)
- `SRC-019-L06` Demo: commanding a multi-team incident simulation (15 min)

#### SRC-020 · Mentorship
*63 min video · 3 h practice* · Prerequisites: MID-066

**Topics:** Delegation, code review coaching, design feedback

**Lessons:**
- `SRC-020-L01` Mentoring as a senior responsibility (8 min)
- `SRC-020-L02` Delegation that grows people (12 min)
- `SRC-020-L03` Coaching through reviews (10 min)
- `SRC-020-L04` Design feedback (10 min)
- `SRC-020-L05` Growth plans (8 min)
- `SRC-020-L06` Demo: a coaching review of a junior's design doc (15 min)

---

## Level 5 — Senior Backend Engineer — Grade B (Cross-team design) (`SRB`)

- **Audience:** Senior engineers owning a subsystem.
- **Graduation outcome:** Leads complex multi-team technical initiatives, evolves existing architectures safely, and balances delivery speed, cost, and long-term maintainability.
- **Study hours:** 160–240 plus cross-team delivery experience · **Video hours:** 25–40 · **Lessons:** 65–95
- **Capstone:** `SRB-CAP` Architecture Modernization: Design and lead a simulated migration from a modular monolith to selected services, with phased releases, compatibility guarantees, observability, rollback plans, and measurable outcomes.
- **Graduation gate:** Scenario-based migration review with stakeholder negotiation.

### SRB-P1 — Advanced Distributed Architecture

#### SRB-001 · Distributed architecture patterns
*100 min video · 4.5 h practice* · Prerequisites: MID-022, MID-031

**Topics:** CQRS, event sourcing, sagas, orchestration, materialized views

**Lessons:**
- `SRB-001-L01` Patterns as trade-offs, not upgrades (10 min)
- `SRB-001-L02` CQRS in full (12 min)
- `SRB-001-L03` Event sourcing (14 min)
- `SRB-001-L04` Projections, snapshots, and upcasting (12 min)
- `SRB-001-L05` Materialized views across services (10 min)
- `SRB-001-L06` Workflow engines vs hand-built sagas (12 min)
- `SRB-001-L07` Demo: modeling shipment tracking with and without event sourcing (15 min)
- `SRB-001-L08` Demo: rebuilding a broken projection from the event store (15 min)

#### SRB-002 · Event-driven architecture
*86 min video · 4 h practice* · Prerequisites: MID-062, SRB-001

**Topics:** Event contracts, event ownership, schema evolution, replay

**Lessons:**
- `SRB-002-L01` Event-driven architecture at organization scale (10 min)
- `SRB-002-L02` Kinds of events and when to use each (12 min)
- `SRB-002-L03` Ownership and event catalogs (10 min)
- `SRB-002-L04` Schema evolution across teams (12 min)
- `SRB-002-L05` Replay and backfill (12 min)
- `SRB-002-L06` Demo: designing the Shop ↔ FulfillCo event contract (15 min)
- `SRB-002-L07` Demo: a replay that would have resent 40,000 emails, and the fix (15 min)

#### SRB-003 · Distributed data
*86 min video · 3.5 h practice* · Prerequisites: MID-030, MID-032, SRC-007

**Topics:** Consensus concepts, quorum, replication, consistency models

**Lessons:**
- `SRB-003-L01` Replication strategies (12 min)
- `SRB-003-L02` Consensus and Raft (14 min)
- `SRB-003-L03` Quorums (10 min)
- `SRB-003-L04` Consistency models, revisited (10 min)
- `SRB-003-L05` Reading a Jepsen report (10 min)
- `SRB-003-L06` Demo: partitioning a three-node cluster and watching it choose (15 min)
- `SRB-003-L07` Demo: a quorum read returning stale data, explained (15 min)

#### SRB-004 · Multi-region systems
*94 min video · 4 h practice* · Prerequisites: SRC-013, SRB-003

**Topics:** Active-active vs active-passive, routing, data residency

**Lessons:**
- `SRB-004-L01` Why go multi-region (10 min)
- `SRB-004-L02` Active-passive (12 min)
- `SRB-004-L03` Active-active and conflict handling (14 min)
- `SRB-004-L04` Global traffic routing (10 min)
- `SRB-004-L05` Data residency (10 min)
- `SRB-004-L06` Selective multi-region (8 min)
- `SRB-004-L07` Demo: regional failover of the order path, step by step (15 min)
- `SRB-004-L08` Demo: the hidden single-region dependency that breaks failover (15 min)

#### SRB-005 · High-availability design
*86 min video · 3.5 h practice* · Prerequisites: SRC-009, SRB-004

**Topics:** Redundancy, load shedding, failover, fault containment

**Lessons:**
- `SRB-005-L01` Availability math (12 min)
- `SRB-005-L02` Redundancy and hidden SPOFs (10 min)
- `SRB-005-L03` Load shedding and admission control (12 min)
- `SRB-005-L04` Cell-based architecture (12 min)
- `SRB-005-L05` Shuffle sharding (10 min)
- `SRB-005-L06` Demo: shedding low-priority traffic during a flash sale (15 min)
- `SRB-005-L07` Demo: computing checkout's real availability from its dependencies (15 min)

#### SRB-006 · Large-scale messaging
*92 min video · 3.5 h practice* · Prerequisites: MID-028, SRC-005

**Topics:** Partition strategies, consumer lag, rebalancing, backpressure

**Lessons:**
- `SRB-006-L01` Messaging at scale (8 min)
- `SRB-006-L02` Partition strategy (12 min)
- `SRB-006-L03` Consumer lag (10 min)
- `SRB-006-L04` Rebalancing (10 min)
- `SRB-006-L05` Backpressure end to end (12 min)
- `SRB-006-L06` Cluster capacity and governance (10 min)
- `SRB-006-L07` Demo: recovering from a six-hour consumer backlog (15 min)
- `SRB-006-L08` Demo: choosing partition counts for three years of growth (15 min)

#### SRB-007 · Data platform integration
*86 min video · 4 h practice* · Prerequisites: MID-029, SRB-002

**Topics:** CDC, Debezium, stream processing, analytics pipelines

**Lessons:**
- `SRB-007-L01` Integrating systems you can't change (10 min)
- `SRB-007-L02` Change data capture with Debezium (14 min)
- `SRB-007-L03` From CDC events to domain events (10 min)
- `SRB-007-L04` Stream processing concepts (12 min)
- `SRB-007-L05` Analytics pipelines and data ownership (10 min)
- `SRB-007-L06` Demo: streaming FulfillCo's stock table without touching its code (15 min)
- `SRB-007-L07` Demo: filtering personal data out of a CDC stream (15 min)

#### SRB-008 · Architecture migration
*94 min video · 4.5 h practice* · Prerequisites: SRC-008, SRB-007

**Topics:** Strangler fig, branch by abstraction, dual-write risks

**Lessons:**
- `SRB-008-L01` Why big-bang rewrites fail (10 min)
- `SRB-008-L02` The strangler fig (12 min)
- `SRB-008-L03` Branch by abstraction (10 min)
- `SRB-008-L04` Dual writes and their alternatives (12 min)
- `SRB-008-L05` Moving data ownership (12 min)
- `SRB-008-L06` Rollback and exit criteria (8 min)
- `SRB-008-L07` Demo: extracting shipment tracking from the FulfillCo monolith (15 min)
- `SRB-008-L08` Demo: catching a dual-write inconsistency in production data (15 min)

#### SRB-009 · Service mesh
*90 min video · 3 h practice* · Prerequisites: MID-051, MID-057

**Topics:** mTLS, traffic management, policy enforcement, trade-offs

**Lessons:**
- `SRB-009-L01` What a mesh does (10 min)
- `SRB-009-L02` Mesh architectures (10 min)
- `SRB-009-L03` mTLS and workload identity (12 min)
- `SRB-009-L04` Traffic management (10 min)
- `SRB-009-L05` Policy enforcement (8 min)
- `SRB-009-L06` The cost of a mesh (10 min)
- `SRB-009-L07` Demo: canary traffic split and mTLS with a mesh (15 min)
- `SRB-009-L08` Demo: measuring a mesh's latency and operational overhead (15 min)

#### SRB-010 · Platform engineering
*84 min video · 3.5 h practice* · Prerequisites: MID-055, MID-057

**Topics:** Internal developer platforms, golden paths, self-service capabilities

**Lessons:**
- `SRB-010-L01` Why platform teams exist (10 min)
- `SRB-010-L02` Platform as a product (12 min)
- `SRB-010-L03` Golden paths (10 min)
- `SRB-010-L04` Self-service with guardrails (12 min)
- `SRB-010-L05` Measuring a platform (10 min)
- `SRB-010-L06` Demo: a service template that ships with CI, telemetry, and SLOs (15 min)
- `SRB-010-L07` Demo: interviewing teams to find the platform's first capability (15 min)

#### SRB-021 · AI platform capabilities
*88 min video · 4 h practice* · Prerequisites: SRB-010, SRC-021 · added in v2.0

**Topics:** Shared LLM gateway with quotas, redaction, cost attribution, and routing, shared retrieval services, AI golden path

**Lessons:**
- `SRB-021-L01` Why AI needs platform support (10 min)
- `SRB-021-L02` The LLM gateway (14 min)
- `SRB-021-L03` Quotas, redaction, and cost attribution (12 min)
- `SRB-021-L04` Shared retrieval services and data ownership (12 min)
- `SRB-021-L05` An AI golden path (10 min)
- `SRB-021-L06` Demo: four teams, one gateway, one cost report (15 min)
- `SRB-021-L07` Demo: redacting customer data before it reaches a model (15 min)

### SRB-P2 — Engineering Leadership and Delivery

#### SRB-011 · Cross-team design
*86 min video · 4 h practice* · Prerequisites: SRC-006, SRB-008

**Topics:** Aligning contracts, ownership, timelines, and dependencies

**Lessons:**
- `SRB-011-L01` Designs that cross team boundaries (10 min)
- `SRB-011-L02` Ownership and dependency mapping (12 min)
- `SRB-011-L03` Inclusive design processes (10 min)
- `SRB-011-L04` Contract-first parallel delivery (12 min)
- `SRB-011-L05` Resolving cross-team conflicts (12 min)
- `SRB-011-L06` Demo: a four-team design session for stock synchronization (15 min)
- `SRB-011-L07` Demo: unblocking a team stuck on another team's API (15 min)

#### SRB-012 · Architecture governance
*84 min video · 3 h practice* · Prerequisites: SRC-003, SRC-010

**Topics:** RFCs, design reviews, exception processes

**Lessons:**
- `SRB-012-L01` Governance that helps (10 min)
- `SRB-012-L02` RFC processes (12 min)
- `SRB-012-L03` Running design reviews (12 min)
- `SRB-012-L04` Exceptions and waivers (10 min)
- `SRB-012-L05` Right-sizing governance (10 min)
- `SRB-012-L06` Demo: a design review that improves a proposal without blocking it (15 min)
- `SRB-012-L07` Demo: writing an RFC that gets a decision in one review (15 min)

#### SRB-013 · Technology evaluation
*90 min video · 3.5 h practice* · Prerequisites: MID-044, SRC-003

**Topics:** Proofs of concept, evaluation matrices, decision criteria

**Lessons:**
- `SRB-013-L01` Start with the problem (10 min)
- `SRB-013-L02` Criteria and weights (10 min)
- `SRB-013-L03` Proofs of concept that answer questions (12 min)
- `SRB-013-L04` Evaluation matrices (10 min)
- `SRB-013-L05` Exit costs and lock-in (10 min)
- `SRB-013-L06` Bias in technology choices (8 min)
- `SRB-013-L07` Demo: evaluating two workflow engines in a two-day PoC (15 min)
- `SRB-013-L08` Demo: scoring options and checking the matrix for bias (15 min)

#### SRB-014 · Engineering metrics
*82 min video · 3 h practice* · Prerequisites: MID-055, SRC-012

**Topics:** DORA metrics, reliability indicators, delivery effectiveness

**Lessons:**
- `SRB-014-L01` Why measure delivery (8 min)
- `SRB-014-L02` DORA metrics (14 min)
- `SRB-014-L03` Reliability indicators (10 min)
- `SRB-014-L04` Metrics that backfire (10 min)
- `SRB-014-L05` From metric to improvement experiment (10 min)
- `SRB-014-L06` Demo: diagnosing a slow lead time from pipeline data (15 min)
- `SRB-014-L07` Demo: spotting a metric that is being gamed (15 min)

#### SRB-022 · AI tools across teams
*86 min video · 3.5 h practice* · Prerequisites: MID-072, SRB-014 · added in v2.0

**Topics:** Rolling out coding assistants, usage policy, security review of AI tools, honest impact measurement

**Lessons:**
- `SRB-022-L01` AI assistants as a team capability (10 min)
- `SRB-022-L02` Pilots and rollout (12 min)
- `SRB-022-L03` Usage policy (12 min)
- `SRB-022-L04` Reviewing an AI tool's security (10 min)
- `SRB-022-L05` Measuring impact without fooling yourself (12 min)
- `SRB-022-L06` Demo: designing a two-team pilot with a control group (15 min)
- `SRB-022-L07` Demo: reading a pilot's results that look better than they are (15 min)

#### SRB-015 · Cost optimization
*84 min video · 3.5 h practice* · Prerequisites: MID-056, SRC-004

**Topics:** Infrastructure utilization, cloud cost drivers, FinOps basics

**Lessons:**
- `SRB-015-L01` Cost as an architectural quality (10 min)
- `SRB-015-L02` Cloud cost drivers (12 min)
- `SRB-015-L03` Attribution and unit economics (12 min)
- `SRB-015-L04` Optimization levers (12 min)
- `SRB-015-L05` FinOps basics (8 min)
- `SRB-015-L06` Demo: cutting cost per order by 30% (15 min)
- `SRB-015-L07` Demo: tagging a cloud bill and finding the top three cost drivers (15 min)

#### SRB-016 · Security architecture
*86 min video · 3.5 h practice* · Prerequisites: SRC-018, SRB-009

**Topics:** Identity boundaries, zero-trust principles, service-to-service authorization

**Lessons:**
- `SRB-016-L01` Security architecture vs security features (10 min)
- `SRB-016-L02` Identity boundaries (12 min)
- `SRB-016-L03` Zero trust in practice (12 min)
- `SRB-016-L04` Service-to-service authorization (12 min)
- `SRB-016-L05` Policy as code (10 min)
- `SRB-016-L06` Demo: authorizing FulfillCo services to Shop events and APIs (15 min)
- `SRB-016-L07` Demo: replacing network-based trust with workload identity (15 min)

#### SRB-017 · Large migrations
*94 min video · 4.5 h practice* · Prerequisites: SRC-011, SRB-008

**Topics:** Rollout strategy, feature flags, canary deployment, data backfills

**Lessons:**
- `SRB-017-L01` Anatomy of a large migration (10 min)
- `SRB-017-L02` Rollout strategies (12 min)
- `SRB-017-L03` Shadow traffic and comparison (12 min)
- `SRB-017-L04` Feature flags at program scale (10 min)
- `SRB-017-L05` Backfills (12 min)
- `SRB-017-L06` Decommissioning (8 min)
- `SRB-017-L07` Demo: shadow-reading shipment status from both systems (15 min)
- `SRB-017-L08` Demo: a backfill that has to be stopped and resumed (15 min)

#### SRB-018 · Mentoring senior peers
*82 min video · 3 h practice* · Prerequisites: SRC-020

**Topics:** Design facilitation, conflict resolution, technical influence

**Lessons:**
- `SRB-018-L01` Mentoring people at your own level (10 min)
- `SRB-018-L02` Facilitating design discussions (12 min)
- `SRB-018-L03` Technical conflict resolution (12 min)
- `SRB-018-L04` Influence through understanding (10 min)
- `SRB-018-L05` Peer feedback (8 min)
- `SRB-018-L06` Demo: facilitating a deadlocked design debate (15 min)
- `SRB-018-L07` Demo: giving hard feedback to a senior peer (15 min)

#### SRB-019 · Risk management
*82 min video · 3 h practice* · Prerequisites: SRC-009, SRB-011

**Topics:** Dependency risk, technical uncertainty, contingency planning

**Lessons:**
- `SRB-019-L01` Risk in technical programs (10 min)
- `SRB-019-L02` Identifying risks (10 min)
- `SRB-019-L03` Risk registers that are used (10 min)
- `SRB-019-L04` Buying information early (12 min)
- `SRB-019-L05` Contingency planning (10 min)
- `SRB-019-L06` Demo: a monthly risk review that changes the plan (15 min)
- `SRB-019-L07` Demo: invoking a contingency plan when a dependency slips (15 min)

#### SRB-020 · Stakeholder communication
*82 min video · 3 h practice* · Prerequisites: SRC-017

**Topics:** Business impact, status reporting, technical proposals

**Lessons:**
- `SRB-020-L01` Knowing your audience (10 min)
- `SRB-020-L02` Business impact framing (12 min)
- `SRB-020-L03` Status reports (10 min)
- `SRB-020-L04` Technical proposals for decision-makers (12 min)
- `SRB-020-L05` Delivering bad news (8 min)
- `SRB-020-L06` Demo: rewriting an engineering update for the executive team (15 min)
- `SRB-020-L07` Demo: telling leadership the program is four weeks late (15 min)

---

## Level 6 — Senior Backend Engineer — Grade A (Technical leadership) (`SRA`)

- **Audience:** Senior engineers leading cross-team work.
- **Graduation outcome:** Shapes the technical direction of a major product area, resolves difficult architectural problems, establishes engineering standards, and influences several teams without formal authority.
- **Study hours:** 160–240 plus organizational leadership experience · **Video hours:** 25–40 · **Lessons:** 65–95
- **Capstone:** `SRA-CAP` Multi-Year Platform Evolution: Three-year architecture evolution strategy for a growing commerce platform: capacity assumptions, modernization sequencing, security and reliability objectives, cost estimates, and governance.
- **Graduation gate:** Strategy defense before a simulated leadership panel.

### SRA-P1 — Advanced System Strategy

#### SRA-001 · Architecture at scale
*86 min video · 4 h practice* · Prerequisites: SRB-010, SRB-012

**Topics:** Organizational architecture, platform boundaries, evolutionary architecture

**Lessons:**
- `SRA-001-L01` From system architecture to organizational architecture (12 min)
- `SRA-001-L02` Platforms, domains, and shared capabilities (12 min)
- `SRA-001-L03` Drawing platform boundaries (10 min)
- `SRA-001-L04` Evolutionary architecture (12 min)
- `SRA-001-L05` Reading misalignment between teams and systems (10 min)
- `SRA-001-L06` Demo: mapping the Commerce 2030 landscape (15 min)
- `SRA-001-L07` Demo: moving one capability from product teams into a platform (15 min)

#### SRA-002 · Long-term system evolution
*84 min video · 3.5 h practice* · Prerequisites: SRB-014, SRA-001

**Topics:** Architectural fitness functions, technical roadmaps, obsolescence

**Lessons:**
- `SRA-002-L01` Architecture decays unless guided (10 min)
- `SRA-002-L02` Fitness functions (12 min)
- `SRA-002-L03` Automating fitness functions (10 min)
- `SRA-002-L04` Technical roadmaps: target and transition states (12 min)
- `SRA-002-L05` Managing obsolescence (10 min)
- `SRA-002-L06` Demo: a fitness function that blocks a coupling regression (15 min)
- `SRA-002-L07` Demo: replanning a roadmap after a vendor end-of-life notice (15 min)

#### SRA-003 · Complex domain modeling
*88 min video · 4 h practice* · Prerequisites: MID-060, SRB-002

**Topics:** Strategic DDD, context mapping, anti-corruption layers

**Lessons:**
- `SRA-003-L01` Strategic DDD (12 min)
- `SRA-003-L02` Core, supporting, and generic subdomains (10 min)
- `SRA-003-L03` Context mapping patterns (14 min)
- `SRA-003-L04` Anti-corruption layers (10 min)
- `SRA-003-L05` Event storming at scale (12 min)
- `SRA-003-L06` Demo: event storming the seller marketplace (15 min)
- `SRA-003-L07` Demo: an anti-corruption layer around a carrier API (15 min)

#### SRA-004 · Data ownership strategy
*84 min video · 3.5 h practice* · Prerequisites: SRB-007, SRA-003

**Topics:** Federated ownership, governance, data contracts

**Lessons:**
- `SRA-004-L01` Who owns the data (10 min)
- `SRA-004-L02` Federated ownership (12 min)
- `SRA-004-L03` Data contracts (12 min)
- `SRA-004-L04` Federated governance (10 min)
- `SRA-004-L05` Data mesh: ideas and limits (10 min)
- `SRA-004-L06` Demo: writing a data contract for order events used by finance (15 min)
- `SRA-004-L07` Demo: resolving a dispute over who owns "customer" (15 min)

#### SRA-005 · Multi-region trade-offs
*84 min video · 3.5 h practice* · Prerequisites: SRB-003, SRB-004

**Topics:** Availability vs consistency, jurisdiction, operational complexity

**Lessons:**
- `SRA-005-L01` Multi-region as a business decision (10 min)
- `SRA-005-L02` Consistency needs per capability (12 min)
- `SRA-005-L03` Jurisdiction and data transfer (12 min)
- `SRA-005-L04` The operational cost of regions (10 min)
- `SRA-005-L05` Sequencing geographic expansion (10 min)
- `SRA-005-L06` Demo: a capability-by-capability region decision table (15 min)
- `SRA-005-L07` Demo: costing three expansion options (15 min)

#### SRA-006 · Enterprise resilience
*84 min video · 3.5 h practice* · Prerequisites: SRC-013, SRB-005

**Topics:** Regional failure, chaos engineering, systemic risk

**Lessons:**
- `SRA-006-L01` Resilience at organization scale (10 min)
- `SRA-006-L02` Regional and provider failure (12 min)
- `SRA-006-L03` Chaos engineering as a program (12 min)
- `SRA-006-L04` Systemic and correlated risk (12 min)
- `SRA-006-L05` Resilience investment cases (8 min)
- `SRA-006-L06` Demo: a chaos experiment with a hypothesis and abort criteria (15 min)
- `SRA-006-L07` Demo: finding the shared dependency behind three "unrelated" incidents (15 min)

#### SRA-007 · Large-scale performance
*84 min video · 3.5 h practice* · Prerequisites: SRC-016, SRB-015

**Topics:** Capacity forecasting, workload modeling, cost-performance optimization

**Lessons:**
- `SRA-007-L01` Capacity at product-area scale (10 min)
- `SRA-007-L02` Forecasting from business drivers (12 min)
- `SRA-007-L03` Workload modeling (12 min)
- `SRA-007-L04` Cost-performance optimization (12 min)
- `SRA-007-L05` Performance budgets for teams (8 min)
- `SRA-007-L06` Demo: forecasting the marketplace launch's load (15 min)
- `SRA-007-L07` Demo: trading 10 ms of latency for 25% lower cost (15 min)

#### SRA-008 · Architecture economics
*84 min video · 3.5 h practice* · Prerequisites: SRB-013, SRB-015

**Topics:** Build vs buy, total cost of ownership, opportunity cost

**Lessons:**
- `SRA-008-L01` Architecture decisions are investment decisions (10 min)
- `SRA-008-L02` Build vs buy vs open source (12 min)
- `SRA-008-L03` Total cost of ownership (12 min)
- `SRA-008-L04` Opportunity cost (10 min)
- `SRA-008-L05` Real options thinking (10 min)
- `SRA-008-L06` Demo: buy vs build for marketplace seller payouts (15 min)
- `SRA-008-L07` Demo: a finance review of an architecture business case (15 min)

#### SRA-021 · AI strategy and build vs buy
*88 min video · 4 h practice* · Prerequisites: SRA-008, SRB-021 · added in v2.0

**Topics:** Where AI creates value, hosted vs open-weight models, RAG vs fine-tuning, total cost of ownership, lock-in, data strategy

**Lessons:**
- `SRA-021-L01` Finding real AI value (12 min)
- `SRA-021-L02` Hosted, open-weight, or managed (12 min)
- `SRA-021-L03` Prompting, RAG, or fine-tuning (12 min)
- `SRA-021-L04` AI total cost of ownership and lock-in (12 min)
- `SRA-021-L05` Data foundations for AI (10 min)
- `SRA-021-L06` Demo: scoring ten AI ideas for the marketplace (15 min)
- `SRA-021-L07` Demo: hosted API vs self-hosted model, three-year cost (15 min)

#### SRA-009 · Security and compliance
*84 min video · 3.5 h practice* · Prerequisites: SRC-014, SRB-016

**Topics:** Privacy by design, auditability, regulatory constraints

**Lessons:**
- `SRA-009-L01` Compliance as an architecture driver (10 min)
- `SRA-009-L02` Privacy by design (12 min)
- `SRA-009-L03` Auditability (10 min)
- `SRA-009-L04` From regulation to requirements (12 min)
- `SRA-009-L05` Reducing compliance scope (10 min)
- `SRA-009-L06` Demo: shrinking PCI scope with tokenization (15 min)
- `SRA-009-L07` Demo: designing data deletion across 30 services (15 min)

#### SRA-022 · Responsible AI and AI compliance
*86 min video · 3.5 h practice* · Prerequisites: SRA-009, SRA-021 · added in v2.0

**Topics:** Privacy, residency of model calls, transparency, bias, human oversight, auditability, regulation at concept level

**Lessons:**
- `SRA-022-L01` Responsible AI as engineering (10 min)
- `SRA-022-L02` Privacy and residency of model calls (12 min)
- `SRA-022-L03` Risk-based classification of AI use cases (12 min)
- `SRA-022-L04` Transparency, bias, and human oversight (12 min)
- `SRA-022-L05` Auditability of AI decisions (10 min)
- `SRA-022-L06` Demo: risk-classifying the marketplace's AI features (15 min)
- `SRA-022-L07` Demo: designing human oversight for automated seller suspensions (15 min)

#### SRA-010 · Technical strategy
*94 min video · 4.5 h practice* · Prerequisites: SRA-002, SRA-008

**Topics:** Investment planning, modernization, platform vs product priorities

**Lessons:**
- `SRA-010-L01` What a technical strategy is (10 min)
- `SRA-010-L02` Diagnosis (12 min)
- `SRA-010-L03` Guiding policies (12 min)
- `SRA-010-L04` Coherent actions and investment allocation (12 min)
- `SRA-010-L05` Prioritizing modernization (10 min)
- `SRA-010-L06` Measuring and revising strategy (8 min)
- `SRA-010-L07` Demo: writing the diagnosis for Commerce 2030 (15 min)
- `SRA-010-L08` Demo: defending a 30% platform allocation to product leadership (15 min)

### SRA-P2 — Influence and Organizational Execution

#### SRA-011 · Technical vision
*82 min video · 4 h practice* · Prerequisites: SRA-010

**Topics:** Writing and communicating a multi-year engineering vision

**Lessons:**
- `SRA-011-L01` Why teams need a technical vision (10 min)
- `SRA-011-L02` Vision, strategy, and roadmap (10 min)
- `SRA-011-L03` Writing a vision people can use (12 min)
- `SRA-011-L04` Telling the vision as a story (10 min)
- `SRA-011-L05` Feedback without dilution (10 min)
- `SRA-011-L06` Demo: drafting the Commerce 2030 vision document (15 min)
- `SRA-011-L07` Demo: presenting the vision to an all-hands of engineers (15 min)

#### SRA-012 · Engineering standards
*80 min video · 3 h practice* · Prerequisites: SRB-012, SRA-001

**Topics:** Standardization without unnecessary centralization

**Lessons:**
- `SRA-012-L01` The cost and value of standards (10 min)
- `SRA-012-L02` What to standardize (12 min)
- `SRA-012-L03` Principles, defaults, exceptions (10 min)
- `SRA-012-L04` Adoption through paved roads (10 min)
- `SRA-012-L05` Retiring standards (8 min)
- `SRA-012-L06` Demo: writing an observability standard teams accept (15 min)
- `SRA-012-L07` Demo: handling a team that wants an exception (15 min)

#### SRA-013 · Decision-making under uncertainty
*82 min video · 3 h practice* · Prerequisites: SRC-003, SRB-019

**Topics:** Assumptions, experiments, option value, decision records

**Lessons:**
- `SRA-013-L01` Deciding without all the facts (10 min)
- `SRA-013-L02` Surfacing and ranking assumptions (12 min)
- `SRA-013-L03` Experiments that buy information (12 min)
- `SRA-013-L04` Option value and commitment timing (10 min)
- `SRA-013-L05` Decision records with assumptions (8 min)
- `SRA-013-L06` Demo: an assumption map for the marketplace launch (15 min)
- `SRA-013-L07` Demo: revisiting a decision when its key assumption fails (15 min)

#### SRA-014 · Leading ambiguous initiatives
*80 min video · 3.5 h practice* · Prerequisites: SRB-011, SRA-013

**Topics:** Defining problems, building alignment, sequencing delivery

**Lessons:**
- `SRA-014-L01` Ambiguity is the job (10 min)
- `SRA-014-L02` Defining the problem (12 min)
- `SRA-014-L03` Alignment before solutions (10 min)
- `SRA-014-L04` Sequencing for early value (10 min)
- `SRA-014-L05` Handing off (8 min)
- `SRA-014-L06` Demo: turning "the platform is slow to change" into a defined initiative (15 min)
- `SRA-014-L07` Demo: the first 30 days of an ambiguous initiative (15 min)

#### SRA-015 · Cross-functional leadership
*82 min video · 3 h practice* · Prerequisites: SRB-020

**Topics:** Working with product, security, finance, infrastructure

**Lessons:**
- `SRA-015-L01` Engineering is one function among several (10 min)
- `SRA-015-L02` What product, finance, and security need from you (12 min)
- `SRA-015-L03` Joint planning (10 min)
- `SRA-015-L04` Negotiating as peers (12 min)
- `SRA-015-L05` Building relationships across functions (8 min)
- `SRA-015-L06` Demo: a joint planning session with product and finance (15 min)
- `SRA-015-L07` Demo: negotiating a security requirement that threatens a launch date (15 min)

#### SRA-016 · Engineering capability development
*80 min video · 3 h practice* · Prerequisites: SRB-018

**Topics:** Mentorship systems, communities of practice, knowledge sharing

**Lessons:**
- `SRA-016-L01` Capability is a system, not a talent (10 min)
- `SRA-016-L02` Assessing capability gaps (10 min)
- `SRA-016-L03` Mentorship systems (10 min)
- `SRA-016-L04` Communities of practice (12 min)
- `SRA-016-L05` Measuring capability growth (8 min)
- `SRA-016-L06` Demo: launching a reliability guild (15 min)
- `SRA-016-L07` Demo: a capability gap analysis across eight teams (15 min)

#### SRA-017 · Architectural reviews
*80 min video · 3.5 h practice* · Prerequisites: SRC-018, SRB-012

**Topics:** Reviewing designs for risk, complexity, and operability

**Lessons:**
- `SRA-017-L01` The reviewer's job (10 min)
- `SRA-017-L02` Reviewing for risk (12 min)
- `SRA-017-L03` Reviewing for complexity and operability (12 min)
- `SRA-017-L04` Blocking issues vs preferences (8 min)
- `SRA-017-L05` Questions that teach (8 min)
- `SRA-017-L06` Demo: reviewing a team's marketplace search design (15 min)
- `SRA-017-L07` Demo: a review that finds a data-loss risk through questions alone (15 min)

#### SRA-018 · Organizational bottlenecks
*82 min video · 3 h practice* · Prerequisites: SRC-008, SRA-001

**Topics:** Coordination costs, team boundaries, Conway's Law

**Lessons:**
- `SRA-018-L01` Conway's Law (10 min)
- `SRA-018-L02` Measuring coordination cost (12 min)
- `SRA-018-L03` Team topologies and cognitive load (12 min)
- `SRA-018-L04` The inverse Conway maneuver (10 min)
- `SRA-018-L05` Working with managers on team design (8 min)
- `SRA-018-L06` Demo: finding the team that every change waits on (15 min)
- `SRA-018-L07` Demo: proposing a team split aligned with the context map (15 min)

#### SRA-019 · Executive communication
*80 min video · 3 h practice* · Prerequisites: SRB-020, SRA-011

**Topics:** Technical risk translated into business impact

**Lessons:**
- `SRA-019-L01` How executives decide (10 min)
- `SRA-019-L02` From technical risk to business impact (12 min)
- `SRA-019-L03` The executive brief (10 min)
- `SRA-019-L04` Handling hard questions (10 min)
- `SRA-019-L05` Getting to a decision (8 min)
- `SRA-019-L06` Demo: a 10-minute funding pitch for the modernization program (15 min)
- `SRA-019-L07` Demo: briefing the CEO after a major outage (15 min)

#### SRA-020 · Succession and delegation
*78 min video · 2.5 h practice* · Prerequisites: SRB-018

**Topics:** Creating ownership and reducing key-person dependencies

**Lessons:**
- `SRA-020-L01` Key-person risk (10 min)
- `SRA-020-L02` Delegating ownership (12 min)
- `SRA-020-L03` Decision rights (8 min)
- `SRA-020-L04` Growing successors (10 min)
- `SRA-020-L05` Knowledge that survives you (8 min)
- `SRA-020-L06` Demo: mapping your own key-person risks (15 min)
- `SRA-020-L07` Demo: a handover of decision rights for the event platform (15 min)

---

## Level 7 — Staff Software Engineer (`STF`)

- **Audience:** Senior engineers moving toward organization-wide scope. Related track, not a mandatory step after SRA.
- **Graduation outcome:** Identifies systemic technical problems, creates organization-wide leverage, leads strategic engineering programs, and improves the effectiveness of multiple teams.
- **Study hours:** 180–280; role readiness requires demonstrated organizational impact · **Video hours:** 30–45 · **Lessons:** 70–100
- **Capstone:** `STF-CAP` Internal Developer Platform: Platform for 10–20 hypothetical product teams: architecture, self-service deployment, CI/CD, observability and security standards, service templates, adoption roadmap, cost model, governance, success metrics.
- **Graduation gate:** Assessed on organizational leverage, not only code quality.

### STF-P1 — Staff-Level Technical Strategy

#### STF-001 · Staff engineering role
*100 min video · 3 h practice* · Prerequisites: SRA-014, SRA-020

**Topics:** Scope, leverage, influence, archetypes, boundaries with management

**Lessons:**
- `STF-001-L01` What organizations hire Staff engineers to do (12 min)
- `STF-001-L02` Scope, time horizon, and leverage (12 min)
- `STF-001-L03` Staff archetypes (12 min)
- `STF-001-L04` Staff engineers and managers: a partnership (12 min)
- `STF-001-L05` Choosing work by leverage (12 min)
- `STF-001-L06` Staying technical without a team (10 min)
- `STF-001-L07` Demo: the first 90 days in Platform 2.0 (15 min)
- `STF-001-L08` Demo: saying no to a high-visibility, low-leverage request (15 min)

#### STF-002 · Technical strategy
*100 min video · 4.5 h practice* · Prerequisites: SRA-010, STF-001

**Topics:** Connecting business priorities to engineering investment

**Lessons:**
- `STF-002-L01` Strategy at organization scale (12 min)
- `STF-002-L02` From business priorities to engineering bets (14 min)
- `STF-002-L03` Gathering evidence across 20 teams (12 min)
- `STF-002-L04` Writing the diagnosis (12 min)
- `STF-002-L05` What we will stop doing (10 min)
- `STF-002-L06` Endorsement and refresh cycles (10 min)
- `STF-002-L07` Demo: diagnosing Platform 2.0 from delivery and incident data (15 min)
- `STF-002-L08` Demo: turning three business goals into two engineering bets (15 min)

#### STF-003 · Architecture governance at scale
*98 min video · 3.5 h practice* · Prerequisites: SRB-012, SRA-012

**Topics:** Principles, reference architectures, decision rights

**Lessons:**
- `STF-003-L01` Governance as an enabling system (12 min)
- `STF-003-L02` Principles that decide things (12 min)
- `STF-003-L03` Reference architectures (12 min)
- `STF-003-L04` Decision rights (12 min)
- `STF-003-L05` Measuring the cost of governance (10 min)
- `STF-003-L06` Evolving governance as the organization grows (10 min)
- `STF-003-L07` Demo: writing a decision-rights matrix with engineering managers (15 min)
- `STF-003-L08` Demo: a reference architecture for event-driven services (15 min)

#### STF-004 · Platform strategy
*100 min video · 4.5 h practice* · Prerequisites: SRB-010, STF-002

**Topics:** Developer experience, paved roads, internal platforms

**Lessons:**
- `STF-004-L01` Why internal platforms succeed or fail (12 min)
- `STF-004-L02` Developer journeys and toil mapping (12 min)
- `STF-004-L03` Paved roads and escape hatches (12 min)
- `STF-004-L04` The platform as a product (12 min)
- `STF-004-L05` Build, assemble, or buy platform capabilities (12 min)
- `STF-004-L06` Funding and staffing a platform team (10 min)
- `STF-004-L07` Demo: mapping the "new service to production" journey across five teams (15 min)
- `STF-004-L08` Demo: choosing the platform's first three capabilities (15 min)

#### STF-005 · Organization-wide reliability
*96 min video · 4 h practice* · Prerequisites: SRC-012, SRA-006

**Topics:** Reliability programs, systemic risk reduction, operational maturity

**Lessons:**
- `STF-005-L01` Reliability as an organizational property (12 min)
- `STF-005-L02` Mining incidents for systemic causes (12 min)
- `STF-005-L03` Designing a reliability program (12 min)
- `STF-005-L04` Operational maturity models (10 min)
- `STF-005-L05` On-call health (10 min)
- `STF-005-L06` Reporting reliability to leadership (10 min)
- `STF-005-L07` Demo: finding the cause behind 30 incidents in 12 teams (15 min)
- `STF-005-L08` Demo: a quarterly reliability review with the CTO (15 min)

#### STF-006 · Cross-domain systems
*90 min video · 4 h practice* · Prerequisites: SRA-003, SRA-004

**Topics:** Identity, billing, commerce, data, integration platforms

**Lessons:**
- `STF-006-L01` Systems everyone depends on (12 min)
- `STF-006-L02` Identity, billing, and data as cross-domain capabilities (14 min)
- `STF-006-L03` Shared platform or domain-owned? (12 min)
- `STF-006-L04` Ownership and funding of shared systems (10 min)
- `STF-006-L05` Evolving a shared system safely (12 min)
- `STF-006-L06` Demo: untangling three competing customer-identity systems (15 min)
- `STF-006-L07` Demo: a funding model for the shared integration platform (15 min)

#### STF-007 · Technology portfolio
*88 min video · 3.5 h practice* · Prerequisites: SRB-013, SRA-002

**Topics:** Standardization, consolidation, adoption, retirement

**Lessons:**
- `STF-007-L01` Technology choices as a portfolio (12 min)
- `STF-007-L02` A technology radar that people use (12 min)
- `STF-007-L03` Standardize, consolidate, or diversify (12 min)
- `STF-007-L04` Introducing new technology safely (10 min)
- `STF-007-L05` Retiring technology (12 min)
- `STF-007-L06` Demo: building the first Platform 2.0 technology radar (15 min)
- `STF-007-L07` Demo: retiring a second message broker across eight teams (15 min)

#### STF-008 · Security architecture strategy
*98 min video · 3.5 h practice* · Prerequisites: SRB-016, SRA-009

**Topics:** Threat landscapes, trust boundaries, secure defaults

**Lessons:**
- `STF-008-L01` Security strategy vs security reviews (10 min)
- `STF-008-L02` Threat landscape for a commerce organization (12 min)
- `STF-008-L03` Organization-wide trust boundaries (12 min)
- `STF-008-L04` Secure defaults in the platform (14 min)
- `STF-008-L05` Supply-chain security at scale (10 min)
- `STF-008-L06` A joint roadmap with security (10 min)
- `STF-008-L07` Demo: turning five recurring audit findings into platform defaults (15 min)
- `STF-008-L08` Demo: a trust-boundary map for the whole organization (15 min)

#### STF-009 · Engineering productivity
*98 min video · 4 h practice* · Prerequisites: SRB-014, STF-004

**Topics:** Build pipelines, developer tooling, feedback loops

**Lessons:**
- `STF-009-L01` What productivity means for engineers (12 min)
- `STF-009-L02` Measuring without surveillance (12 min)
- `STF-009-L03` Feedback loops: where time goes (12 min)
- `STF-009-L04` Build and test pipelines at scale (12 min)
- `STF-009-L05` Onboarding as a product (10 min)
- `STF-009-L06` Making the business case (10 min)
- `STF-009-L07` Demo: cutting a 40-minute CI pipeline to 8 minutes (15 min)
- `STF-009-L08` Demo: running a developer-experience survey and acting on it (15 min)

#### STF-021 · AI governance and engineering productivity
*88 min video · 4 h practice* · Prerequisites: SRB-022, STF-009 · added in v2.0

**Topics:** Approved tools, usage policy, evaluation standards, quality and security guardrails, measuring productivity honestly

**Lessons:**
- `STF-021-L01` Why AI needs governance, not prohibition (10 min)
- `STF-021-L02` Approved tools, data rules, and decision rights (12 min)
- `STF-021-L03` Evaluation and quality standards (12 min)
- `STF-021-L04` Guardrails as paved roads (12 min)
- `STF-021-L05` Measuring AI's effect on engineering (12 min)
- `STF-021-L06` Demo: turning an AI policy into platform guardrails (15 min)
- `STF-021-L07` Demo: an org-wide AI productivity report with honest caveats (15 min)

#### STF-010 · Technical due diligence
*96 min video · 3.5 h practice* · Prerequisites: SRA-008, STF-007

**Topics:** Assessing architecture, risk, team capabilities, modernization needs

**Lessons:**
- `STF-010-L01` When due diligence is needed (10 min)
- `STF-010-L02` Assessing architecture and code health (12 min)
- `STF-010-L03` Assessing operations and security (12 min)
- `STF-010-L04` Assessing team capability and key-person risk (12 min)
- `STF-010-L05` Risk severity and remediation cost (10 min)
- `STF-010-L06` Writing the report (10 min)
- `STF-010-L07` Demo: a two-week due diligence of an acquisition target (15 min)
- `STF-010-L08` Demo: presenting findings to a deal team (15 min)

### STF-P2 — Influence, Communication, and Leadership

#### STF-011 · Influence without authority
*98 min video · 3.5 h practice* · Prerequisites: SRB-018, STF-001

**Topics:** Trust, alignment, negotiation, conflict management

**Lessons:**
- `STF-011-L01` Authority you have vs influence you build (12 min)
- `STF-011-L02` Trust and credibility (12 min)
- `STF-011-L03` Stakeholder mapping (10 min)
- `STF-011-L04` Negotiation for engineers (14 min)
- `STF-011-L05` Conflict management (12 min)
- `STF-011-L06` Influence and integrity (8 min)
- `STF-011-L07` Demo: winning over a skeptical tech lead (15 min)
- `STF-011-L08` Demo: negotiating platform migration timing with three managers (15 min)

#### STF-012 · Technical proposals
*98 min video · 4 h practice* · Prerequisites: SRB-012, STF-011

**Topics:** Problem framing, RFCs, evidence, alternatives

**Lessons:**
- `STF-012-L01` Why good ideas fail on paper (10 min)
- `STF-012-L02` Problem framing (12 min)
- `STF-012-L03` Evidence and alternatives (12 min)
- `STF-012-L04` Structure of a strong RFC (12 min)
- `STF-012-L05` Running the review to a decision (12 min)
- `STF-012-L06` One proposal, three audiences (10 min)
- `STF-012-L07` Demo: rewriting a rejected RFC so it gets approved (15 min)
- `STF-012-L08` Demo: handling 60 comments on a controversial proposal (15 min)

#### STF-013 · Cross-team programs
*96 min video · 4 h practice* · Prerequisites: SRB-011, SRA-014

**Topics:** Dependencies, milestones, accountability, escalation

**Lessons:**
- `STF-013-L01` Programs vs projects (10 min)
- `STF-013-L02` Milestones that show progress (12 min)
- `STF-013-L03` Dependencies and the critical path (12 min)
- `STF-013-L04` Accountability without authority (12 min)
- `STF-013-L05` Escalation done well (10 min)
- `STF-013-L06` Working with technical program managers (10 min)
- `STF-013-L07` Demo: a program review for the migration of 20 teams' pipelines (15 min)
- `STF-013-L08` Demo: escalating a blocked dependency with options (15 min)

#### STF-014 · Organizational change
*94 min video · 3.5 h practice* · Prerequisites: SRA-018, STF-011

**Topics:** Adoption strategies, incentives, resistance, feedback

**Lessons:**
- `STF-014-L01` Why technical change is organizational change (12 min)
- `STF-014-L02` Adoption curves and early adopters (12 min)
- `STF-014-L03` Incentives (10 min)
- `STF-014-L04` Understanding resistance (12 min)
- `STF-014-L05` Feedback loops during change (10 min)
- `STF-014-L06` When to stop pushing (8 min)
- `STF-014-L07` Demo: picking the first three teams for the golden path (15 min)
- `STF-014-L08` Demo: an adoption review that changes the plan (15 min)

#### STF-022 · Leading an AI adoption program
*86 min video · 3.5 h practice* · Prerequisites: STF-014, STF-021 · added in v2.0

**Topics:** Adoption strategy, enablement, communities, risk management, measuring outcomes across the organization

**Lessons:**
- `STF-022-L01` AI adoption is organizational change (10 min)
- `STF-022-L02` Champions, enablement, and communities (12 min)
- `STF-022-L03` Resistance and trust (12 min)
- `STF-022-L04` Managing adoption risk (12 min)
- `STF-022-L05` Reporting and adjusting (10 min)
- `STF-022-L06` Demo: a town hall on AI tools with skeptical engineers (15 min)
- `STF-022-L07` Demo: pausing a rollout after a quality drop (15 min)

#### STF-015 · Mentoring at scale
*94 min video · 3 h practice* · Prerequisites: SRA-016

**Topics:** Growing senior engineers, technical communities

**Lessons:**
- `STF-015-L01` From mentoring people to growing an organization (10 min)
- `STF-015-L02` Mentoring vs sponsorship (12 min)
- `STF-015-L03` Stretch assignments (10 min)
- `STF-015-L04` Technical communities that last (12 min)
- `STF-015-L05` Scaling knowledge: talks, docs, office hours (10 min)
- `STF-015-L06` Inclusive sponsorship (10 min)
- `STF-015-L07` Demo: a sponsorship conversation with a senior engineer (15 min)
- `STF-015-L08` Demo: relaunching a dying architecture community (15 min)

#### STF-016 · Decision facilitation
*94 min video · 3 h practice* · Prerequisites: SRB-018, SRA-013

**Topics:** Managing disagreements, clarifying trade-offs, building consensus

**Lessons:**
- `STF-016-L01` Why technical decisions get stuck (10 min)
- `STF-016-L02` Structuring a decision (12 min)
- `STF-016-L03` Making trade-offs explicit (12 min)
- `STF-016-L04` Consensus and its limits (10 min)
- `STF-016-L05` Disagree and commit (10 min)
- `STF-016-L06` Decisions that stick (10 min)
- `STF-016-L07` Demo: facilitating the "one CI system or many" debate (15 min)
- `STF-016-L08` Demo: a decision meeting where the facilitator does not decide (15 min)

#### STF-017 · Executive communication
*88 min video · 3.5 h practice* · Prerequisites: SRA-019, STF-002

**Topics:** Business cases, cost/risk narratives, technical storytelling

**Lessons:**
- `STF-017-L01` What executives need from Staff engineers (12 min)
- `STF-017-L02` The engineering business case (14 min)
- `STF-017-L03` Cost and risk narratives (12 min)
- `STF-017-L04` Technical storytelling (12 min)
- `STF-017-L05` Ongoing executive relationships (8 min)
- `STF-017-L06` Demo: the Platform 2.0 business case for the board (15 min)
- `STF-017-L07` Demo: explaining a year of platform spend to the CFO (15 min)

#### STF-018 · Incident and crisis leadership
*94 min video · 3.5 h practice* · Prerequisites: SRC-019, STF-005

**Topics:** Coordinating major incidents, strategic corrective actions

**Lessons:**
- `STF-018-L01` When an incident becomes a crisis (10 min)
- `STF-018-L02` Leading many teams in an incident (12 min)
- `STF-018-L03` Crisis communication (12 min)
- `STF-018-L04` From postmortem to strategic action (12 min)
- `STF-018-L05` Improving the incident process (10 min)
- `STF-018-L06` Looking after responders (8 min)
- `STF-018-L07` Demo: a simulated payment-provider outage on the busiest day of the year (15 min)
- `STF-018-L08` Demo: presenting a crisis review to the executive team (15 min)

#### STF-019 · Measuring impact
*86 min video · 3.5 h practice* · Prerequisites: SRB-014, STF-002

**Topics:** Adoption, reliability, cost, delivery, developer experience

**Lessons:**
- `STF-019-L01` Why Staff work is hard to measure (10 min)
- `STF-019-L02` Choosing success measures up front (12 min)
- `STF-019-L03` Leading and lagging indicators (12 min)
- `STF-019-L04` Attribution and honesty (12 min)
- `STF-019-L05` Impact dashboards (10 min)
- `STF-019-L06` Demo: the Platform 2.0 success metrics, from baseline to target (15 min)
- `STF-019-L07` Demo: an impact report that admits what did not work (15 min)

#### STF-020 · Staff career development
*96 min video · 3 h practice* · Prerequisites: STF-001, STF-019

**Topics:** Promotion evidence, influence mapping, sustainable leadership

**Lessons:**
- `STF-020-L01` How Staff promotions are decided (12 min)
- `STF-020-L02` Building a promotion packet (12 min)
- `STF-020-L03` Influence mapping (10 min)
- `STF-020-L04` Staff, Principal, manager, or architect (12 min)
- `STF-020-L05` Sustainable leadership (10 min)
- `STF-020-L06` Staying technical (10 min)
- `STF-020-L07` Demo: reviewing a Staff promotion packet with a calibration panel (15 min)
- `STF-020-L08` Demo: planning a quarter that protects deep work (15 min)

---

## Level 8 — Solution Architect (`ARC`)

- **Audience:** Senior engineers moving toward end-to-end solution design. Related track, not a mandatory step after STF.
- **Graduation outcome:** Designs a complete solution connecting business requirements, applications, integrations, infrastructure, security, data, operations, delivery, and cost.
- **Study hours:** 220–350 with extensive case-study and stakeholder practice · **Video hours:** 40–60 · **Lessons:** 100–140
- **Capstone:** `ARC-CAP` Enterprise Digital Commerce Platform: Complete solution architecture package for a retailer (web/mobile, inventory, payments, fulfillment, customer service, reporting, ERP integration), from requirements to executive presentation.
- **Graduation gate:** Defend the solution in a simulated architecture review with competing requirements, budget constraints, changing priorities, and failure scenarios.

### ARC-P1 — Business and Enterprise Architecture Foundations

#### ARC-001 · Architecture roles
*67 min video · 2.5 h practice* · Prerequisites: SRC-010

**Topics:** Software, solution, enterprise, cloud, and data architects

**Lessons:**
- `ARC-001-L01` What architects actually do (10 min)
- `ARC-001-L02` Software, solution, enterprise, cloud, and data architects (12 min)
- `ARC-001-L03` The solution architect in a program (12 min)
- `ARC-001-L04` Accountabilities and boundaries (10 min)
- `ARC-001-L05` From senior engineer to architect (10 min)
- `ARC-001-L06` Demo: mapping the architecture roles on the Larkspur program (13 min)

#### ARC-002 · Business architecture
*79 min video · 3.5 h practice* · Prerequisites: SRA-001, ARC-001

**Topics:** Capabilities, processes, value streams, stakeholders

**Lessons:**
- `ARC-002-L01` Why architects start with the business (8 min)
- `ARC-002-L02` Business capabilities (12 min)
- `ARC-002-L03` Capability maps and heat maps (10 min)
- `ARC-002-L04` Value streams and processes (12 min)
- `ARC-002-L05` Stakeholder mapping (8 min)
- `ARC-002-L06` Demo: Larkspur's capability map, built live (15 min)
- `ARC-002-L07` Demo: tracing "buy online, pick up in store" across capabilities (14 min)

#### ARC-003 · Requirements discovery
*93 min video · 4 h practice* · Prerequisites: SRC-001, ARC-002

**Topics:** Workshops, interviews, functional/nonfunctional requirements

**Lessons:**
- `ARC-003-L01` Discovery as the architect's first deliverable (8 min)
- `ARC-003-L02` Planning workshops and interviews (12 min)
- `ARC-003-L03` Facilitation techniques (12 min)
- `ARC-003-L04` Functional requirements and journeys (10 min)
- `ARC-003-L05` Nonfunctional requirements that can be tested (12 min)
- `ARC-003-L06` Constraints, assumptions, and conflicts (10 min)
- `ARC-003-L07` Demo: facilitating Larkspur's discovery workshop (15 min)
- `ARC-003-L08` Demo: resolving "real-time stock" vs "keep the ERP as master" (14 min)

#### ARC-004 · Architecture frameworks
*67 min video · 2.5 h practice* · Prerequisites: SRB-012, ARC-001

**Topics:** TOGAF concepts, architecture viewpoints, governance

**Lessons:**
- `ARC-004-L01` Why architecture frameworks exist (8 min)
- `ARC-004-L02` TOGAF concepts and the ADM (14 min)
- `ARC-004-L03` Architecture domains and building blocks (10 min)
- `ARC-004-L04` Viewpoints, views, and concerns (12 min)
- `ARC-004-L05` Governance and tailoring (10 min)
- `ARC-004-L06` Demo: tailoring a lightweight framework for the Larkspur program (13 min)

#### ARC-005 · Architecture modeling
*66 min video · 3.5 h practice* · Prerequisites: MID-063, ARC-002

**Topics:** C4, UML, ArchiMate introduction, deployment and integration diagrams

**Lessons:**
- `ARC-005-L01` Models answer questions (8 min)
- `ARC-005-L02` C4 for solution architects (10 min)
- `ARC-005-L03` The useful parts of UML (10 min)
- `ARC-005-L04` ArchiMate introduction (12 min)
- `ARC-005-L05` Integration and deployment diagrams (12 min)
- `ARC-005-L06` Demo: one Larkspur model, three audiences (14 min)

#### ARC-006 · Solution architecture lifecycle
*64 min video · 3 h practice* · Prerequisites: ARC-003, ARC-004

**Topics:** Discovery, options, design, review, delivery, transition

**Lessons:**
- `ARC-006-L01` The lifecycle at a glance (8 min)
- `ARC-006-L02` Discovery and options (10 min)
- `ARC-006-L03` Design and review (10 min)
- `ARC-006-L04` Supporting delivery (12 min)
- `ARC-006-L05` Transition and handover (10 min)
- `ARC-006-L06` Demo: planning Larkspur's architecture lifecycle and checkpoints (14 min)

#### ARC-007 · Architecture principles
*56 min video · 2.5 h practice* · Prerequisites: SRA-012, ARC-004

**Topics:** Standardization, interoperability, security, evolvability

**Lessons:**
- `ARC-007-L01` What makes a principle useful (10 min)
- `ARC-007-L02` Statement, rationale, implications (10 min)
- `ARC-007-L03` Common principle sets (12 min)
- `ARC-007-L04` When principles conflict (10 min)
- `ARC-007-L05` Demo: drafting Larkspur's principles with the CIO (14 min)

#### ARC-008 · Technology assessment
*67 min video · 3.5 h practice* · Prerequisites: SRB-013, SRA-008

**Topics:** Build vs buy vs SaaS, vendor evaluation, proof of concept

**Lessons:**
- `ARC-008-L01` Build, buy, or SaaS (12 min)
- `ARC-008-L02` Differentiating vs commodity capabilities (10 min)
- `ARC-008-L03` Evaluating vendors' architecture fit (12 min)
- `ARC-008-L04` Proofs of concept that reduce risk (10 min)
- `ARC-008-L05` Recommendation and sensitivity (8 min)
- `ARC-008-L06` Demo: commerce platform — build, packaged suite, or SaaS? (15 min)

#### ARC-009 · Enterprise integration
*87 min video · 4 h practice* · Prerequisites: SRB-002, SRB-007

**Topics:** APIs, events, ESB, iPaaS, batch, file exchange

**Lessons:**
- `ARC-009-L01` Integration is where projects fail (8 min)
- `ARC-009-L02` APIs and events (10 min)
- `ARC-009-L03` ESB and iPaaS (12 min)
- `ARC-009-L04` Batch and file exchange still matter (10 min)
- `ARC-009-L05` Canonical models: when and when not (10 min)
- `ARC-009-L06` Operating integrations (8 min)
- `ARC-009-L07` Demo: Larkspur's integration landscape, interface by interface (15 min)
- `ARC-009-L08` Demo: the nightly ERP file that can't go away yet (14 min)

#### ARC-010 · Legacy modernization
*83 min video · 4 h practice* · Prerequisites: SRB-008, ARC-009

**Topics:** Rehost, replatform, refactor, replace, retire

**Lessons:**
- `ARC-010-L01` Why modernize, and why not (8 min)
- `ARC-010-L02` Rehost, replatform, refactor, replace, retire (14 min)
- `ARC-010-L03` Assessing an application portfolio (12 min)
- `ARC-010-L04` Sequencing and coexistence (10 min)
- `ARC-010-L05` The modernization business case (10 min)
- `ARC-010-L06` Demo: assessing Larkspur's application portfolio (15 min)
- `ARC-010-L07` Demo: replace the web shop, retain the ERP — the case (14 min)

### ARC-P2 — Cloud and Infrastructure Architecture

#### ARC-011 · Cloud service models
*58 min video · 2.5 h practice* · Prerequisites: MID-056

**Topics:** IaaS, PaaS, SaaS, managed services

**Lessons:**
- `ARC-011-L01` IaaS, PaaS, SaaS, managed services (12 min)
- `ARC-011-L02` Shared responsibility by model (12 min)
- `ARC-011-L03` Control vs operational burden (10 min)
- `ARC-011-L04` Lock-in, honestly assessed (10 min)
- `ARC-011-L05` Demo: choosing service models for each Larkspur component (14 min)

#### ARC-012 · Cloud architecture
*75 min video · 4 h · `version:` provider-specific practice* · Prerequisites: MID-056, ARC-011

**Topics:** AWS or Azure reference architectures, regions, availability zones

**Lessons:**
- `ARC-012-L01` Regions, zones, and edge locations (10 min)
- `ARC-012-L02` Reading reference architectures critically (12 min)
- `ARC-012-L03` Accounts, subscriptions, and environments (12 min)
- `ARC-012-L04` A reference web/mobile commerce architecture (12 min)
- `ARC-012-L05` Demo: Larkspur's target cloud architecture (15 min)
- `ARC-012-L06` Demo: adapting a reference architecture to Larkspur's constraints (14 min)

#### ARC-013 · Networking
*95 min video · 4 h · `version:` provider-specific practice* · Prerequisites: MID-056, ARC-012

**Topics:** CIDR, routing, VPC/VNet, subnets, NAT, VPN, private endpoints

**Lessons:**
- `ARC-013-L01` CIDR and address planning (12 min)
- `ARC-013-L02` VPC/VNet layout and subnets (12 min)
- `ARC-013-L03` Routing and NAT (10 min)
- `ARC-013-L04` Hybrid connectivity (12 min)
- `ARC-013-L05` Private endpoints and private data paths (10 min)
- `ARC-013-L06` Hub-and-spoke topologies (10 min)
- `ARC-013-L07` Demo: planning address space for Larkspur, stores, and the data center (15 min)
- `ARC-013-L08` Demo: connecting the cloud platform to the on-premises ERP (14 min)

#### ARC-014 · Compute choices
*66 min video · 3 h practice* · Prerequisites: MID-057, ARC-012

**Topics:** VMs, containers, Kubernetes, serverless

**Lessons:**
- `ARC-014-L01` The compute spectrum (10 min)
- `ARC-014-L02` VMs and managed container platforms (10 min)
- `ARC-014-L03` Kubernetes: when it is worth it (12 min)
- `ARC-014-L04` Serverless functions (12 min)
- `ARC-014-L05` Matching compute to workload shape (8 min)
- `ARC-014-L06` Demo: compute choices for Larkspur's storefront, order processing, and nightly batch (14 min)

#### ARC-015 · Storage architecture
*58 min video · 2.5 h practice* · Prerequisites: ARC-012

**Topics:** Object, block, file, backup, lifecycle policies

**Lessons:**
- `ARC-015-L01` Object, block, and file storage (12 min)
- `ARC-015-L02` Backups, retention, and immutability (12 min)
- `ARC-015-L03` Lifecycle policies and tiers (10 min)
- `ARC-015-L04` Securing stored data (10 min)
- `ARC-015-L05` Demo: storage design for product media, documents, and backups (14 min)

#### ARC-016 · Database architecture
*68 min video · 3.5 h practice* · Prerequisites: SRC-007, ARC-012

**Topics:** Managed SQL, NoSQL, caching, replication, DR

**Lessons:**
- `ARC-016-L01` Managed databases: what you still own (10 min)
- `ARC-016-L02` Selecting stores by workload (12 min)
- `ARC-016-L03` Replication, read scaling, failover (12 min)
- `ARC-016-L04` Backup, PITR, and DR for data (10 min)
- `ARC-016-L05` Migrating databases to the cloud (10 min)
- `ARC-016-L06` Demo: Larkspur's data stores and their failover design (14 min)

#### ARC-017 · Identity architecture
*87 min video · 4 h practice* · Prerequisites: MID-051, ARC-012

**Topics:** IAM, federation, SSO, OAuth 2.0, OIDC, SAML concepts

**Lessons:**
- `ARC-017-L01` Identity as the new perimeter (8 min)
- `ARC-017-L02` Workforce identity and SSO (12 min)
- `ARC-017-L03` Federation: SAML, OAuth 2.0, OIDC (14 min)
- `ARC-017-L04` Customer identity (12 min)
- `ARC-017-L05` Cloud IAM for people and workloads (12 min)
- `ARC-017-L06` Demo: Larkspur's identity architecture end to end (15 min)
- `ARC-017-L07` Demo: SSO for store staff into the new back office (14 min)

#### ARC-018 · Network security
*64 min video · 3 h practice* · Prerequisites: SRB-016, ARC-013

**Topics:** Firewalls, WAF, segmentation, private connectivity

**Lessons:**
- `ARC-018-L01` Defense in depth for networks (10 min)
- `ARC-018-L02` Security groups, firewalls, and WAF (12 min)
- `ARC-018-L03` Segmentation (10 min)
- `ARC-018-L04` DDoS and edge protection (10 min)
- `ARC-018-L05` Private connectivity to SaaS and partners (8 min)
- `ARC-018-L06` Demo: protecting Larkspur's storefront and payment paths (14 min)

#### ARC-019 · High availability and DR
*83 min video · 4 h practice* · Prerequisites: SRC-013, SRB-004, ARC-012

**Topics:** Multi-AZ, multi-region, RPO/RTO, disaster recovery design

**Lessons:**
- `ARC-019-L01` Availability and recovery as business decisions (10 min)
- `ARC-019-L02` Multi-AZ design (10 min)
- `ARC-019-L03` DR patterns from backup-restore to active-active (14 min)
- `ARC-019-L04` Dependencies you don't own (10 min)
- `ARC-019-L05` Testing DR (10 min)
- `ARC-019-L06` Demo: costing three DR patterns for Larkspur's checkout (15 min)
- `ARC-019-L07` Demo: what happens to stores when the cloud region is down (14 min)

#### ARC-020 · Infrastructure governance
*66 min video · 3 h · `version:` provider-specific practice* · Prerequisites: MID-058, ARC-012

**Topics:** Landing zones, policies, tagging, infrastructure as code

**Lessons:**
- `ARC-020-L01` Why landing zones exist (10 min)
- `ARC-020-L02` Account and subscription hierarchies (12 min)
- `ARC-020-L03` Policy guardrails (12 min)
- `ARC-020-L04` Tagging standards (8 min)
- `ARC-020-L05` Infrastructure as code as governance (10 min)
- `ARC-020-L06` Demo: Larkspur's landing zone design (14 min)

#### ARC-021 · Cost architecture
*79 min video · 3.5 h practice* · Prerequisites: SRB-015, ARC-012

**Topics:** Sizing, pricing assumptions, budgets, cost controls

**Lessons:**
- `ARC-021-L01` Cost as a design input (8 min)
- `ARC-021-L02` Sizing and pricing assumptions (12 min)
- `ARC-021-L03` Building a cost model (12 min)
- `ARC-021-L04` Unit cost and sensitivity (10 min)
- `ARC-021-L05` Budgets and controls (8 min)
- `ARC-021-L06` Demo: Larkspur's cloud cost model, line by line (15 min)
- `ARC-021-L07` Demo: what the cost does at peak season and at 3× growth (14 min)

#### ARC-022 · Cloud architecture frameworks
*57 min video · 3 h practice* · Prerequisites: ARC-019, ARC-021

**Topics:** AWS or Azure Well-Architected principles

**Lessons:**
- `ARC-022-L01` Well-architected frameworks and their pillars (12 min)
- `ARC-022-L02` Running a review (12 min)
- `ARC-022-L03` Prioritizing findings (10 min)
- `ARC-022-L04` From findings to remediation (8 min)
- `ARC-022-L05` Demo: a well-architected review of Larkspur's design (15 min)

### ARC-P3 — Enterprise Data, Integration, and Security

#### ARC-023 · Data architecture
*68 min video · 3 h practice* · Prerequisites: MID-044, SRA-004

**Topics:** Operational vs analytical workloads, data lifecycle

**Lessons:**
- `ARC-023-L01` Data architecture for solution architects (10 min)
- `ARC-023-L02` Operational vs analytical workloads (12 min)
- `ARC-023-L03` Warehouses, lakes, and lakehouses (12 min)
- `ARC-023-L04` The data lifecycle (10 min)
- `ARC-023-L05` Conceptual models and data-flow views (10 min)
- `ARC-023-L06` Demo: Larkspur's data landscape from sales floor to board report (14 min)

#### ARC-024 · Integration patterns
*70 min video · 4 h practice* · Prerequisites: SRB-007, ARC-009

**Topics:** Synchronous APIs, async events, batch ETL/ELT, CDC

**Lessons:**
- `ARC-024-L01` Integration styles compared (12 min)
- `ARC-024-L02` Coupling, latency, and failure (10 min)
- `ARC-024-L03` Batch, ETL, and ELT (10 min)
- `ARC-024-L04` Enterprise integration patterns (10 min)
- `ARC-024-L05` Demo: choosing a style for each Larkspur interface (14 min)
- `ARC-024-L06` Demo: replacing a nightly stock file with near-real-time CDC (14 min)

#### ARC-045 · AI solution architecture
*70 min video · 4 h practice* · Prerequisites: SRA-021, ARC-024 · added in v2.0

**Topics:** Reference architectures for assistants, RAG, and agents over enterprise data, deployment options, cost and latency

**Lessons:**
- `ARC-045-L01` AI reference architectures (12 min)
- `ARC-045-L02` Grounding AI in enterprise data (12 min)
- `ARC-045-L03` Agents and tools over enterprise systems (10 min)
- `ARC-045-L04` Deployment options and their trade-offs (10 min)
- `ARC-045-L05` Demo: architecture of the Larkspur customer-service assistant (14 min)
- `ARC-045-L06` Demo: costing the assistant per conversation (12 min)

#### ARC-025 · API management
*58 min video · 3 h practice* · Prerequisites: MID-035, SRC-006

**Topics:** Gateways, developer portals, governance, quotas

**Lessons:**
- `ARC-025-L01` APIs as products (10 min)
- `ARC-025-L02` What API management platforms provide (12 min)
- `ARC-025-L03` API governance and lifecycle (12 min)
- `ARC-025-L04` Quotas, keys, and consumer tiers (10 min)
- `ARC-025-L05` Demo: designing Larkspur's partner API program (14 min)

#### ARC-026 · Event architecture
*66 min video · 3 h practice* · Prerequisites: SRB-002, ARC-024

**Topics:** Event ownership, event catalogs, schemas, compatibility

**Lessons:**
- `ARC-026-L01` Events at enterprise scale (10 min)
- `ARC-026-L02` Event ownership (10 min)
- `ARC-026-L03` Event catalogs and schemas (12 min)
- `ARC-026-L04` Compatibility and evolution (10 min)
- `ARC-026-L05` When an event backbone pays off (10 min)
- `ARC-026-L06` Demo: Larkspur's order and stock events, from catalog to consumers (14 min)

#### ARC-027 · Identity and access
*58 min video · 3 h practice* · Prerequisites: ARC-017

**Topics:** RBAC, ABAC, identity federation, privileged access

**Lessons:**
- `ARC-027-L01` Authorization models: RBAC and ABAC (12 min)
- `ARC-027-L02` Identity federation (12 min)
- `ARC-027-L03` Privileged access (10 min)
- `ARC-027-L04` Joiners, movers, leavers, and access reviews (10 min)
- `ARC-027-L05` Demo: store managers, call-center agents, and partners in one access model (14 min)

#### ARC-028 · Security architecture
*71 min video · 4 h practice* · Prerequisites: SRA-009, ARC-018

**Topics:** Zero trust, threat modeling, defense in depth

**Lessons:**
- `ARC-028-L01` Security architecture for whole solutions (10 min)
- `ARC-028-L02` Zero trust and defense in depth (12 min)
- `ARC-028-L03` Solution-level threat modeling (12 min)
- `ARC-028-L04` Controls and security requirements (10 min)
- `ARC-028-L05` Demo: threat-modeling Larkspur's checkout and payment flow (14 min)
- `ARC-028-L06` Demo: walking a security team through the security architecture view (13 min)

#### ARC-029 · Privacy and compliance
*74 min video · 3.5 h practice* · Prerequisites: SRA-009, ARC-023

**Topics:** Data classification, retention, residency, audit requirements

**Lessons:**
- `ARC-029-L01` Data classification (10 min)
- `ARC-029-L02` Retention and deletion (10 min)
- `ARC-029-L03` Data-subject rights across many systems (10 min)
- `ARC-029-L04` Residency and cross-border transfers (8 min)
- `ARC-029-L05` Payment compliance scope (10 min)
- `ARC-029-L06` Demo: shrinking Larkspur's PCI DSS scope with a hosted payment page (13 min)
- `ARC-029-L07` Demo: tracing one customer's data for an erasure request (13 min)

#### ARC-046 · AI security
*58 min video · 3.5 h practice* · Prerequisites: ARC-029, ARC-045 · added in v2.0

**Topics:** Data classification for prompts, residency, vendor terms, guardrails, auditability, responsible AI controls

**Lessons:**
- `ARC-046-L01` Data classification for AI (10 min)
- `ARC-046-L02` Provider terms: residency, retention, training use (12 min)
- `ARC-046-L03` Architectural guardrails (12 min)
- `ARC-046-L04` Auditability and data-subject rights (10 min)
- `ARC-046-L05` Demo: threat-modeling the Larkspur assistant (14 min)

#### ARC-030 · Data governance
*58 min video · 2.5 h practice* · Prerequisites: SRA-004, ARC-029

**Topics:** Ownership, quality, lineage, access policies

**Lessons:**
- `ARC-030-L01` Governance that enables use (10 min)
- `ARC-030-L02` Owners and stewards (10 min)
- `ARC-030-L03` Data quality rules (12 min)
- `ARC-030-L04` Lineage and access policies (12 min)
- `ARC-030-L05` Demo: tracing a wrong revenue number back to its source (14 min)

#### ARC-031 · Resilience architecture
*58 min video · 3 h practice* · Prerequisites: SRA-006, ARC-019

**Topics:** Failure scenarios, fault isolation, continuity plans

**Lessons:**
- `ARC-031-L01` Resilience beyond infrastructure (10 min)
- `ARC-031-L02` Failure scenarios for enterprise solutions (12 min)
- `ARC-031-L03` Fault isolation and degradation (12 min)
- `ARC-031-L04` Business continuity planning (10 min)
- `ARC-031-L05` Demo: keeping 120 stores selling when the central platform is down (14 min)

#### ARC-032 · Integration with enterprise systems
*72 min video · 4 h practice* · Prerequisites: ARC-024, ARC-027

**Topics:** ERP, CRM, payment gateways, identity providers

**Lessons:**
- `ARC-032-L01` Working with systems of record (10 min)
- `ARC-032-L02` ERP integration (12 min)
- `ARC-032-L03` CRM integration (10 min)
- `ARC-032-L04` Payment gateways and identity providers (12 min)
- `ARC-032-L05` Demo: an anti-corruption layer between the platform and the ERP (14 min)
- `ARC-032-L06` Demo: reconciling payments between the gateway, platform, and ERP (14 min)

### ARC-P4 — Solution Design, Governance, and Delivery

#### ARC-033 · Solution options
*71 min video · 4 h practice* · Prerequisites: SRC-003, ARC-006

**Topics:** Alternative designs, evaluation criteria, decision matrices

**Lessons:**
- `ARC-033-L01` Why one option is no option (10 min)
- `ARC-033-L02` Generating real alternatives (10 min)
- `ARC-033-L03` Criteria and weights with stakeholders (12 min)
- `ARC-033-L04` Decision matrices and sensitivity (12 min)
- `ARC-033-L05` Demo: four options for Larkspur's commerce platform (14 min)
- `ARC-033-L06` Demo: when changing one weight flips the recommendation (13 min)

#### ARC-034 · Architecture deliverables
*71 min video · 4 h practice* · Prerequisites: ARC-005, ARC-033

**Topics:** HLD, LLD, ADRs, interface contracts, deployment diagrams

**Lessons:**
- `ARC-034-L01` Deliverables and their readers (10 min)
- `ARC-034-L02` The high-level design (12 min)
- `ARC-034-L03` The low-level design (12 min)
- `ARC-034-L04` Interface contracts and deployment diagrams (10 min)
- `ARC-034-L05` Demo: writing Larkspur's HLD section by section (14 min)
- `ARC-034-L06` Demo: turning an HLD component into an LLD a team can build (13 min)

#### ARC-035 · Architecture review boards
*56 min video · 2.5 h practice* · Prerequisites: ARC-007, ARC-034

**Topics:** Governance, compliance checks, design exceptions

**Lessons:**
- `ARC-035-L01` What review boards are for (10 min)
- `ARC-035-L02` Preparing a submission (12 min)
- `ARC-035-L03` Compliance checks (10 min)
- `ARC-035-L04` Exceptions and conditions (10 min)
- `ARC-035-L05` Demo: a Larkspur ARB session with conditions (14 min)

#### ARC-036 · Solution roadmaps
*56 min video · 3 h practice* · Prerequisites: SRA-002, ARC-033

**Topics:** Phased implementation, dependencies, milestones

**Lessons:**
- `ARC-036-L01` Roadmaps that deliver value early (10 min)
- `ARC-036-L02` Phasing a solution (12 min)
- `ARC-036-L03` Dependency mapping (10 min)
- `ARC-036-L04` Milestones and exit criteria (10 min)
- `ARC-036-L05` Demo: Larkspur's 18-month roadmap, phase by phase (14 min)

#### ARC-037 · Migration strategy
*71 min video · 4 h practice* · Prerequisites: SRB-017, ARC-010

**Topics:** Cutover, coexistence, rollback, data migration

**Lessons:**
- `ARC-037-L01` Cutover approaches (12 min)
- `ARC-037-L02` Coexistence of old and new (10 min)
- `ARC-037-L03` Data migration (12 min)
- `ARC-037-L04` Rollback and go/no-go (10 min)
- `ARC-037-L05` Demo: migrating Larkspur's customers and orders from the old web shop (14 min)
- `ARC-037-L06` Demo: a pilot-store rollout and its rollback plan (13 min)

#### ARC-038 · Operational architecture
*58 min video · 3 h practice* · Prerequisites: SRC-011, ARC-036

**Topics:** Monitoring, support, incident processes, service ownership

**Lessons:**
- `ARC-038-L01` Designing for operations (10 min)
- `ARC-038-L02` Monitoring a mixed estate (12 min)
- `ARC-038-L03` Support models and service ownership (12 min)
- `ARC-038-L04` Incident and change processes with vendors (10 min)
- `ARC-038-L05` Demo: Larkspur's operating model on a single page (14 min)

#### ARC-039 · Financial analysis
*69 min video · 4 h practice* · Prerequisites: SRA-008, ARC-021

**Topics:** TCO, ROI, cost-benefit, licensing, operational costs

**Lessons:**
- `ARC-039-L01` Finance for architects (10 min)
- `ARC-039-L02` Total cost of ownership (12 min)
- `ARC-039-L03` ROI, payback, and benefits (10 min)
- `ARC-039-L04` Licensing and operating costs (10 min)
- `ARC-039-L05` Demo: a five-year TCO for Larkspur's options (14 min)
- `ARC-039-L06` Demo: a finance review of the business case (13 min)

#### ARC-040 · Vendor and procurement
*58 min video · 3 h practice* · Prerequisites: ARC-008, ARC-039

**Topics:** RFP/RFI, technical evaluation, SLAs, contracts

**Lessons:**
- `ARC-040-L01` The procurement process (10 min)
- `ARC-040-L02` RFIs and RFPs (12 min)
- `ARC-040-L03` Technical evaluation (12 min)
- `ARC-040-L04` SLAs and contracts from an architect's view (10 min)
- `ARC-040-L05` Demo: scoring two vendor RFP responses (14 min)

#### ARC-047 · AI vendor and model evaluation
*70 min video · 3.5 h practice* · Prerequisites: ARC-040, ARC-045 · added in v2.0

**Topics:** AI vendor criteria, public benchmarks vs own evaluations, total cost, exit plans

**Lessons:**
- `ARC-047-L01` Evaluating AI vendors and models (12 min)
- `ARC-047-L02` Benchmarks vs your own evaluations (12 min)
- `ARC-047-L03` AI proofs of concept (10 min)
- `ARC-047-L04` Multi-year AI cost and exit planning (10 min)
- `ARC-047-L05` Demo: scoring three AI vendors for Larkspur (14 min)
- `ARC-047-L06` Demo: building a 50-question evaluation set from support tickets (12 min)

#### ARC-041 · Stakeholder management
*56 min video · 3 h practice* · Prerequisites: SRA-015, ARC-003

**Topics:** Business, engineering, security, operations, vendors

**Lessons:**
- `ARC-041-L01` Stakeholder mapping (10 min)
- `ARC-041-L02` Engagement plans (10 min)
- `ARC-041-L03` Resolving conflicting requirements (12 min)
- `ARC-041-L04` Keeping alignment over time (10 min)
- `ARC-041-L05` Demo: mediating between store operations and e-commerce (14 min)

#### ARC-042 · Architecture assurance
*58 min video · 3 h practice* · Prerequisites: SRC-011, ARC-035

**Topics:** Design reviews, testing evidence, operational acceptance

**Lessons:**
- `ARC-042-L01` Assurance during delivery (10 min)
- `ARC-042-L02` Architecture drift (10 min)
- `ARC-042-L03` Non-functional testing evidence (12 min)
- `ARC-042-L04` Operational acceptance and go-live readiness (12 min)
- `ARC-042-L05` Demo: finding drift in a delivery team's design (14 min)

#### ARC-043 · Solution documentation
*54 min video · 3 h practice* · Prerequisites: ARC-034

**Topics:** Architecture packs, decision logs, assumptions, risks

**Lessons:**
- `ARC-043-L01` The architecture pack (10 min)
- `ARC-043-L02` Decision and assumption logs (10 min)
- `ARC-043-L03` Risk registers (10 min)
- `ARC-043-L04` Keeping documentation alive (10 min)
- `ARC-043-L05` Demo: assembling Larkspur's architecture pack (14 min)

#### ARC-044 · Architecture communication
*70 min video · 4 h practice* · Prerequisites: SRA-019, ARC-043

**Topics:** Presenting solutions to executives and engineering teams

**Lessons:**
- `ARC-044-L01` One solution, many audiences (10 min)
- `ARC-044-L02` Presenting to executives (12 min)
- `ARC-044-L03` Presenting to engineering teams (10 min)
- `ARC-044-L04` Defending a design (10 min)
- `ARC-044-L05` Demo: Larkspur's ten-minute executive presentation (14 min)
- `ARC-044-L06` Demo: a hostile technical design defense, handled (14 min)

---
