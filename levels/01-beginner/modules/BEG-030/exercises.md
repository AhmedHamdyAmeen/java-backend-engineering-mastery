# BEG-030 · Collections — Exercises and lab

## Lab
### BEG-030-LAB1 · Word frequency
**Outcomes:** 1–4 · **Time:** ~3 h
Read a paragraph (a file or a text block). Count word frequencies with a `Map`, list the unique words alphabetically, and show the top 10 by count. Write one line explaining each collection you chose.
**Acceptance:** correct counts; justified collection choices.

## Exercises (assessment: six exercises plus a collection-choice quiz)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-030-EX01 | 1 | Create a `List<String>` of five names; add, remove one by value, and print its size and the second element. |
| BEG-030-EX02 | 1 | Remove duplicates from a list of numbers using a `Set`; print the result in the original order. |
| BEG-030-EX03 | 2 | For each need, pick the class: sorted unique names; fast key lookup; insertion-ordered unique tags; frequent insert at the front. |
| BEG-030-EX04 | 1 | Use a `Queue` to simulate three customers being served in arrival order. |
| BEG-030-EX05 | 3 | Remove all negative numbers from a list, first showing the failing for-each version, then a safe fix. |
| BEG-030-EX06 | 4 | Rewrite `ArrayList<String> x = new ArrayList<String>();` using interface type and diamond; explain the benefit. |

## Solutions
- **EX01** `List<String> l = new ArrayList<>(List.of("a","b","c","d","e")); l.add("f"); l.remove("c"); l.size(); l.get(1);`
- **EX02** `new ArrayList<>(new LinkedHashSet<>(numbers))` keeps first-seen order.
- **EX03** `TreeSet`; `HashMap`; `LinkedHashSet`; `ArrayDeque`/`LinkedList` (use `addFirst`).
- **EX04** `Queue<String> q = new ArrayDeque<>(); q.offer(...)` three times, then `while (!q.isEmpty()) System.out.println(q.poll());`.
- **EX05** For-each with `remove` throws `ConcurrentModificationException`; fix: `list.removeIf(n -> n < 0);`.
- **EX06** `List<String> x = new ArrayList<>();` The variable type is the interface, so the implementation can change in one place.
- The collection-choice quiz is `quiz.md`; it also covers outcome 2.
