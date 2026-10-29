# BEG-020 · Classes and objects — Exercises and lab

## Lab
### BEG-020-LAB1 · Bank Accounts v1
**Outcomes:** 1, 2, 3, 4 · **Time:** ~2 h
Write an `Account` class with owner, number, and balance; a full constructor and an overloaded one; `deposit` and `withdraw`. In `main`, create several accounts and use them. Add a static counter of accounts created.
**Acceptance:** compiles, works, no logic in `main` beyond wiring.

## Exercises (assessment: 5 exercises plus Bank Accounts v1)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-020-EX01 | 1 | Write a `Book` class with title, author, pages, and two constructors (one with pages defaulting to 100). |
| BEG-020-EX02 | 2 | Create two `Book` objects, change one's pages, and show the other is unchanged. |
| BEG-020-EX03 | 3 | Find and fix the bug: `Book(String title) { title = title; }`. |
| BEG-020-EX04 | 3 | Rewrite the second constructor of EX01 to use `this(...)` to call the first. |
| BEG-020-EX05 | 4 | Decide static or instance for: `pages`, `Book.count`, `isLong()`, `MAX_PAGES`. Justify each. |

## Solutions
- **EX01**
  ```java
  public class Book {
      String title, author; int pages;
      Book(String title, String author, int pages) { this.title = title; this.author = author; this.pages = pages; }
      Book(String title, String author) { this(title, author, 100); }
  }
  ```
- **EX02** `a.pages = 300;` then `b.pages` still prints its own value; each object has its own copy.
- **EX03** The parameter is assigned to itself and the field stays `null`. Use `this.title = title;`.
- **EX04** Shown in EX01: `this(title, author, 100);` must be the first statement.
- **EX05** `pages` instance; `Book.count` static (shared); `isLong()` instance (uses this book's pages); `MAX_PAGES` static final constant.
- Outcomes 1-4 are also covered by the lab and quiz.
