# BEG-015 · Arrays and strings — Exercises and lab

## Lab
### BEG-015-LAB1 · Student-grade manager (mini-project 3 of 3)
**Outcomes:** 1–4 · **Time:** ~3 h
1. Store student names and grades in arrays (read them or start with sample data).
2. Compute the average, highest, and lowest grade, and a letter grade for each student.
3. Search a student by name (ignore case) and show the grade, or "not found".
4. Print an aligned report.
5. Handle an empty class without crashing.

**Acceptance:** correct statistics; case-insensitive search; handles empty class.

## Exercises (assessment: seven exercises plus the grade manager)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-015-EX01 | 1 | Create an `int[]` of 5 numbers, fill it with a loop, print it with `Arrays.toString`, and make a real copy. |
| BEG-015-EX02 | 1 | Create a 3x3 `int[][]` and print its diagonal and the sum of all cells. |
| BEG-015-EX03 | 2 | Given `"  Hello, World  "`: trim it, get its length, the index of "World", and the substring "Hello". |
| BEG-015-EX04 | 2 | Split `"ana,bob,carl"` and print each name in upper case. |
| BEG-015-EX05 | 3 | Explain why `s.toUpperCase();` alone does not change `s`. |
| BEG-015-EX06 | 3 | Build the string "1,2,3,...,1000" with `StringBuilder` and explain why not `+=`. |
| BEG-015-EX07 | 4 | List the valid indices for `new int[4]`; fix a loop with `i <= arr.length`. |

## Solutions
- **EX01** `int[] a = new int[5]; for (int i = 0; i < a.length; i++) a[i] = i * 2; int[] b = Arrays.copyOf(a, a.length);` (`b = a` would not be a copy).
- **EX02** Diagonal `g[i][i]`; sum with two nested loops over `g.length` and `g[r].length`.
- **EX03** `t = s.trim()` gives "Hello, World"; length 12; `t.indexOf("World")` is 7; `t.substring(0, 5)` is "Hello".
- **EX04** `for (String n : "ana,bob,carl".split(",")) System.out.println(n.toUpperCase());`
- **EX05** Strings are immutable; the method returns a new String that must be assigned: `s = s.toUpperCase();`.
- **EX06** `StringBuilder sb; for (i = 1..1000) { if (i > 1) sb.append(','); sb.append(i); }` — `+=` copies the whole string each time.
- **EX07** Valid indices are 0, 1, 2, 3. Change `<=` to `<`.
- Outcome 4 is also tested in the lab (empty class) and quiz.
