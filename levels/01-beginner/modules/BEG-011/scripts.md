# BEG-011 · Input and output — Lecture scripts

**Video:** 48 min · **Analogy used throughout:** a shop counter: ask the customer, check what they say, print a receipt.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-011-L01 · Reading input with Scanner (10 min)
**Goal:** read text and numbers from the keyboard.

**Key points**
- Import it: `import java.util.Scanner;`.
- Create one: `Scanner in = new Scanner(System.in);`.
- `in.nextLine()` reads a whole line of text. `in.nextInt()` reads an int. `in.nextDouble()` reads a decimal.
- Always print a prompt first so the user knows what to type.
- Close the scanner when finished: `in.close();`.

**Show**
```java
Scanner in = new Scanner(System.in);
System.out.print("Name: ");
String name = in.nextLine();
System.out.println("Hi, " + name);
```

**Check:** Which method reads a whole line? *(`nextLine()`.)*

---

## BEG-011-L02 · The `nextInt` / `nextLine` trap (8 min)
**Goal:** avoid the skipped-input bug.

**Key points**
- `nextInt()` reads the number but leaves the Enter key (the new line) in the input.
- The next `nextLine()` then reads that leftover and returns an empty string.
- Fix: call `in.nextLine()` once after `nextInt()` to throw away the leftover.
- Or read everything with `nextLine()` and convert it yourself.

**Show:** the bug (the name prompt is skipped after reading an age), then the one-line fix.

**Check:** Why does `nextLine()` return empty after `nextInt()`? *(It reads the leftover Enter.)*

---

## BEG-011-L03 · Parsing strings into numbers (8 min)
**Goal:** convert text to numbers.

**Key points**
- Input arrives as text; numbers must be converted.
- `Integer.parseInt("42")` gives `42`. `Double.parseDouble("3.5")` gives `3.5`.
- Bad text such as `"abc"` makes the program stop with an error.
- Check before reading: `in.hasNextInt()` is true only if an int is waiting.

**Show:** `Integer.parseInt("42") + 1` is `43`; `"42" + 1` is `"421"`.

**Check:** What is `Integer.parseInt("7") * 2`? *(14.)*

---

## BEG-011-L04 · Formatting output (8 min)
**Goal:** print neat, aligned numbers.

**Key points**
- `System.out.printf("format", values...)` prints formatted text.
- `%d` int, `%f` decimal, `%s` text, `%n` new line.
- `%.2f` keeps 2 decimals. `%8.2f` is 8 characters wide.
- `%-10s` left-aligns text in 10 characters; `%10s` right-aligns.
- `String.format(...)` builds the same text as a `String`.

**Show**
```java
System.out.printf("%-10s %3d %8.2f%n", "Pen", 2, 1.5);
```

**Check:** What does `%.2f` do? *(Prints a decimal with two digits after the point.)*

---

## BEG-011-L05 · Validating input: never trust the user (6 min)
**Goal:** accept only valid input.

**Key points**
- Users type the wrong thing: letters instead of numbers, negative amounts, nothing at all.
- Check input before using it. Re-ask until it is valid.
- Pattern: loop while `!in.hasNextInt()`, discard the bad token, ask again.
- Check ranges too: a quantity must be at least 1.
- The same rule applies to every program that takes input from anywhere, including web requests later.

**Show**
```java
int qty;
while (true) {
    System.out.print("Quantity: ");
    if (in.hasNextInt()) {
        qty = in.nextInt();
        if (qty >= 1) break;
    } else {
        in.next(); // discard bad text
    }
    System.out.println("Enter a whole number, 1 or more.");
}
```

**Check:** Why validate even if the user is friendly? *(Mistakes happen, and bad input can break or attack the program.)*

---

## BEG-011-L06 · Demo: building the receipt printer with input validation (8 min)
**Goal:** combine input, validation, and formatting. Prepares `BEG-011-LAB1`.

**Steps**
1. Ask for an item name, quantity, and price.
2. Validate the quantity (whole number, 1 or more) with a loop.
3. Calculate line total and 15% tax.
4. Print an aligned receipt with `printf`.
5. **Planned mistake:** read the quantity with `nextInt()` and then the item name with `nextLine()`; the name is skipped. Fix with the extra `nextLine()`.
6. Try typing `abc` as the quantity and watch it re-prompt.
