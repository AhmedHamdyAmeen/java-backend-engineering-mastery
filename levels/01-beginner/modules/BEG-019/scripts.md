# BEG-019 · OOP introduction — Lecture scripts

**Video:** 43 min · **Analogy used throughout:** a real bank branch with tellers, customers, and account cards.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-019-L01 · When procedural code stops scaling (10 min)
**Goal:** see why loose variables and functions get hard to manage as a program grows.

**Key points**
- Procedural code = data in variables, logic in separate methods that receive the data.
- With one account it is easy. With 1,000 accounts you need parallel arrays: `owners[]`, `balances[]`, `numbers[]`.
- Any method can change any array, so nothing protects the data.
- Adding a new field (say `currency`) means touching every method and array.
- Object-oriented programming (OOP) groups data and the methods that use it into one unit.

**Show**
```java
String[] owners = {"Ana", "Omar"};
double[] balances = {100.0, 50.0};
static void deposit(double[] balances, int i, double amount) { balances[i] += amount; }
```
Point out: nothing stops `balances[7] = -999;` from anywhere.

**Check:** Name one problem with parallel arrays for accounts. *(Related data is split apart, so it is easy to mix up or corrupt.)*

---

## BEG-019-L02 · Objects: state + behavior (10 min)
**Goal:** describe anything as an object with state and behavior.

**Key points**
- An object is a thing in your program that has **state** (what it knows) and **behavior** (what it can do).
- A bank account: state = owner, number, balance. Behavior = deposit, withdraw, show balance.
- State is stored in **fields**; behavior is written as **methods**.
- Each object has its own state: Ana's balance is not Omar's.
- Objects talk to each other by calling methods.

**Show:** a drawing of an account card with a "state" box (owner, number, balance) and a "behavior" box (deposit, withdraw).

**Check:** Is "withdraw" state or behavior? *(Behavior.)*

---

## BEG-019-L03 · Classes as blueprints (7 min)
**Goal:** explain the difference between a class and an object.

**Key points**
- A **class** is the blueprint: it says which fields and methods exist.
- An **object** (or instance) is one real thing built from the blueprint.
- One class can make many objects, each with its own values.
- Like a form template and the filled-in forms.
- The class is written once; objects are created while the program runs.

**Show**
```java
class Account { String owner; double balance; }   // blueprint
// objects built from it: Ana's account, Omar's account
```

**Check:** How many objects can one class create? *(As many as you need.)*

---

## BEG-019-L04 · Finding objects in a problem description (8 min)
**Goal:** pull candidate classes out of plain text.

**Key points**
- Read the description; underline **nouns** (candidate classes or fields) and **verbs** (candidate behaviors).
- Not every noun is a class. "Balance" is a field of an account, not a class of its own.
- Drop nouns that are outside the system ("the weather") or just synonyms.
- Ask: does it have state and behavior that matter here?
- It is a first guess; you will improve it later.

**Show:** "A customer opens an account. The customer deposits money. The bank keeps a record of each transaction." Nouns: customer, account, money, bank, transaction. Verbs: open, deposit, keep record.

**Check:** Should "money" automatically be its own class? *(Not automatically: it may be just a number field for now.)*

---

## BEG-019-L05 · Demo: rewriting a procedural bank as objects (8 min)
**Goal:** convert the parallel-array bank into an `Account` class. Prepares `BEG-019-LAB1`.

**Steps**
1. Show the procedural version with three arrays and static `deposit`/`withdraw` methods.
2. List the nouns and verbs of the description on screen.
3. Create an `Account` class with `owner`, `number`, `balance` fields.
4. Move `deposit` into the class so it works on its own balance.
5. **Planned mistake:** keep `deposit` as a separate method outside the class that takes the account as a parameter. Discuss: the behavior is separated from the data it acts on; move it inside.
6. Compare both versions side by side and note the code in `main` shrinks.
