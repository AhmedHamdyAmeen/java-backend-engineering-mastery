# BEG-006 · Command line — Lecture scripts

**Video:** 68 min · **Analogy used throughout:** giving written orders to a very literal assistant.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-006-L01 · Terminal, shell, and prompt (8 min)
**Goal:** know what you are typing into.

**Key points**
- The terminal is the window; the shell (Bash, PowerShell) is the program that reads your commands.
- The prompt shows where you are and waits for a command.
- You type a command, press Enter, and read the result.
- Why use it: it is fast, repeatable, and servers have no screen.

**Show:** open Windows Terminal / macOS Terminal and point at the prompt.

**Check:** What is the shell? *(The program that reads and runs your commands.)*

---

## BEG-006-L02 · Paths: absolute, relative, home, `.` and `..` (10 min)
**Goal:** move around folders confidently.

**Key points**
- `pwd` shows where you are; `cd` moves; `ls` (or `dir`) lists.
- Absolute path starts at the root: `C:\Users\Ana` or `/home/ana`.
- Relative path starts from where you are.
- `.` is here, `..` is the parent folder, `~` is your home folder.
- Put quotes around paths with spaces.

**Show:** walk down into a folder and back up with `cd ..`.

**Check:** What does `cd ..` do? *(Moves to the parent folder.)*

---

## BEG-006-L03 · Working with files and folders (12 min)
**Goal:** create, copy, move, and delete from the terminal.

**Key points**
- Make a folder: `mkdir`. Make a file: `touch` (Bash) or `New-Item` (PowerShell).
- Copy: `cp`. Move or rename: `mv`. Delete: `rm`.
- Deleting from the terminal skips the recycle bin.
- Check where you are (`pwd`) before deleting.
- `-r` means "include everything inside" for folders.

**Show:** build a small folder tree, then delete it carefully.

**Check:** How do you rename a file in Bash? *(`mv oldname newname`.)*

---

## BEG-006-L04 · Pipes and redirection (10 min)
**Goal:** connect commands and save output.

**Key points**
- `>` sends output into a file instead of the screen.
- `>>` adds to the end of a file.
- `|` (pipe) sends the output of one command into the next.
- Example: list files, then keep only lines that contain "log".
- Filtering tools: `grep` (Bash), `Select-String` (PowerShell).

**Show:** `ls > files.txt`, then search `files.txt` for a word.

**Check:** What does `>` do? *(Writes the output to a file.)*

---

## BEG-006-L05 · Environment variables in the shell (8 min)
**Goal:** read and set a variable for this session.

**Key points**
- Bash read: `echo $NAME`. Set: `export NAME=value`.
- PowerShell read: `$env:NAME`. Set: `$env:NAME = "value"`.
- It lasts only until you close that terminal.
- Permanent changes go in the system settings or a startup file.

**Show:** set a variable, print it, open a new terminal, see it is gone.

**Check:** Does `export NAME=value` survive closing the terminal? *(No.)*

---

## BEG-006-L06 · Permissions basics (7 min)
**Goal:** explain why a script may refuse to run.

**Key points**
- Files have permissions: read, write, execute.
- On Linux and macOS, `ls -l` shows them; `chmod +x` makes a file executable.
- "Permission denied" usually means you lack a permission.
- Windows uses a different system, but the idea is the same.

**Show:** a script that fails, then works after `chmod +x`.

**Check:** What does `chmod +x script.sh` do? *(Allows the file to be executed.)*

---

## BEG-006-L07 · Bash vs PowerShell cheat sheet (5 min)
**Goal:** one table of equivalent commands.

**Key points**
- Same jobs, different names: list (`ls` / `Get-ChildItem`), show text (`cat` / `Get-Content`), search (`grep` / `Select-String`).
- PowerShell also accepts many Bash-style aliases such as `ls`, `cd`, `cat`.
- Do not mix the two syntaxes in one session.

**Show:** a two-column cheat sheet.

**Check:** What is the PowerShell way to read a variable `X`? *(`$env:X`.)*

---

## BEG-006-L08 · Demo: setting up a project folder using only the terminal (8 min)
**Goal:** do real work without the mouse. Prepares `BEG-006-LAB1`.

**Steps**
1. Make a `demo` folder with `src` and `docs` inside.
2. Create two files and write text into one with `>`.
3. List files, save the listing to `listing.txt`.
4. Search `listing.txt` for a word.
5. **Planned mistake:** run a delete from the wrong folder (on a safe dummy folder); show how `pwd` first would have prevented it.
