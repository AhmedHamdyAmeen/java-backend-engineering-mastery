# JNR-030 · Entity relationships — Lecture scripts

**Video:** 79 min · **Analogy used throughout:** folders and sticky notes: a sticky note (foreign key) on one document points to another; the folder (aggregate) owns the pages inside it.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## JNR-030-L01 · Many-to-one: the default relationship (10 min)
**Goal:** map the most common relationship correctly.

**Key points**
- Many `Product`s belong to one `Category`: `@ManyToOne` on the product.
- The table holding the foreign key is the "many" side (`product.category_id`).
- `@JoinColumn` names the foreign key column.
- Use `fetch = FetchType.LAZY`; the default for `@ManyToOne` is `EAGER`, which often causes extra queries.
- Start here; most designs need only this plus a query.

**Show**
```java
@ManyToOne(fetch = FetchType.LAZY, optional = false)
@JoinColumn(name = "category_id")
private Category category;
```

**Check:** Which table holds the foreign key in a many-to-one? *(The "many" side.)*

---

## JNR-030-L02 · One-to-many and the owning side (12 min)
**Goal:** map the collection side and know who owns the relationship.

**Key points**
- `@OneToMany(mappedBy = "order")` is the inverse side: it shows the children but does not write the foreign key.
- The side with `@JoinColumn` (the many-to-one) is the owning side; only its value is saved.
- Keep both sides in sync with helper methods (`addLine`, `removeLine`).
- Initialize collections (`new ArrayList<>()`) and expose them carefully.
- Forgetting to set the owning side saves a `null` foreign key.

**Show**
```java
@OneToMany(mappedBy = "order", cascade = CascadeType.ALL, orphanRemoval = true)
private List<OrderLine> lines = new ArrayList<>();

public void addLine(OrderLine line) {
    lines.add(line);
    line.setOrder(this);   // owning side
}
```

**Check:** Which side's value is written to the foreign key column? *(The owning side, the one without `mappedBy`.)*

---

## JNR-030-L03 · One-to-one (7 min)
**Goal:** map a one-to-one link and know its trade-offs.

**Key points**
- `@OneToOne` with a unique foreign key column on the owning side.
- Typical example: `Customer` and `CustomerProfile`.
- Inverse (`mappedBy`) one-to-one cannot be lazy easily, because Hibernate must check if the row exists.
- `@MapsId` shares the primary key with the parent and avoids a separate key.
- Often an `@Embeddable` or a plain column set is simpler.

**Show**
```java
@OneToOne(fetch = FetchType.LAZY)
@JoinColumn(name = "customer_id", unique = true)
private Customer customer;
```

**Check:** When might an embeddable be better than one-to-one? *(When the data has no identity and lives in the same table.)*

---

## JNR-030-L04 · Many-to-many and join entities (10 min)
**Goal:** know when `@ManyToMany` is enough and when to model the link.

**Key points**
- `@ManyToMany` uses a hidden join table with only the two foreign keys.
- It cannot hold extra data (quantity, date, price at the time).
- When the link has data, create an entity for it (`OrderLine` links `Order` and `Product` with quantity and price).
- Each side then has a plain `@OneToMany` to the join entity.
- Prefer explicit join entities from the start in real systems.

**Show:** a diagram: `Order 1 — * OrderLine * — 1 Product`, where `OrderLine` has `quantity` and `unitPrice`.

**Check:** Where do you store the quantity of a product in an order? *(In the join entity `OrderLine`.)*

---

## JNR-030-L05 · Cascades and orphan removal (10 min)
**Goal:** choose cascade types on purpose.

**Key points**
- Cascade passes an operation (`persist`, `remove`, ...) from parent to children.
- It fits an aggregate: `Order` owns its `OrderLine`s.
- `orphanRemoval = true` deletes a child when it is removed from the parent's collection.
- Do not cascade to entities with their own lifecycle: `Order` must not cascade to `Product` or `Customer`.
- `CascadeType.ALL` everywhere can delete shared data by accident.

**Show**
```java
order.removeLine(line);   // removed from the list
// at flush: delete from order_line where id = ?
```

**Check:** Should `Order` cascade `REMOVE` to `Product`? *(No; products live on their own.)*

---

## JNR-030-L06 · Unidirectional by default (6 min)
**Goal:** keep relationships as simple as possible.

**Key points**
- A relationship defined on one side only (unidirectional) is simpler and safer.
- Add the second side only when a real use case needs navigation.
- Bidirectional mappings need synchronization code and cause serialization loops (infinite JSON) if returned.
- `OrderLine` -> `Product` is unidirectional: a line knows its product, a product does not list its lines.
- To find "all lines of a product", use a query instead.

**Show:** a diagram with arrows only in one direction: `OrderLine → Product`, `Order → OrderLine` (with `mappedBy` back-reference).

**Check:** Does `Product` need a `List<OrderLine>`? *(No; use a repository query when needed.)*

---

## JNR-030-L07 · Demo: mapping Order and OrderLine as an aggregate (12 min)
**Goal:** map the order aggregate; prepares JNR-030-LAB1.

**Steps**
1. Create `Order` (id, customer, status, createdAt) and `OrderLine` (id, product, quantity, unitPrice).
2. Add `@ManyToOne(LAZY)` from `Order` to `Customer` and from `OrderLine` to `Product`.
3. Add `lines` with `cascade = ALL, orphanRemoval = true` and the `addLine`/`removeLine` helpers.
4. **Planned mistake:** add a line to the list without setting `line.setOrder(this)`; show the null foreign key error and fix it with the helper.
5. Save an order and read the SQL log: one order insert, then one insert per line.

---

## JNR-030-L08 · Demo: cascade and orphan-removal surprises (12 min)
**Goal:** see what cascades and orphan removal really do; prepares JNR-030-LAB1.

**Steps**
1. Remove one line from the order's list and commit; the log shows a `delete` for that line only.
2. Replace the whole list with `order.setLines(newList)` and show the orphan-removal error ("collection was no longer referenced") and why to mutate the same collection.
3. **Planned mistake:** put `CascadeType.ALL` on `OrderLine.product`; delete an order and watch it try to delete a product used elsewhere (constraint error).
4. Remove the cascade and show the order deletes alone.
5. Summarize: cascade only parent-to-owned-children.
