# MID-042 · MongoDB — Exercises and lab

## Lab
### MID-042-LAB1 · Reviews service
**Outcomes:** 1–5 · **Time:** ~2.5 h
Build a reviews service on MongoDB with Spring Data MongoDB: add a review, list the latest 20 for a product, and return a ratings summary (average and count per star) computed by an aggregation. Create indexes for the queries and show their plans with `explain`.
**Acceptance:** indexes match queries; summary computed in the database.

## Exercises (assessment: document-model review)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-042-EX01 | 1 | Decide embed or reference: order items, product reviews, customer address in an order, product category. |
| MID-042-EX02 | 2 | Create the right index for "latest reviews of a product" and show the plan before and after. |
| MID-042-EX03 | 3 | Write a pipeline that returns the count per rating for product 42. |
| MID-042-EX04 | 4 | Give one case that needs a multi-document transaction and one that can be modeled away; state the cost. |
| MID-042-EX05 | 5 | Write a `MongoRepository` with a derived query for the 20 latest reviews of a product. |
| MID-042-EX06 | 1 | Review a given document model of `Product` with an embedded `reviews` array and a table-per-entity layout; list the problems and a fix. |

## Solutions
- **EX01** Order items: embed (owned, bounded). Reviews: reference. Address in order: embed a snapshot. Category: reference id and copy the name.
- **EX02** `createIndex({productId:1, createdAt:-1})`; plan changes from `COLLSCAN` to `IXSCAN` with `totalDocsExamined` close to `nReturned`.
- **EX03** `[{ $match:{productId:42} }, { $group:{ _id:"$rating", count:{$sum:1} } }, { $sort:{_id:-1} }]`.
- **EX04** Needed: move credit between two wallet documents. Modeled away: update an order and its embedded items in one document. Cost: extra latency, retries, locking, replica set required.
- **EX05** `List<Review> findTop20ByProductIdOrderByCreatedAtDesc(long productId);`
- **EX06** Unbounded array (growth, 16 MB, slow updates) and relational copying (many lookups). Fix: separate `reviews` collection plus an embedded small summary; embed data that is read together.

**Outcome 5** is also covered by the lab.
