# BEG-028 · OOP design practice — Lecture scripts

**Video:** 53 min · **Analogy used throughout:** staffing a small shop: give each job to the person who already has the tools and information for it.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-028-L01 · From requirements to classes: worked example (15 min)
**Goal:** turn a written description into a first design.

**Key points**
- Read the requirements; underline nouns (candidate classes) and verbs (candidate behaviors).
- Mark rules ("a ticket is valid for one visit") as invariants for a class.
- Decide relationships: has-a, is-a, uses (dependency), and multiplicities.
- Sketch a small UML diagram; expect to revise it.
- Start with the simplest design that works; add interfaces and inheritance only when a real variation appears.

**Show:** requirement "A library lends books to members; each loan has a due date; late loans pay a fine." Candidates: `Library`, `Book`, `Member`, `Loan`, `Fine` (maybe just a method on `Loan`). A small diagram with `Member 1 — * Loan * — 1 Book`.

**Check:** Is every noun a class? *(No; some are just fields or rules.)*

---

## BEG-028-L02 · Assigning responsibilities (10 min)
**Goal:** put each behavior where the information is.

**Key points**
- Ask: which class already has the data needed for this job? Give it the job.
- A `Loan` knows its due date, so `Loan.isOverdue(today)` and `fine(today)` belong there.
- Avoid a "manager" that reads data from others and does all the work.
- Give each class one clear reason to change (single responsibility).
- If you pass lots of data between two classes, the behavior may be in the wrong place.

**Show**
```java
class Loan {
    private final LocalDate due;
    boolean isOverdue(LocalDate today) { return today.isAfter(due); }
}
```

**Check:** Where does "is this loan overdue?" belong? *(In `Loan`, which owns the due date.)*

---

## BEG-028-L03 · Recognizing and splitting god classes (10 min)
**Goal:** find an overloaded class and divide it.

**Key points**
- A **god class** does too much: hundreds of lines, many unrelated fields, names like `Manager` or `Util`.
- Smell: you describe it with "and" ("it prices tickets and prints receipts and saves files").
- Split by responsibility: pricing, receipts, storage become separate classes.
- The opposite smell is the **anemic** class: only data, with all logic elsewhere.
- Split gradually, keeping the program working after each step.

**Show:** `ParkingManager` with `park()`, `calculateFee()`, `printTicket()`, `saveToFile()`, split into `Garage`, `FeePolicy`, `TicketPrinter`, `TicketStore`.

**Check:** What is one sign of a god class? *(It does many unrelated jobs; its description needs several "and"s.)*

---

## BEG-028-L04 · Explaining a design (10 min)
**Goal:** present and defend design choices to a reviewer.

**Key points**
- Start with the problem, then the main classes and how they cooperate.
- For each key decision, say the option you rejected and why (trade-off).
- Show the UML diagram and one walk-through scenario ("a car enters").
- Admit weaknesses and what you would change with more time.
- Listen to review comments; a design is not a verdict on you.

**Show:** a half-page rationale template: Problem, Main classes, Key decisions and trade-offs, Risks, Next steps.

**Check:** Why mention the options you rejected? *(It shows the choice was deliberate and lets the reviewer check your reasoning.)*

---

## BEG-028-L05 · Demo: modeling the parking garage from requirements (8 min)
**Goal:** go from text to a small working design. Prepares `BEG-028-LAB1`.

**Steps**
1. Read the requirements: levels, spots of different sizes, vehicles, tickets, fees by time.
2. List nouns and verbs; pick `Garage`, `Level`, `Spot`, `Vehicle`, `Ticket`, `FeePolicy`.
3. Assign responsibilities: `Spot` knows if it fits a vehicle; `Ticket` knows entry time; `FeePolicy` computes the fee.
4. Draw the UML and implement `park` and `leave` in `Garage`, delegating to the others.
5. **Planned mistake:** first put fee logic inside `Garage`; show how it grows into a god class, then move it into `FeePolicy`.
6. Walk through one scenario and write the three-line design rationale.
