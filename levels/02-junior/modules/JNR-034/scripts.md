# JNR-034 · Database constraints — Lecture scripts

**Video:** 50 min · **Analogy used throughout:** a bouncer at the club door: whatever the staff inside forget or race to check, the bouncer still stops duplicates and invalid guests.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## JNR-034-L01 · The database as the last line of defense (8 min)
**Goal:** explain why the database must enforce rules, not just the application.

**Key points**
- Many applications and tools can write to one database: services, scripts, admins.
- Application checks can be skipped, buggy, or out of date.
- Concurrency: two requests pass the same application check at the same time ("check then insert"), then both insert.
- Constraints are enforced by the database for every writer, atomically.
- Keep application validation for friendly messages; keep constraints for guarantees.

**Show:** a timeline of two requests: both `exists(sku)` = false, both insert, two rows; with a unique constraint the second insert fails.

**Check:** Why does "check then insert" fail? *(Two requests can both check before either inserts.)*

---

## JNR-034-L02 · Unique and check constraints (10 min)
**Goal:** write the main constraint types.

**Key points**
- `not null`: the value must exist.
- `unique`: no two rows share the value (or combination).
- `foreign key`: the referenced row must exist; choose the delete behavior on purpose.
- `check`: a rule on the row (`price >= 0`).
- Name constraints (`ux_product_sku`) so error messages and handlers are clear.

**Show**
```sql
alter table product
  add constraint ux_product_sku unique (sku),
  add constraint ck_product_price check (price >= 0);
alter table order_line
  add constraint fk_line_order foreign key (order_id) references orders(id);
```

**Check:** Which constraint stops a negative price? *(A check constraint.)*

---

## JNR-034-L03 · Constraint violations to API errors (8 min)
**Goal:** return meaningful HTTP errors for violations.

**Key points**
- A violation reaches Spring as `DataIntegrityViolationException` (for example `DuplicateKeyException`).
- Duplicates mean 409 Conflict; invalid data means 400 or 422.
- Catch it in one place: a `@RestControllerAdvice` or the service where you can act.
- Read the constraint name from the cause to choose the message (verify the exception path for your driver version).
- Never leak SQL text to the client; use the problem-details format from earlier modules.

**Show**
```java
@ExceptionHandler(DataIntegrityViolationException.class)
ProblemDetail conflict(DataIntegrityViolationException e) {
    return ProblemDetail.forStatusAndDetail(HttpStatus.CONFLICT, "SKU already exists");
}
```

**Check:** Which HTTP status for a duplicate SKU? *(409 Conflict.)*

---

## JNR-034-L04 · Indexes: a first look (14 min)
**Goal:** know what an index is and how to check it is used.

**Key points**
- An index is a sorted lookup structure (usually a B-tree) that makes searches fast, like a book's index.
- It costs disk space and slows writes, so do not index every column.
- PostgreSQL creates indexes for primary keys and unique constraints automatically, but not for foreign keys: index them yourself.
- Index columns used in `where`, `join`, and `order by` for common queries.
- `EXPLAIN` shows the plan: `Seq Scan` reads the whole table, `Index Scan` uses an index; `EXPLAIN ANALYZE` also runs the query and times it.

**Show**
```sql
create index ix_order_line_order_id on order_line(order_id);
explain select * from order_line where order_id = 42;
-- expect: Index Scan using ix_order_line_order_id (on large tables)
```

**Check:** Does PostgreSQL index foreign key columns automatically? *(No.)*

---

## JNR-034-L05 · Demo: racing two requests against a unique constraint (10 min)
**Goal:** prove the application check fails under concurrency and the constraint saves you; prepares JNR-034-LAB1.

**Steps**
1. Implement `createProduct` as `if (!repo.existsBySku(sku)) repo.save(...)` with no constraint.
2. Fire two concurrent requests with the same SKU (two threads released by a `CountDownLatch`).
3. **Planned mistake:** run it and show two rows with the same SKU.
4. Add `V3__unique_sku.sql` (clean the duplicate first), then re-run.
5. Map the violation to 409 in the exception handler.
6. Result: one 201 and one 409, every time.
