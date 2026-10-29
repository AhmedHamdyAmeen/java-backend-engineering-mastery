# BEG-032 · Sorting and comparison — Lecture scripts

**Video:** 38 min · **Analogy used throughout:** ranking runners in a race: first by time, then by name if tied.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-032-L01 · Natural ordering with Comparable (10 min)
**Goal:** give a class its default order.

**Key points**
- `String` and numbers already know how to sort; your own classes do not.
- Implement `Comparable<T>` and write `compareTo`.
- `compareTo` returns negative if this comes first, zero if equal, positive if this comes after.
- Once done, `Collections.sort(list)`, `TreeSet`, and `TreeMap` work with your class.
- Avoid `return a - b`; subtraction can overflow. Use `Integer.compare(a, b)`.

**Show**
```java
class Player implements Comparable<Player> {
    String name; int score;
    public int compareTo(Player o) { return Integer.compare(score, o.score); }
}
```

**Check:** What does a negative result from `compareTo` mean? *(This object comes first.)*

---

## BEG-032-L02 · Comparators (10 min)
**Goal:** sort in a way other than the natural order.

**Key points**
- A `Comparator<T>` is a separate "ruler" that compares two objects.
- You can have many comparators for one class: by name, by score.
- `Comparator.comparing(Player::getName)` builds one from a field.
- `.reversed()` flips the order.
- Use it: `list.sort(comparator)` or `new TreeSet<>(comparator)`.

**Show**
```java
players.sort(Comparator.comparing(Player::getName));
players.sort(Comparator.comparingInt(Player::getScore).reversed());
```

**Check:** When do you use a `Comparator` instead of `Comparable`? *(When you need another order, or cannot change the class.)*

---

## BEG-032-L03 · Multi-key sorting (10 min)
**Goal:** break ties with a second key.

**Key points**
- Chain with `thenComparing`: first key, then second, and so on.
- Example: score descending, then name ascending.
- Use `Comparator.comparingInt(...)` for primitives to avoid boxing.
- Keep ordering consistent with `equals` when objects go in a `TreeSet`/`TreeMap`: two items that compare as 0 are treated as the same element.

**Show**
```java
Comparator<Player> byRank =
    Comparator.comparingInt(Player::getScore).reversed()
              .thenComparing(Player::getName);
```

**Check:** What does `thenComparing` do? *(Compares by another key when the first keys are equal.)*

---

## BEG-032-L04 · Demo: a leaderboard with multi-key comparators (8 min)
**Goal:** build a ranked list. Prepares `BEG-032-LAB1`.

**Steps**
1. Create a `Player` with name and score; add six players, including two tied scores.
2. Sort with score descending only and notice the ties are in random-looking order.
3. Add `thenComparing(Player::getName)`.
4. **Planned mistake:** write `(a, b) -> b.score - a.score` and show why `Integer.compare` is safer (overflow with huge values).
5. Print the top 3 using `subList(0, 3)` or a loop.
