# JNR-028 · JPA and Hibernate — Lecture scripts

**Video:** 84 min · **Analogy used throughout:** a desk with open folders (the persistence context): what you open and edit on the desk gets filed back when you finish.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## JNR-028-L01 · Mapping an entity (12 min)
**Goal:** turn a class into a table mapping.

**Key points**
- `@Entity` marks a class as persistent; `@Id` marks its primary key.
- JPA needs a no-argument constructor (protected is fine); entities are normal classes, not records.
- `@Table` and `@Column` set names, length, and nullability; they should match the real schema.
- Store enums with `@Enumerated(EnumType.STRING)`, never the default ordinal (numbers break when you reorder).
- Entities model the database, not the API: do not return them from controllers.

**Show**
```java
@Entity
@Table(name = "product")
public class Product {
    @Id @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    @Column(nullable = false, length = 120)
    private String name;
    @Enumerated(EnumType.STRING)
    private ProductStatus status;
    protected Product() {}
}
```

**Check:** Which enum mapping is safe? *(`EnumType.STRING`.)*

---

## JNR-028-L02 · Identifiers and generation strategies (10 min)
**Goal:** choose how ids are created.

**Key points**
- `IDENTITY`: the database fills the id on insert (PostgreSQL identity column); simple, but Hibernate must insert immediately, which disables insert batching.
- `SEQUENCE`: Hibernate asks a sequence for ids, can fetch many at once, and supports batching; usually better for PostgreSQL.
- `UUID` ids can be created in Java before saving.
- The id is `null` until the entity is saved (for generated ids).
- Pick one strategy per project and keep it consistent with the schema.

**Show**
```java
@Id
@GeneratedValue(strategy = GenerationType.SEQUENCE, generator = "product_seq")
@SequenceGenerator(name = "product_seq", sequenceName = "product_seq", allocationSize = 50)
private Long id;
```

**Check:** Which strategy disables insert batching? *(`IDENTITY`.)*

---

## JNR-028-L03 · Embeddables and value objects (8 min)
**Goal:** store a value object in the owner's table.

**Key points**
- A value object has no identity of its own; `Money` is just amount plus currency.
- `@Embeddable` marks the class; `@Embedded` uses it in an entity.
- Its fields become columns of the owner's table (granularity solved).
- Rename columns with `@AttributeOverride` if the same embeddable appears twice.
- Make value objects immutable.

**Show**
```java
@Embeddable
public record Money(
    @Column(name = "price_amount") BigDecimal amount,
    @Column(name = "price_currency", length = 3) String currency) {}

// in Product:
@Embedded private Money price;
```

**Check:** Does an embeddable get its own table? *(No; its columns live in the owner's table.)*

---

## JNR-028-L04 · Entity lifecycle (12 min)
**Goal:** name the four states and the moves between them.

**Key points**
- Transient: new object, not known to JPA.
- Managed: tracked by the persistence context; changes are saved at flush.
- Detached: was managed, but the context closed (usually after the transaction).
- Removed: marked for deletion at flush.
- `persist` makes transient managed; `merge` copies a detached state into a managed instance; `remove` schedules deletion.

**Show:** a diagram: `new` → transient → `persist` → managed → `remove` → removed; managed → context closes → detached → `merge` → managed.

**Check:** Are changes to a detached entity saved automatically? *(No.)*

---

## JNR-028-L05 · Dirty checking and flushing (10 min)
**Goal:** predict when SQL is sent.

**Key points**
- Dirty checking: at flush, Hibernate compares each managed entity with its loaded snapshot and issues `UPDATE` for changes.
- No `save` call is needed for managed entities.
- Flush happens at commit, and before a query that might need pending changes (auto flush), or on `flush()`.
- `IDENTITY` inserts are sent at `persist` time.
- Read-only code should not trigger updates; keep setters purposeful.

**Show**
```java
@Transactional
void rename(Long id, String name) {
    Product p = repo.findById(id).orElseThrow(); // select
    p.setName(name);                             // nothing yet
}                                                // update at commit
```

**Check:** When does the update above run? *(At flush, which happens on commit.)*

---

## JNR-028-L06 · Entity equality (8 min)
**Goal:** write `equals`/`hashCode` that survive the lifecycle.

**Key points**
- Default `equals` compares memory identity; two loads in different transactions are different objects.
- Using all fields (as Lombok `@Data` does) breaks when fields change and can load lazy relations.
- The generated id is `null` before saving, so id-based `hashCode` changes after `persist` if the entity is in a `HashSet`.
- Safe options: a stable business key (such as SKU) or the id-based pattern with a constant `hashCode`.
- Never use `@Data` on entities.

**Show**
```java
@Override public boolean equals(Object o) {
    if (this == o) return true;
    if (!(o instanceof Product other)) return false;
    return id != null && id.equals(other.id);
}
@Override public int hashCode() { return getClass().hashCode(); }
```

**Check:** Why is `@Data` risky on an entity? *(Its `equals`/`hashCode` use all fields, which change and may trigger lazy loading.)*

---

## JNR-028-L07 · Demo: mapping Shop entities and predicting the SQL (12 min)
**Goal:** map `Product`, `Category`, and `Money`, and predict each statement; prepares JNR-028-LAB1.

**Steps**
1. Add `spring-boot-starter-data-jpa` and enable SQL logging (`spring.jpa.show-sql` or the `org.hibernate.SQL` logger); set `ddl-auto=none`.
2. Map `Category` and `Product` with `Money` embedded; match columns to the manual `schema.sql`.
3. Write a create-update-read sequence in a transactional test.
4. Before running, write on screen the SQL you expect for each line.
5. **Planned mistake:** map an enum without `EnumType.STRING`; show the number stored, fix it.
6. Run and compare the log with the predictions.

---

## JNR-028-L08 · Demo: entity states in the debugger (12 min)
**Goal:** observe entity states and flush timing live; prepares JNR-028-LAB1.

**Steps**
1. Put breakpoints in a transactional test around `new`, `persist`, a setter, and the end of the method.
2. Inspect the entity: id `null` while transient; use `entityManager.contains(p)` to show managed.
3. Change a field and show that the SQL log stays silent until `flush()` or commit.
4. **Planned mistake:** modify an entity after the transaction ended (detached); show nothing is saved, then fix with `merge` inside a transaction.
5. Call `remove` and show the `DELETE` is sent at flush.
