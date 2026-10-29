# ARC-023 · Data architecture — Lecture scripts

**Video:** 68 min · **Running case:** *Larkspur Retail* — a mid-size retailer with 120 stores and a dated on-premises web shop; you are the solution architect for a new platform integrated with the existing ERP and CRM.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## ARC-023-L01 · Data architecture for solution architects (10 min)
**Goal:** explain what a solution architect owns in data architecture and what is left to specialists.

**Key points**
- You decide where each data set lives, who owns it, how it moves, and how long it stays; a data engineer decides how to tune the pipeline.
- Every data set needs one system of record: the one place whose version wins in a dispute.
- Data architecture is a view of the pack, next to the context, container, and deployment views.
- Decisions here outlive the application: reports and audits read today's data for years.

**Show:** a table of Larkspur data sets (customers, products, prices, stock, orders, payments, returns) with empty columns "system of record", "consumers", "retention" to be filled during the module.

**Check:** What is a system of record? *(The single system whose copy of a data set is authoritative when copies disagree.)*

---

## ARC-023-L02 · Operational vs analytical workloads (12 min)
**Goal:** show why transaction processing and reporting need different stores.

**Key points**
- Operational (OLTP): many small reads and writes, milliseconds, current state; a till sale must never wait.
- Analytical (OLAP): few huge scans and aggregations over history; a quarterly margin query touches millions of rows.
- Running both on one database lets a report slow down checkout and a schema change break the report.
- The bridge is a copy: replicas, change capture, or pipelines feed a separate analytical store.

**Show:** a two-column table, OLTP vs OLAP, with rows for access pattern, data shape, freshness, users, typical store, and a Larkspur example in each (basket write vs "margin by region by week").

**Check:** Why not point the board dashboard at the order database? *(Heavy scans compete with checkout, and report needs shape the schema badly; use a separate analytical copy.)*

---

## ARC-023-L03 · Warehouses, lakes, and lakehouses (12 min)
**Goal:** pick between warehouse, lake, and lakehouse for a reporting need.

**Key points**
- Warehouse: modeled, cleaned, structured data with fast SQL; best for finance and KPI reporting.
- Lake: cheap storage of raw files of any shape; best for exploration, logs, and data science; quality is up to you.
- Lakehouse: lake storage with table features (transactions, schema) so one copy serves both; newer, so check team skills.
- Choose from the questions asked, the data shapes, and the team, not from fashion.

**Show:** a decision table with Larkspur needs (daily sales report, clickstream analysis, demand-forecast training data) and the chosen store with one-line reasons.

**Check:** Which fits a finance-signed daily sales report best? *(A warehouse, because it needs modeled, reconciled, consistent data.)*

---

## ARC-023-L04 · The data lifecycle (10 min)
**Goal:** describe the five lifecycle stages and set rules for each data set.

**Key points**
- Stages: creation, use, sharing, archiving, deletion.
- Each stage has rules: who may write, who may read, where copies go, when it moves to cheap storage, when it is destroyed.
- Deletion is the stage teams forget; copies in backups, analytics, and partner systems must be counted.
- Retention comes from law, contract, and business need; record the source of each rule.

**Show:** a lifecycle table for "online order" and "customer profile": retention at each stage, copies that exist, and the deletion trigger.

**Check:** Why list copies in the lifecycle table? *(Deletion and sharing rules only work if every copy is known.)*

---

## ARC-023-L05 · Conceptual models and data-flow views (10 min)
**Goal:** produce a conceptual data model and a data-flow view readable by business and IT.

**Key points**
- Conceptual model: the business things (Customer, Order, Product, Shipment) and how they relate, with no tables or types.
- Data-flow view: boxes for systems, arrows for data moving, labeled with data set and trigger.
- Mark the system of record on each entity; arrows into a non-record system are copies.
- Keep one page each; detail belongs in the data dictionary.

**Show:** a sketch: Customer 1-many Order, Order 1-many OrderLine many-1 Product, Order 1-many Payment; beside it a flow from stores and web to platform, ERP, and warehouse.

**Check:** What distinguishes a conceptual from a physical model? *(The conceptual model shows business entities and relations without tables, columns, or technology.)*

---

## ARC-023-L06 · Demo: Larkspur's data landscape from sales floor to board report (14 min)
**Goal:** work through the full data architecture for Larkspur as a design session; prepares ARC-023-LAB1.

**Steps**
1. List the data sets from interviews: customers, products, prices, stock, orders, payments, returns, loyalty points.
2. Assign a system of record to each: ERP for products, prices, and financials; CRM for marketing profile; platform for web and mobile orders; payment provider for card data.
3. Draw the flow from 120 stores and the web shop into the platform, ERP, and a warehouse, and mark which arrows are copies.
4. **Planned mistake:** point the board dashboard at the platform database "because it is quick". Fix: show checkout latency during a heavy query and move reporting to the warehouse fed by change capture.
5. Fill the lifecycle table with retention per data set and a deletion trigger, including the warehouse and backup copies.
6. Present the one-page data architecture view and note two decisions it already drives (warehouse choice, deletion plan).
