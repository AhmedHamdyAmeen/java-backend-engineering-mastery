# BEG-005 · Development environment — Exercises and lab

## Lab
### BEG-005-LAB1 · Working toolbox
**Outcomes:** 1, 2, 3, 4 · **Time:** ~2 h
1. Install the JDK and IntelliJ IDEA.
2. Print `java -version` and `javac -version` in a terminal.
3. Break `PATH` in a new terminal session and observe the error.
4. Restore `PATH` and show it works.

**Acceptance:** screenshots of both states and the fix.

## Exercises
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-005-EX01 | 4 | Turn on file extensions and show `.java` and `.txt` files side by side. |
| BEG-005-EX02 | 4 | Why does `Hello.java.txt` not compile as Java? |
| BEG-005-EX03 | 1 | Print the Java and compiler versions. |
| BEG-005-EX04 | 3 | Print your `PATH` and find the JDK folder in it. |
| BEG-005-EX05 | 3 | You get "command not found" for `java`. List two possible causes. |
| BEG-005-EX06 | 2 | Create a project in IntelliJ, run it, and close it. |

## Solutions
- **EX01** Windows: File Explorer → View → File name extensions. macOS: Finder preferences.
- **EX02** Its real extension is `.txt`, so it is treated as plain text.
- **EX03** `java -version` and `javac -version`; both print versions.
- **EX04** Windows: `echo %PATH%`; Bash: `echo $PATH`; PowerShell: `$env:PATH`.
- **EX05** JDK not installed, or its `bin` folder not on `PATH`; or the terminal was opened before the change.
- **EX06** New Project → JDK → add a class with `main` → Run → File → Close Project.
