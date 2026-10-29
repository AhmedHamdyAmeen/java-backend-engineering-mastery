# BEG-053 · API fundamentals — Exercises and lab

## Lab
### BEG-053-LAB1 · API explorer
**Outcomes:** 1–3 · **Time:** ~2 h
Call a public API for a list, a single item, and a filtered query; save a Postman collection; then sketch the endpoints a Library API would need.
**Acceptance:** collection exported; endpoint sketch reviewed.

## Exercises (assessment: endpoint design exercise)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-053-EX01 | 1 | Explain what an API is to a non-programmer in three sentences. |
| BEG-053-EX02 | 1 | Name the resources in a school system and write their URLs. |
| BEG-053-EX03 | 1 | Fix these URLs: `/getBooks`, `/createMember`, `/book/delete/7`. |
| BEG-053-EX04 | 2 | Call a public API with Postman and with `curl`; compare the responses. |
| BEG-053-EX05 | 2 | Read an API's docs and call one endpoint with a query parameter. |
| BEG-053-EX06 | 3 | Sketch endpoints (URL, method, status) for `members`. |
| BEG-053-EX07 | 3 | Sketch an endpoint for "loans of one member" and for "overdue loans". |

## Solutions
- **EX01** An API is a menu of requests a program may make to another; the provider decides the rules and hides the inside.
- **EX02** `/students`, `/teachers`, `/courses`, `/students/5/enrollments`.
- **EX03** `GET /books`, `POST /members`, `DELETE /books/7`.
- **EX04** Same data; `curl -i` also shows status and headers.
- **EX05** For example `GET /items?limit=5`; check status 200.
- **EX06** `GET /members` 200; `GET /members/{id}` 200/404; `POST /members` 201/400; `PUT /members/{id}` 200/404; `DELETE /members/{id}` 204/404.
- **EX07** `GET /members/{id}/loans`; `GET /loans?status=overdue`.
