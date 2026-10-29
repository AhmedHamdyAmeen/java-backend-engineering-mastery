# BEG-036 · Stream API — Exercises and lab

## Lab
### BEG-036-LAB1 · Sales report
**Outcomes:** 1–4 · **Time:** ~2.5 h
From a list of orders compute revenue by category, top customers, and average order value per month. Keep each pipeline short and readable; note any step you wrote as a loop and why.
**Acceptance:** correct results, readable pipelines.

## Exercises (assessment: six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-036-EX01 | 1 | From a list of names, produce the distinct, upper-case names longer than 3 letters, sorted, first 5 only. |
| BEG-036-EX02 | 2 | Given integers, compute the sum with `reduce`, test whether any is negative, and count the evens. |
| BEG-036-EX03 | 1 | Given `List<Order>` where each has `List<String> items`, produce a flat list of distinct item names. |
| BEG-036-EX04 | 3 | Group people by city and count them; then group orders by category and sum the amounts. |
| BEG-036-EX05 | 2 | Find the first person older than 60 and print their name, or "none". |
| BEG-036-EX06 | 4 | Review: rewrite a 10-step stream chain with a side effect as a loop, and justify the change in two sentences. |

## Solutions
- **EX01** `names.stream().filter(n -> n.length() > 3).map(String::toUpperCase).distinct().sorted().limit(5).toList();`
- **EX02** `reduce(0, Integer::sum)`; `anyMatch(n -> n < 0)`; `filter(n -> n % 2 == 0).count()`.
- **EX03** `orders.stream().flatMap(o -> o.getItems().stream()).distinct().toList();`
- **EX04** `groupingBy(Person::getCity, counting())`; `groupingBy(Order::getCategory, summingDouble(Order::getAmount))`.
- **EX05** `people.stream().filter(p -> p.getAge() > 60).findFirst()` returns an `Optional`; for now use `.map(Person::getName).orElse("none")`.
- **EX06** A named-variable loop with the side effect inside; the answer says the loop is easier to read and debug and the side effect is explicit.
- Reusing a consumed stream is covered in demo L07 and quiz Q09.
