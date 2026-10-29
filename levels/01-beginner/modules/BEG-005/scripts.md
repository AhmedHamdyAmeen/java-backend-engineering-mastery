# BEG-005 · Development environment — Lecture scripts

**Video:** 58 min · **Analogy used throughout:** setting up a workshop (tools on the bench, and a list of where tools are kept).
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-005-L01 · Files, folders, and extensions on Windows, macOS, and Linux (8 min)
**Goal:** see file extensions and understand why they matter.

**Key points**
- Files live in folders; the folder path says where.
- The extension (`.java`, `.txt`) is the ending of a file name and tells the system what the file is.
- Windows hides extensions by default; turn them on.
- `Hello.java` and `Hello.java.txt` are different files. The second one is just text.
- Dot-files like `.gitignore` are hidden on macOS and Linux by default.

**Show:** the "File name extensions" checkbox in Windows File Explorer, and `Cmd+Shift+.` on macOS.

**Check:** Why can `Hello.java.txt` not be compiled as Java? *(Its real extension is `.txt`.)*

---

## BEG-005-L02 · Installing the JDK (all three operating systems) (12 min)
**Goal:** install the JDK and check it works.

**Key points**
- JDK = the Java Development Kit: what you need to write and run Java. (JRE alone is not enough.)
- Install the current LTS version from the vendor's download page; verify the version before recording.
- Windows: installer. macOS: installer or package manager. Linux: package manager.
- Check with `java -version` and `javac -version` in a new terminal.
- Both commands must print a version number.

**Show:** the install on each OS, ending with both version commands.

**Check:** Which command shows that the compiler is installed? *(`javac -version`.)*

---

## BEG-005-L03 · Environment variables and PATH (10 min)
**Goal:** explain PATH and fix "command not found".

**Key points**
- An environment variable is a named setting the system gives to programs.
- `PATH` is a list of folders the terminal searches when you type a command.
- If the folder with `java` is not on `PATH`, the terminal says "command not found".
- Changes to `PATH` apply only to terminals opened afterwards.
- Many tools also read `JAVA_HOME`, the JDK's location.

**Show:** print `PATH`; remove the JDK folder; see the error; put it back.

**Check:** You fixed `PATH` but the old terminal still fails. Why? *(It was opened before the change.)*

---

## BEG-005-L04 · Installing and tour of IntelliJ IDEA (12 min)
**Goal:** create and run a project in IntelliJ.

**Key points**
- An IDE is an editor with helpers: it highlights errors, completes code, and runs programs.
- Install IntelliJ IDEA Community Edition.
- New Project → choose the JDK → name it.
- Main parts: project tree, editor, run button, console.
- Close a project from File → Close Project.

**Show:** create a project, add a class, press Run, see output in the console.

**Check:** Where do you see a program's output in IntelliJ? *(The Run console at the bottom.)*

---

## BEG-005-L05 · VS Code as an alternative (8 min)
**Goal:** know the lighter option exists.

**Key points**
- VS Code is a lightweight editor; Java support comes from extensions.
- Install the Extension Pack for Java.
- It is fine for learning. IntelliJ is the main tool in this course.
- Pick one and stay with it.

**Show:** open a folder in VS Code, write a class, click Run.

**Check:** What must you install to run Java in VS Code? *(The JDK plus the Java extension pack.)*

---

## BEG-005-L06 · Demo: installing the JDK and fixing a broken PATH (8 min)
**Goal:** practise the full setup and the most common failure. Prepares `BEG-005-LAB1`.

**Steps**
1. Install the JDK.
2. Open a new terminal; run `java -version` and `javac -version`.
3. Remove the JDK folder from `PATH` and open a new terminal.
4. Run `java -version` and read the error.
5. **Planned mistake:** fix `PATH` but test in the old terminal; it still fails. Open a new terminal and it works.
