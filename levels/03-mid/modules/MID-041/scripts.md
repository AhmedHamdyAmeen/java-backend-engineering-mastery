# MID-041 · NoSQL fundamentals — Lecture scripts

**Video:** 54 min · **Analogy used throughout:** different kinds of storage furniture: a locker row, a folder cabinet, a wide ledger, a wall of strings between pins. Each is great at one job. Running project: Shop.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-041-L01 · Why NoSQL exists (8 min)
**Goal:** know what problems NoSQL stores were built for, and what they give up.

**Key points**
- "NoSQL" means "not only relational": stores built for a specific access pattern, scale, or data shape.
- Drivers: horizontal scale, huge write rates, flexible shape, very low latency, relationship-heavy data.
- Typical cost: weaker joins, fewer or no multi-row transactions, you design data around queries.
- Relational databases scale a long way; NoSQL is a choice made from evidence (MID-044), not default.

**Show:** a four-quadrant diagram: key-value, document, wide-column, graph, each with one product and one Shop use case.

**Check:** Name one thing you often give up with NoSQL. *(Ad hoc queries/joins or multi-row transactions.)*

---

## MID-041-L02 · Key-value and document stores (10 min)
**Goal:** describe the two most common models.

**Key points**
- Key-value (Redis, DynamoDB basics): fetch by key; very fast; no query by value unless you build an index.
- Document (MongoDB): JSON-like documents with nested data and flexible fields; indexes on fields; query inside the document.
- Document fits data read as a unit: a review with its comments, a product with attributes.
- Consistency: single-document writes are atomic; cross-document needs transactions or design around them.

**Show**
```json
{ "_id": "r1", "productId": 42, "rating": 5, "text": "Great", "tags": ["fast"] }
```
Lookup by `_id` is O(1) in a key-value store; querying by `productId` needs an index in a document store.

**Check:** What is a document store good at? *(Reading and writing a nested object as one unit.)*

---

## MID-041-L03 · Wide-column stores (8 min)
**Goal:** understand tables designed for huge write volume and known queries.

**Key points**
- Cassandra, ScyllaDB, HBase: rows are found by a partition key, ordered inside the partition by clustering columns.
- A table is designed for one query; the same data is duplicated into several tables for several queries.
- Writes are very fast and scale out; queries without the partition key are not supported or are slow.
- Consistency is tunable per request; many designs favor availability (see CAP and PACELC).

**Show:** table `reviews_by_product(product_id, created_at, review_id, rating)` with partition key `product_id` and clustering `created_at DESC`: "latest reviews of a product" is one partition read.

**Check:** Why duplicate data in wide-column? *(Each query needs its own table with the right partition key.)*

---

## MID-041-L04 · Graph databases (8 min)
**Goal:** recognise relationship-heavy problems.

**Key points**
- Data is nodes and edges with properties (Neo4j, query language Cypher).
- Strong when queries traverse many hops: recommendations, fraud rings, social graphs.
- The same question in SQL needs many joins that get slower with depth.
- Weak for bulk analytics and simple key lookups; scaling out is harder than for key-value stores.

**Show:** `(Customer)-[:BOUGHT]->(Product)<-[:BOUGHT]-(Other)-[:BOUGHT]->(Rec)`: "customers who bought this also bought".

**Check:** When does a graph store beat SQL? *(Deep multi-hop relationship queries.)*

---

## MID-041-L05 · Modeling for queries (8 min)
**Goal:** design data from the questions, and relate it to CAP and PACELC.

**Key points**
- Relational: model the facts, normalize, query anything later. NoSQL: list the queries first, shape the data for them.
- Trade-off: speed and scale for known queries versus flexibility for unknown ones.
- "Schemaless" does not mean no schema: the schema lives in your code, and migrations are your job.
- CAP: during a network partition choose consistency or availability. PACELC: else (no partition), choose latency or consistency. Verify each product's actual defaults before claiming them.

**Show:** query list for reviews: (1) latest 20 for a product, (2) average rating per product, (3) all reviews by a customer; each mapped to a structure.

**Check:** What does "schemaless" really mean? *(The database does not enforce the schema; your application must.)*

---

## MID-041-L06 · Demo: the same data in four models (12 min)
**Goal:** model Shop reviews four ways and compare the queries each supports. Prepares MID-041-LAB1.

**Steps**
1. Relational: tables `review`, `product`, `customer`; show the join for "latest 20 with customer name".
2. Document: one review per document, with the customer name copied in; show a find by `productId` sorted by date.
3. Wide-column: `reviews_by_product` and `reviews_by_customer` tables; show the duplicated writes.
4. Graph: `(Customer)-[:WROTE]->(Review)-[:ABOUT]->(Product)`; show a "similar reviewers" traversal.
5. **Planned mistake:** copy the relational schema into the document store with references everywhere; every read needs several lookups. Fix: embed what is read together (customer display name, rating).
6. Fill the comparison table of queries each model supports well.

**Check:** Which model best answers "latest reviews of a product" at huge write volume? *(Wide-column, partitioned by product.)*
