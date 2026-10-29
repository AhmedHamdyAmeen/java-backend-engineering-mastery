# BEG-015 · Arrays and strings — Lecture scripts

**Video:** 74 min · **Analogy used throughout:** a row of numbered lockers (starting at 0), and a printed sheet of text that cannot be erased, only reprinted.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-015-L01 · Arrays: fixed-size lists (10 min)
**Goal:** store many values of one type under one name.

**Key points**
- An array is a row of lockers: fixed size, same type, numbered from 0.
- Create: `int[] scores = new int[5];` (all zeros) or `{80, 90, 70}`.
- Read and write with an index: `scores[0] = 95;`.
- `scores.length` is the size (no parentheses).
- The first index is 0 and the last is `length - 1`.

**Show**
```java
int[] scores = {80, 90, 70};
System.out.println(scores[1]);     // 90
System.out.println(scores.length); // 3
```

**Check:** What is the last valid index of an array of 5? *(4.)*

---

## BEG-015-L02 · Iterating and enhanced for (8 min)
**Goal:** visit every element and avoid bad indices.

**Key points**
- Classic loop: `for (int i = 0; i < arr.length; i++)`. Use `<`, not `<=`.
- Enhanced for: `for (int s : scores)` visits each value, no index needed.
- Use the classic loop when you need the index or want to change elements.
- Using index `length` throws `ArrayIndexOutOfBoundsException`.
- To stay safe, ask: is my index between 0 and `length - 1`?

**Show**
```java
int total = 0;
for (int s : scores) {
    total += s;
}
```

**Check:** What error does `scores[scores.length]` cause? *(`ArrayIndexOutOfBoundsException`.)*

---

## BEG-015-L03 · Two-dimensional arrays (10 min)
**Goal:** store a table of rows and columns.

**Key points**
- A 2D array is an array of arrays: a grid of lockers.
- Declare: `int[][] grid = new int[3][4];` (3 rows, 4 columns).
- Access: `grid[row][col]`.
- `grid.length` is rows; `grid[0].length` is columns.
- Use nested loops to visit every cell.

**Show**
```java
int[][] grid = new int[3][4];
for (int r = 0; r < grid.length; r++) {
    for (int c = 0; c < grid[r].length; c++) {
        grid[r][c] = r * c;
    }
}
```

**Check:** What is `grid[0].length` for `new int[3][4]`? *(4.)*

---

## BEG-015-L04 · Working with Strings (12 min)
**Goal:** use the everyday `String` methods.

**Key points**
- `length()`, `charAt(i)` (first char is index 0), `substring(a, b)` (b excluded).
- `indexOf("x")` gives the position, or -1 if missing.
- `trim()` removes spaces at both ends; `toUpperCase()`, `toLowerCase()`.
- `split(",")` cuts text into a `String[]`.
- Compare text with `equals` (or `equalsIgnoreCase`), never `==`.

**Show**
```java
String s = "  Java,Rocks ";
String t = s.trim();           // "Java,Rocks"
String[] p = t.split(",");     // {"Java", "Rocks"}
System.out.println(p[1].equals("Rocks")); // true
```

**Check:** Why not `==` for text? *(`==` compares references; `equals` compares the characters.)*

---

## BEG-015-L05 · Immutability and StringBuilder (10 min)
**Goal:** understand why changing a String makes a new one, and how to avoid waste.

**Key points**
- A `String` never changes: `toUpperCase()` returns a new String (the printed sheet is reprinted).
- `s = s + "x"` in a loop creates a new String every time, which is slow for big loops.
- `StringBuilder` is a notebook you can edit in place.
- Use `append(...)`, then `toString()` at the end.
- Use `+` for a few pieces; `StringBuilder` for loops.

**Show**
```java
StringBuilder sb = new StringBuilder();
for (int i = 1; i <= 5; i++) {
    sb.append(i).append(' ');
}
String result = sb.toString(); // "1 2 3 4 5 "
```

**Check:** Does `s.toUpperCase()` change `s`? *(No, it returns a new String.)*

---

## BEG-015-L06 · `Arrays` utility class (8 min)
**Goal:** use ready-made helpers for arrays.

**Key points**
- `Arrays.toString(arr)` prints readable content; `println(arr)` prints a code.
- `Arrays.sort(arr)` sorts in place.
- `Arrays.copyOf(arr, n)` makes a copy; `arr2 = arr` only copies the reference.
- `Arrays.fill(arr, v)` sets every element.
- `Arrays.equals(a, b)` compares contents; `a == b` does not.

**Show**
```java
int[] a = {3, 1, 2};
Arrays.sort(a);
System.out.println(Arrays.toString(a)); // [1, 2, 3]
```

**Check:** Does `int[] b = a;` make a copy? *(No, both names point to the same array.)*

---

## BEG-015-L07 · Demo: student-grade manager with arrays (8 min)
**Goal:** build the core of the grade manager. Prepares `BEG-015-LAB1`.

**Steps**
1. Create parallel arrays `String[] names` and `double[] grades`.
2. Loop to compute the average, highest, and lowest.
3. Write a `letterGrade(double)` method.
4. Add a search by name with `equalsIgnoreCase`.
5. **Planned mistake:** loop with `i <= grades.length`; `ArrayIndexOutOfBoundsException`. Read the line number in the trace and fix to `<`.
6. Test an empty class: avoid dividing by zero.

**Check:** Why guard against an empty class? *(An average over zero students divides by zero.)*

---

## BEG-015-L08 · Demo: string bugs: `==`, off-by-one, and slow concatenation (8 min)
**Goal:** see three classic string bugs and fix each.

**Steps**
1. Compare `new String("hi") == "hi"`: prints false. Use `equals`.
2. Take `s.substring(0, s.length() + 1)`: `StringIndexOutOfBoundsException`; the end index is exclusive and must be at most `length()`.
3. Build a 100,000-item string with `+=` in a loop and time it.
4. **Planned mistake:** leave the `+=` version in. Rewrite it with `StringBuilder` and compare the time.
5. Summarize: `equals`, check bounds, `StringBuilder` in loops.

**Check:** Which of the three bugs is about speed, not wrong output? *(Slow concatenation in a loop.)*
