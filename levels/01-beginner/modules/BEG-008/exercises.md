# BEG-008 · First Java program — Exercises and lab

## Lab
### BEG-008-LAB1 · Business card
**Outcomes:** 1–4 · **Time:** ~2 h
1. Print a formatted multi-line business card (name, role, email, phone) using `println` and `print`.
2. Add a Javadoc comment on the class and one useful `//` comment.
3. Fix the five broken programs below using only the compiler messages.

**Acceptance:** all five compile and print `Hello`; the card prints as designed.

### The five broken programs (all should print `Hello`)
```java
// B1
public class B1 {
    public static void main(String[] args) {
        System.out.println("Hello")
    }
}
```
```java
// B2
public class B2 {
    public static void main(String[] args) {
        system.out.println("Hello");
    }
}
```
```java
// B3
public class B3 {
    public static void main(String[] args) {
        System.out.println("Hello");
    }
```
```java
// B4
public class B4 {
    public static void main(String args) {
        System.out.println("Hello");
    }
}
```
```java
// B5
public class B5 {
    public static void main(String[] args) {
        System.out.println("Hello);
    }
}
```

## Exercises (assessment: EX01–EX05)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-008-EX01 | 1 | Label the parts of Hello World: class line, `main` line, braces, statement. |
| BEG-008-EX02 | 2 | Print your name on one line and your city on the next, using only `print`. |
| BEG-008-EX03 | 2 | Print `Total: 3 items` by joining text and the number 3. |
| BEG-008-EX04 | 3 | Add a single-line, a multi-line, and a Javadoc comment to any program. Which one would you keep and why? |
| BEG-008-EX05 | 4 | Rename `main` to `Main` and read the error. What does the JVM say? |

## Solutions
- **Lab fixes** B1 add `;`. B2 `System`. B3 add the final `}`. B4 `String[] args`. B5 close the quote.
- **EX01** `public class Hello` is the class line; `public static void main(String[] args)` is the entry point; `{ }` are blocks; `System.out.println(...);` is the statement.
- **EX02** `System.out.print("Ana\n"); System.out.print("Cairo");`
- **EX03** `System.out.println("Total: " + 3 + " items");`
- **EX04** Keep comments that explain why, not what.
- **EX05** Compile succeeds but running reports that no `main` method was found.
