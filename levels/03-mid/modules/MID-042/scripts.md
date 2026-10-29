# MID-042 · MongoDB — Lecture scripts

**Video:** 68 min · **Analogy used throughout:** a folder cabinet where each folder holds everything about one thing, and you decide what goes inside the folder or in a separate one. Running project: Shop.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-042-L01 · Documents and collections (8 min)
**Goal:** know the MongoDB data model and basic operations.

**Key points**
- A document is BSON (binary JSON) with an `_id`; documents live in collections; collections live in databases.
- Documents in one collection may differ in shape, but design a consistent shape and validate it (JSON Schema validation).
- Basic operations: `insertOne`, `find`, `updateOne` with `$set`, `deleteOne`.
- Maximum document size is 16 MB (verify before recording); unbounded growth is a design smell.

**Show**
```js
db.reviews.insertOne({ productId: 42, customerId: 7, rating: 5, text: "Great", createdAt: new Date() })
db.reviews.find({ productId: 42 }).sort({ createdAt: -1 }).limit(20)
```

**Check:** What is a collection? *(A group of documents, like a table without a fixed schema.)*

---

## MID-042-L02 · Embedding vs referencing (12 min)
**Goal:** decide where related data lives, based on access patterns.

**Key points**
- Embed when data is read together, is owned by the parent, and stays bounded (an address inside an order).
- Reference when data is shared, large, changes on its own, or grows without limit (all reviews of a product).
- An unbounded array inside a document (reviews inside a product) is the classic mistake: documents grow, updates slow down, 16 MB limit.
- Copy small, stable fields (customer display name) into the document to avoid lookups; accept update cost.
- Do not copy a relational schema table by table.

**Show:** two options for reviews: embedded array in `product` (bad: unbounded) versus a `reviews` collection with `productId` (good), plus an embedded `ratingSummary` in `product` (small and bounded).

**Check:** Why not embed all reviews in the product document? *(The array is unbounded: the document grows and every update is costly.)*

---

## MID-042-L03 · Indexes and explain (10 min)
**Goal:** create indexes and read query plans.

**Key points**
- Without an index MongoDB does a collection scan (`COLLSCAN`). With one it does an index scan (`IXSCAN`).
- Compound index order follows equality, sort, range (ESR rule): `{ productId: 1, createdAt: -1 }`.
- Check plans with `explain("executionStats")`: compare `totalDocsExamined` with `nReturned`.
- Each index costs write time and memory; build only those queries need. TTL and unique indexes also exist.

**Show**
```js
db.reviews.createIndex({ productId: 1, createdAt: -1 })
db.reviews.find({ productId: 42 }).sort({ createdAt: -1 }).explain("executionStats")
```
Look for `IXSCAN` and `totalDocsExamined` close to `nReturned`.

**Check:** What does `COLLSCAN` in a plan tell you? *(No usable index; every document was read.)*

---

## MID-042-L04 · Aggregation pipelines (12 min)
**Goal:** compute summaries in the database.

**Key points**
- A pipeline is a list of stages; each passes documents to the next: `$match`, `$group`, `$sort`, `$project`, `$lookup`.
- Put `$match` first so it can use an index and shrink the data.
- `$group` with `$avg` and `$sum` computes counts and averages.
- Do the work in the database instead of loading documents into Java.
- `$lookup` is a join; use sparingly, it is not a relational join engine.

**Show**
```js
db.reviews.aggregate([
  { $match: { productId: 42 } },
  { $group: { _id: "$rating", count: { $sum: 1 } } },
  { $sort: { _id: -1 } }
])
```

**Check:** Why put `$match` first? *(It uses an index and reduces the documents later stages process.)*

---

## MID-042-L05 · Transactions (6 min)
**Goal:** know when multi-document transactions are needed and what they cost.

**Key points**
- Single-document updates are atomic; good modeling often removes the need for transactions.
- Multi-document transactions exist (need a replica set or sharded cluster; verify version support).
- Cost: more latency, more locking and memory, short time limits, retries on transient errors.
- Use them for real cross-document invariants (move a value between two documents), not as a habit.

**Show:** Spring `@Transactional` with a `MongoTransactionManager` bean, and a note that it fails on a standalone server.

**Check:** When is a transaction not needed? *(When the change fits in one document, since that write is atomic.)*

---

## MID-042-L06 · Spring Data MongoDB (8 min)
**Goal:** use MongoDB from Spring.

**Key points**
- `spring-boot-starter-data-mongodb`; connection in `spring.data.mongodb.uri`.
- `@Document` classes and `MongoRepository<Review, String>` give CRUD and derived queries.
- `@Indexed` and `@CompoundIndex` declare indexes; check that they really exist in production.
- Complex summaries use `MongoTemplate` with an `Aggregation`, or `@Aggregation` on a repository.

**Show**
```java
@Document("reviews")
record Review(@Id String id, long productId, int rating, String text, Instant createdAt) {}
interface ReviewRepo extends MongoRepository<Review, String> {
    List<Review> findTop20ByProductIdOrderByCreatedAtDesc(long productId);
}
```

**Check:** Where do you put a pipeline with `$group`? *(In `MongoTemplate` aggregation or `@Aggregation`.)*

---

## MID-042-L07 · Demo: building the reviews service on MongoDB (12 min)
**Goal:** build the reviews service with a ratings summary. Prepares MID-042-LAB1.

**Steps**
1. Create the `Review` document and repository; add `POST /products/{id}/reviews` and `GET` for the latest 20.
2. Add the compound index `{ productId: 1, createdAt: -1 }` and prove `IXSCAN` with `explain`.
3. Add `GET /products/{id}/rating-summary` using an aggregation (`$match`, `$group` average and count).
4. Run it against 100 000 seeded reviews; compare timings with and without the index.
5. **Planned mistake:** embed the review list inside a `ProductReviews` document; at a few thousand reviews updates slow down. Fix: one document per review and a separate summary.
6. Use Testcontainers with a MongoDB image for the integration test (verify image tag).

**Check:** Where is the average computed? *(In the database, by the aggregation pipeline.)*
