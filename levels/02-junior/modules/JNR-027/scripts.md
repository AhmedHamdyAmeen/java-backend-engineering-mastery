# JNR-027 · ORM fundamentals — Lecture scripts

**Video:** 45 min · **Analogy used throughout:** a translator between two languages (objects and tables) who is helpful but sometimes loses meaning.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## JNR-027-L01 · Objects vs tables (10 min)
**Goal:** name the four ways objects and tables do not fit together.

**Key points**
- This gap is called the object-relational impedance mismatch.
- Identity: Java has `==` and `equals`; tables have a primary key.
- Inheritance: objects have subclasses; tables have no such thing, so you choose a layout.
- Associations: objects hold references (and can point both ways); tables use foreign keys (one direction, many-to-many needs a join table).
- Granularity: one object may hold nested value objects (`Money`), while a table row is flat.

**Show:** a drawing of `Order` with a `List<OrderLine>` next to the tables `orders` and `order_line` with a foreign key.

**Check:** Which mismatch is shown by a `Money` object stored in two columns? *(Granularity.)*

---

## JNR-027-L02 · What an ORM does (10 min)
**Goal:** list what an ORM automates and what it costs.

**Key points**
- ORM (object-relational mapper) maps classes to tables and generates SQL for you.
- It automates: insert/update/delete/select statements, row-to-object conversion, id handling, and change tracking.
- It costs: hidden SQL, surprise queries, a learning curve, and a performance model you must understand.
- It does not remove the need to know SQL; you still design tables and read the generated statements.
- JPA is the Java standard (a specification); Hibernate is the common implementation.

**Show**
```java
Product p = em.find(Product.class, 42L); // select ... where id = 42
p.setPrice(new BigDecimal("9.99"));      // no SQL yet; update is generated later
```

**Check:** Is JPA a library or a specification? *(A specification; Hibernate implements it.)*

---

## JNR-027-L03 · The persistence context (15 min)
**Goal:** explain the persistence context as an identity map and a unit of work.

**Key points**
- The persistence context is a per-transaction workspace holding the entities you loaded.
- Identity map: asking for the same id twice returns the same Java object, with no second query.
- Unit of work: it remembers the original state; at flush time it compares and writes only what changed.
- Flush means "send pending SQL now"; commit makes it permanent.
- Entities outside the workspace are detached: changes to them are not saved.

**Show**
```java
Product a = em.find(Product.class, 1L); // SQL select
Product b = em.find(Product.class, 1L); // no SQL, from the identity map
System.out.println(a == b);             // true
a.setName("New");                       // tracked; update at flush
```

**Check:** Why does the second `find` issue no SQL? *(The entity is already in the persistence context.)*

---

## JNR-027-L04 · Demo: watching the persistence context with SQL logging (10 min)
**Goal:** see when SQL really runs; prepares JNR-027-LAB1 and JNR-028.

**Steps**
1. Enable `spring.jpa.show-sql` (or `logging.level.org.hibernate.SQL=DEBUG`) in a throwaway sandbox project.
2. Call `find` twice for the same id inside one transaction; count the selects (one).
3. Change a field on the loaded entity and print a marker line before the transaction ends; show the update appears after the marker, at commit.
4. **Planned mistake:** call `find` outside any transaction and change a field; show nothing is saved, then add a transaction.
5. Summarize: identity map avoided a query, unit of work delayed the update.
