# BEG-008 · First Java program — Lecture scripts

**Video:** 48 min · **Analogy used throughout:** a recipe card (title, steps, notes in the margin).
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-008-L01 · Anatomy of Hello World (10 min)
**Goal:** name every part of a minimal Java program.

**Key points**
- Every Java program lives inside a class.
- `main` is where the program starts. Its exact line is `public static void main(String[] args)`.
- Curly braces `{ }` mark where a class or method begins and ends.
- Statements inside `main` run top to bottom.
- Java is case sensitive: `Main` and `main` are different words.
- The file name must match the public class name: `Hello` lives in `Hello.java`.

**Show**
```java
public class Hello {
    public static void main(String[] args) {
        System.out.println("Hello, Java!");
    }
}
```
Colour each part: class line, `main` line, braces, the statement.

**Check:** Where does the program start running? *(In `main`.)*

---

## BEG-008-L02 · Statements, semicolons, and blocks (8 min)
**Goal:** write statements correctly.

**Key points**
- A statement is one instruction. It ends with a semicolon `;`.
- A block is a group of statements inside `{ }`.
- Every `{` needs a matching `}`.
- Indent inside a block. The compiler does not care, but people do.
- Spaces and blank lines are free; use them to make code readable.

**Show:** one program with correct indentation, then the same program on one line to show it still compiles but is hard to read.

**Check:** What ends a statement? *(A semicolon.)*

---

## BEG-008-L03 · Printing output (8 min)
**Goal:** print text and values.

**Key points**
- `System.out.println(x)` prints `x` and moves to a new line.
- `System.out.print(x)` prints `x` and stays on the same line.
- Text goes in double quotes: `"Hello"`. Numbers do not need quotes.
- Join text and values with `+`: `"Age: " + 30`.
- `\n` is a new line and `\t` is a tab inside text.

**Show**
```java
System.out.print("Name: ");
System.out.println("Ana");
System.out.println("Age: " + 30);
```

**Check:** What is the difference between `print` and `println`? *(`println` adds a new line afterwards.)*

---

## BEG-008-L04 · Comments (6 min)
**Goal:** write comments that help.

**Key points**
- `// ...` is a single-line comment.
- `/* ... */` can span many lines.
- `/** ... */` is a Javadoc comment, used to describe classes and methods.
- Comments are ignored by the compiler.
- Explain *why*, not *what*. `// retry because the network is flaky` helps; `// add 1` does not.

**Show:** the three comment styles on a small program, plus one useless and one useful comment.

**Check:** Which comment style is used for Javadoc? *(`/** ... */`.)*

---

## BEG-008-L05 · Reading compiler errors (8 min)
**Goal:** fix errors from the message alone.

**Key points**
- The message shows the file, the line number, and a description.
- Read the first error first; later ones are often caused by it.
- The line shown can be one line after the real mistake (a missing semicolon).
- Five common errors: missing `;`, misspelled name (`system`), unmatched brace, wrong `main` signature, unclosed string quote.
- Fix one, recompile, repeat.

**Show:** a table of message → likely cause, such as `';' expected`, `cannot find symbol`, `class, interface, enum, or record expected`.

**Check:** `cannot find symbol` points at `system.out`. What is wrong? *(Case: it should be `System`.)*

---

## BEG-008-L06 · Demo: fixing five broken programs from compiler messages (8 min)
**Goal:** practise the fix loop. Prepares `BEG-008-LAB1`.

**Steps**
1. Compile program 1; read the error; add the missing semicolon.
2. Program 2: fix `system.out` to `System.out`.
3. Program 3: add the missing closing brace.
4. Program 4: correct `main`'s signature.
5. Program 5: close the open string quote.
6. **Planned mistake:** fix only the first error and think everything is done; recompile and find the next one.
