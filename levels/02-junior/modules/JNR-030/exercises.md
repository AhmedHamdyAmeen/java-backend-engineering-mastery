# JNR-030 · Entity relationships — Exercises and lab

## Lab
### JNR-030-LAB1 · Orders
**Outcomes:** 1–4 · **Time:** ~4 h
1. Map `Order` with `OrderLine`s (`cascade = ALL`, `orphanRemoval = true`) and helper methods.
2. Map `Order` many-to-one to `Customer` and `OrderLine` many-to-one to `Product`, both lazy.
3. Write tests: save an order with two lines; remove one line; delete the order.
4. Prove that deleting an order does not delete products or customers.
5. Add `unitPrice` to `OrderLine` to show why it is a join entity, not `@ManyToMany`.

**Acceptance:** removing a line from the collection deletes it; no cascade from order to product.

## Exercises (assessment: map a provided ER diagram)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-030-EX01 | 1 | Map `Product` to `Category` many-to-one with lazy fetch and a join column. |
| JNR-030-EX02 | 1 | Map a one-to-one `Customer` and `CustomerProfile` with a unique foreign key. |
| JNR-030-EX03 | 2 | In a given bidirectional mapping, mark the owning side and write the missing helper method. |
| JNR-030-EX04 | 3 | Choose cascade settings for `Order`->`OrderLine`, `Order`->`Customer`, `OrderLine`->`Product`; justify each. |
| JNR-030-EX05 | 4 | Replace `@ManyToMany Student-Course` with an `Enrollment` entity that stores a grade. |
| JNR-030-EX06 | 1-4 | Map a provided ER diagram (library: Author, Book, Loan, Member) and list your choices. |

## Solutions
- **EX01** `@ManyToOne(fetch = LAZY, optional = false) @JoinColumn(name = "category_id") private Category category;`
- **EX02** `@OneToOne(fetch = LAZY) @JoinColumn(name = "customer_id", unique = true) private Customer customer;` in the profile.
- **EX03** The owning side holds the foreign key (the many-to-one); `mappedBy` marks the inverse. Helper: `addX(x) { xs.add(x); x.setParent(this); }`.
- **EX04** `Order`->`OrderLine`: `ALL` plus orphan removal (owned children); `Order`->`Customer`: none (independent lifecycle); `OrderLine`->`Product`: none.
- **EX05** `Enrollment(id, student ManyToOne, course ManyToOne, grade)`; `Student` and `Course` each hold `@OneToMany(mappedBy)`.
- **EX06** Loan joins Member and Book with dates, so it is an entity; Author-Book is many-to-many (join entity if it has data); keep relationships unidirectional unless needed.
