# BEG-025 · Relationships — Lecture scripts

**Video:** 43 min · **Analogy used throughout:** a family of contacts: who knows whom, who owns whom, who only borrows a tool once.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-025-L01 · How objects know each other (8 min)
**Goal:** see that objects connect through references.

**Key points**
- Objects work together; to call another object you need a reference to it.
- A reference is stored in a field, received as a parameter, or created locally.
- Where the reference lives decides how long the relationship lasts.
- **Multiplicity** says how many: one, zero or one, many.
- Naming the relationship helps design and communication.

**Show**
```java
class Account { private Customer owner; }       // field: long-lived link
void print(Statement s) { }                      // parameter: short-lived use
```

**Check:** Name two places a reference to another object can come from. *(A field and a method parameter.)*

---

## BEG-025-L02 · Association, aggregation, composition (12 min)
**Goal:** distinguish three "has" relationships.

**Key points**
- **Association:** one object knows another (a Customer uses an Account). The general case.
- **Aggregation:** a whole with parts that can live on their own (a Bank has Customers; customers exist without that bank object).
- **Composition:** parts that cannot exist without the whole (an Account has Transactions; delete the account, the history goes too).
- In code, composition usually means the whole creates and owns the parts, and does not hand out the internal list.
- One-to-many is implemented with a collection: `List<Transaction>`.

**Show**
```java
class Account {
    private final List<Transaction> transactions = new ArrayList<>(); // composition
}
class Bank { private final List<Customer> customers; }               // aggregation
```

**Check:** Which is stronger: aggregation or composition? *(Composition: the parts die with the whole.)*

---

## BEG-025-L03 · Dependency (5 min)
**Goal:** recognize the weakest relationship.

**Key points**
- **Dependency:** a class uses another only briefly, as a parameter or local variable, with no field.
- Example: `Bank.sendStatement(Notifier n)` depends on `Notifier`.
- If the used class changes, the user may break.
- Fewer dependencies mean easier changes: prefer depending on interfaces.
- Not every dependency needs a drawing in a diagram.

**Show:** `void print(Report r) { r.render(); }` (no field, so a dependency only).

**Check:** Does a dependency need a field? *(No; a parameter or local use is enough.)*

---

## BEG-025-L04 · UML class diagrams, the useful 20% (10 min)
**Goal:** draw a small diagram that others can read.

**Key points**
- A class is a box with its name, and optionally key fields and methods in compartments. Do not list every field.
- Association: a solid line; label with a role and multiplicity (`1`, `0..1`, `*`).
- Aggregation: hollow diamond on the whole's side. Composition: filled diamond.
- Dependency: dashed arrow. Inheritance: solid line with a hollow triangle at the parent. Interface implementation: dashed line with hollow triangle.
- Draw first, code second; keep it to one page.

**Show:** a diagram: `Customer 1 ——— * Account`, `Account ◆——— * Transaction` (filled diamond at Account).

**Check:** What does a filled diamond mean? *(Composition: the whole owns the parts.)*

---

## BEG-025-L05 · Demo: drawing the UML, then coding Customer and Account (8 min)
**Goal:** turn a diagram into code. Prepares `BEG-025-LAB1`.

**Steps**
1. Sketch `Customer 1 — * Account` and `Account ◆— * Transaction` on paper or a drawing tool.
2. Code `Transaction` as a small immutable class (type, amount, date).
3. Code `Account` with a private `List<Transaction>`; `deposit` and `withdraw` add transactions.
4. Code `Customer` with a private `List<Account>` and `openAccount(...)`.
5. **Planned mistake:** also store `Customer` inside `Account` and forget to set it when opening an account, leaving a `null`. Fix by setting both sides in one method, or drop the back link if not needed.
6. Compare diagram and code; they must match.
