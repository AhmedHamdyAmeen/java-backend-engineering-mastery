# BEG-032 · Sorting and comparison — Exercises and lab

## Lab
### BEG-032-LAB1 · Leaderboard
**Outcomes:** 1–3 · **Time:** ~1 h
Sort players by score descending, then name ascending, and show the top N. Also keep players in a `TreeSet` using the same comparator.
**Acceptance:** ties ordered correctly.

## Exercises (assessment: three exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-032-EX01 | 1 | Make a `Book` (title, year) implement `Comparable<Book>` by year; sort a list of books. |
| BEG-032-EX02 | 2, 3 | Build a comparator for `Book`: year descending, then title ascending; sort with it. |
| BEG-032-EX03 | 3 | Put books in a `TreeSet` using a title comparator. Add two books with the same title and different years; explain the size. |

## Solutions
- **EX01** `public int compareTo(Book o){ return Integer.compare(year, o.year); }` then `Collections.sort(books);`.
- **EX02** `Comparator.comparingInt(Book::getYear).reversed().thenComparing(Book::getTitle)`.
- **EX03** The set has size 1 for the duplicated title: the comparator returns 0, so the set treats them as the same element. This is why ordering must match what "equal" means for the set.
- Subtraction-overflow mistake is covered in demo L04 and quiz Q09.
