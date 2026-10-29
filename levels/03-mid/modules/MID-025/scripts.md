# MID-025 · Service boundaries — Lecture scripts

**Video:** 62 min · **Analogy used throughout:** departments in a company: each has its own vocabulary, its own files, and a front desk for requests.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-025-L01 · Bounded contexts (12 min)
**Goal:** find boundaries from language and ownership.

**Key points**
- A bounded context is the area where one model and one language are consistent.
- Find it by listening: where words change meaning, or where teams and experts differ.
- The database schema is a poor guide; tables reflect past decisions, not the business.
- A context map shows how contexts relate: upstream/downstream, customer/supplier, anti-corruption layer.
- A service often matches one context; a context may also stay a module in a monolith.

**Show:** a context map of Shop: Catalog, Ordering, Inventory, Payments, Notifications, with arrows showing who depends on whom.

**Check:** Where do bounded contexts come from, schema or language? *(Language and ownership.)*

---

## MID-025-L02 · One concept, several models (8 min)
**Goal:** accept that the same word has different models per context.

**Key points**
- "Product" in Catalog has description and images; in Inventory it is a SKU with a quantity; in Orders it is a name and price snapshot.
- One shared `Product` class for everyone creates coupling and endless changes.
- Each context keeps its own small model and maps at the edge.
- Share identifiers (`productId`), not whole objects.
- An anti-corruption layer translates an external model into your own.

**Show:** three small `Product` classes side by side with their fields.

**Check:** What do contexts share about a product? *(The ID, not the whole model.)*

---

## MID-025-L03 · Data ownership (10 min)
**Goal:** give each service exclusive ownership of its data.

**Key points**
- Each service owns its tables or database; no other service reads or writes them.
- Others get data only through the owner's API or events.
- Shared databases create hidden coupling: a schema change breaks other teams.
- One owner per fact: for example stock levels belong to Inventory, prices to Catalog.
- Separate databases can start as separate schemas; enforce with separate credentials.

**Show:** a table: data item, owning service, how others read it.

**Check:** How may `orders` read stock levels? *(Through inventory's API or events, never its tables.)*

---

## MID-025-L04 · Life without cross-service joins (10 min)
**Goal:** replace joins with three techniques.

**Key points**
- API composition: call each service and combine results in a gateway or backend-for-frontend; fine for small result sets.
- Events and local copies: keep a read-only copy of the fields you need, updated by events; it can be briefly stale.
- Denormalize at write time: store a snapshot, e.g. product name and price in the order line.
- Large reporting joins belong in a separate read model or analytics store.
- Accept that each choice trades freshness, coupling, and cost.

**Show:** order history screen: `orders` stores `productName` and `unitPrice` snapshots, so no call to catalog is needed.

**Check:** Why snapshot price in the order line? *(The price at purchase time must not change, and it avoids a catalog call.)*

---

## MID-025-L05 · Evaluating a boundary (8 min)
**Goal:** test a proposed boundary with questions.

**Key points**
- Do changes usually stay inside one service? Look at change history for co-changing files.
- Does a typical use case need one service or five? Many hops signal a bad cut.
- Can the service work if others are down?
- Is the data owned by exactly one service?
- Is there a team that can own it and a stable API?
- Wrong boundary signs: chatty calls, lockstep releases, shared tables.

**Show:** a checklist table with columns Criterion, Evidence, Pass/Fail.

**Check:** Which sign shows a bad boundary? *(Chatty calls, lockstep releases, or shared tables.)*

---

## MID-025-L06 · Demo: splitting Shop's shared database (14 min)
**Goal:** separate schemas per service. Prepares `MID-025-LAB1`.

**Steps**
1. Map every table to an owner and list queries that cross owners (for example a join of `orders` and `products`).
2. Create separate schemas and database users: `orders`, `inventory`, `payments`.
3. Replace the cross-owner join with a snapshot in `order_lines` and a call to `inventory`'s API for stock.
4. Migrate data and move Flyway migrations into each service.
5. **Planned mistake:** give `orders` read access "just for reporting" on `inventory`'s table. Show how a column rename in inventory breaks it, then revoke and use an event feed instead.
6. Document the context map and data ownership table in the repo.

---
