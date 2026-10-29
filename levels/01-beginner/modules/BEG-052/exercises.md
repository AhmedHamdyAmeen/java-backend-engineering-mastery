# BEG-052 · Web fundamentals — Exercises and lab

## Lab
### BEG-052-LAB1 · Read real traffic
**Outcomes:** 1–4 · **Time:** ~2 h
Capture five requests from a real site in the browser's Network tab and annotate method, URL parts, key headers, status, and body type.
**Acceptance:** all parts correctly labeled.

## Exercises (assessment: quiz)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-052-EX01 | 1 | Label the parts of a given raw request and response. |
| BEG-052-EX02 | 2 | Pick a method for: list books, add a book, replace a book, change only a title, delete a book. |
| BEG-052-EX03 | 2 | Name the status class and likely code for: created, not found, not logged in, server crash. |
| BEG-052-EX04 | 3 | Write JSON for a member with a name, an age, and a list of two phone numbers. |
| BEG-052-EX05 | 3 | Draw the Java class that matches your JSON from EX04. |
| BEG-052-EX06 | 4 | Split `https://api.example.com/books?author=herbert&page=2#top` into its parts. |
| BEG-052-EX07 | 2 | Explain why a "delete" link implemented as `GET /deleteBook?id=7` is a bad idea. |

## Solutions
- **EX01** Request: method, URL/path, headers, optional body. Response: status line, headers, body.
- **EX02** `GET`, `POST`, `PUT`, `PATCH`, `DELETE`.
- **EX03** 2xx 201; 4xx 404; 4xx 401; 5xx 500.
- **EX04** `{"name":"Ana","age":30,"phones":["555-0101","555-0102"]}`.
- **EX05** `class Member { String name; int age; List<String> phones; }`.
- **EX06** Scheme `https`, host `api.example.com`, path `/books`, query `author=herbert&page=2`, fragment `top`.
- **EX07** A GET must not change data; browsers, crawlers, and caches may repeat it. Use `DELETE /books/7`.
