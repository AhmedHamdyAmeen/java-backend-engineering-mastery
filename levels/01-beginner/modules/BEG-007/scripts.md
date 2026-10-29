# BEG-007 · How code runs — Lecture scripts

**Video:** 48 min · **Analogy used throughout:** translating a book: a translator works once up front (compile), then anyone can read it.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-007-L01 · From text to execution: compilers and interpreters (10 min)
**Goal:** explain how text code becomes something the CPU runs.

**Key points**
- Source code is text people write.
- The CPU only understands machine code (binary instructions).
- A compiler translates the whole program before it runs.
- An interpreter translates and runs line by line while it runs.
- Compile-time errors are found before running; runtime errors happen while running.

**Show:** source text → translator → machine code.

**Check:** Which finds mistakes before the program runs: compiler or interpreter? *(Compiler.)*

---

## BEG-007-L02 · Java's approach: bytecode and the JVM (10 min)
**Goal:** explain "write once, run anywhere".

**Key points**
- The Java compiler (`javac`) turns `.java` source into bytecode in a `.class` file.
- Bytecode is not tied to one CPU or OS.
- The JVM (Java Virtual Machine) reads bytecode and runs it on the real machine.
- Each OS has its own JVM, so the same `.class` file runs on Windows, macOS, and Linux.

**Show:** `Hello.java` → `javac` → `Hello.class` → JVM → output.

**Check:** What is inside a `.class` file? *(Bytecode.)*

---

## BEG-007-L03 · JDK vs JRE vs JVM (8 min)
**Goal:** keep the three names straight.

**Key points**
- JVM runs bytecode.
- JRE = JVM + the standard libraries; it can run Java programs.
- JDK = JRE + tools such as `javac`; it can also build them.
- As a developer you install the JDK.

**Show:** nested boxes: JDK contains JRE contains JVM.

**Check:** Which do you need to compile Java? *(The JDK.)*

---

## BEG-007-L04 · Compile and run from the terminal (12 min)
**Goal:** compile and run a program by hand.

**Key points**
- Save a file as `Hello.java`; the file name must match the public class name.
- Compile: `javac Hello.java`. This creates `Hello.class`.
- Run: `java Hello` (no `.class`).
- A syntax error stops compilation and shows a message with the line number.
- A program that compiles can still fail while running.

**Show:** the three commands in a terminal, with the folder listing before and after.

**Check:** Which is right: `java Hello` or `java Hello.class`? *(`java Hello`.)*

---

## BEG-007-L05 · Demo: compile, run, break, and fix Hello World in the terminal (8 min)
**Goal:** see both kinds of error. Prepares `BEG-007-LAB1`.

**Steps**
1. Write, compile, and run Hello World.
2. Open the `.class` file in a text editor to show it is not readable text.
3. Remove a semicolon; compile; read the compile-time error.
4. Add `int x = 5 / 0;`; compile; run; read the runtime error.
5. **Planned mistake:** rename the file so it no longer matches the class name; fix the name and recompile.
