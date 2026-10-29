# BEG-006 · Command line — Exercises and lab

## Lab
### BEG-006-LAB1 · Terminal-only project setup
**Outcomes:** 1–5 · **Time:** ~2 h
Using only the terminal: create a project folder structure, create files, list them sorted by size, save the listing to a file, and search it for a word.
**Acceptance:** a command history file plus the final folder tree.

## Exercises
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-006-EX01 | 1 | From your home folder, go into `Documents`, then back up two levels using relative paths. |
| BEG-006-EX02 | 1 | Print your current folder, then the same location as an absolute path. |
| BEG-006-EX03 | 2 | Create `a/b/c`, create a file in `c`, copy it to `b`, move the original to `a`. |
| BEG-006-EX04 | 2 | Delete the whole `a` folder you made, after checking where you are. |
| BEG-006-EX05 | 3 | Save a folder listing to `list.txt` and show only the lines containing a chosen word. |
| BEG-006-EX06 | 4 | Set a variable `COURSE=java` for this session and print it. |
| BEG-006-EX07 | 5 | Make a script file executable and run it. What happens before and after? |

## Solutions
- **EX01** `cd Documents` then `cd ../..`.
- **EX02** `pwd` (Bash) or `Get-Location` (PowerShell).
- **EX03** `mkdir -p a/b/c; touch a/b/c/f.txt; cp a/b/c/f.txt a/b; mv a/b/c/f.txt a`.
- **EX04** `pwd` first, then `rm -r a`.
- **EX05** `ls > list.txt` then `grep word list.txt`.
- **EX06** `export COURSE=java; echo $COURSE` (PowerShell: `$env:COURSE = "java"; $env:COURSE`).
- **EX07** Before: "Permission denied". After `chmod +x script.sh`: it runs.
