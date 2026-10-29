# BEG-007 · How code runs — Exercises and lab

## Lab
### BEG-007-LAB1 · Hello from the terminal
**Outcomes:** 1–4 · **Time:** ~1.5 h
1. Type the provided Hello program, compile it with `javac`, and run it with `java`.
2. Look at the generated `.class` file.
3. Introduce a syntax error and record the compile-time message.
4. Introduce a division-by-zero error and record the runtime message.
5. Run the same program in IntelliJ.

**Acceptance:** both messages captured and each classified correctly.

## Exercises
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-007-EX01 | 1 | Put in order: machine code, source code, bytecode. |
| BEG-007-EX02 | 1 | Why can the same `.class` file run on Windows and Linux? |
| BEG-007-EX03 | 2 | Draw JDK, JRE, and JVM as nested boxes. |
| BEG-007-EX04 | 2 | Which one do you install to write Java, and why? |
| BEG-007-EX05 | 3 | Compile and run a program from the terminal; list the two commands. |
| BEG-007-EX06 | 3 | `java Hello.class` fails. Why, and what is the fix? |
| BEG-007-EX07 | 4 | Classify: a missing semicolon; dividing by zero; a typo in a variable name. |

## Solutions
- **EX01** Source code → bytecode → machine code.
- **EX02** Each OS has a JVM that runs the same bytecode.
- **EX03** JVM inside JRE inside JDK.
- **EX04** The JDK, because it includes the compiler.
- **EX05** `javac Hello.java` then `java Hello`.
- **EX06** `java` expects the class name, not the file name. Use `java Hello`.
- **EX07** Compile-time; runtime; compile-time.
