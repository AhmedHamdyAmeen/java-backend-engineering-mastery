# ARC-029 · Privacy and compliance — Lecture scripts

**Video:** 74 min · **Running case:** *Larkspur Retail* — a fictional 120-store retailer replacing its dated on-premises web shop with a web and mobile platform (inventory, payments, fulfillment, customer service, reporting) integrated with the existing ERP and CRM. You are the solution architect.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## ARC-029-L01 · Data classification (10 min)
**Goal:** classify data and attach handling rules to each class.

**Key points**
- Classes for Larkspur: public, internal, confidential, personal, payment.
- Each class gets rules: who may access, where it may be stored, encryption, whether it may leave the platform, whether it may appear in logs or analytics.
- Classify per data set and per field; one order record holds several classes.
- Rules that are not enforced by architecture (tagging, masking, access policy) are only wishes.

**Show:** a table: data set, class, system of record, allowed copies, masking rule. Example: customer email = personal; card token = payment-related, no card number anywhere.

**Check:** Why classify at field level? *(One record mixes classes; the email needs different handling from the order total.)*

---

## ARC-029-L02 · Retention and deletion (10 min)
**Goal:** design retention and deletion that actually reaches every copy.

**Key points**
- Each data set has a retention period driven by law, finance, and business need (get the periods from legal; do not invent them).
- Deletion must reach primary stores, search indexes, caches, analytics copies, exports, and backups.
- Backups: expire on schedule or use a documented "beyond use" approach agreed with legal; verify with the data protection officer.
- Prefer deleting or anonymizing automatically by a scheduled, logged job.

**Show:** a lifecycle table for order data: kept 7 years for finance (verify with legal), personal fields anonymized after that, backups expire after 35 days.

**Check:** Where do deletion designs usually fail? *(Backups and analytics copies that nobody listed.)*

---

## ARC-029-L03 · Data-subject rights across many systems (10 min)
**Goal:** handle access, correction, and erasure requests across platform, ERP, and CRM.

**Key points**
- Rights include access, correction, and erasure (the exact set and deadlines depend on the law; verify with legal).
- You need a data map: where one person's data lives and which system is the master.
- Design one request workflow that fans out to every system and collects confirmations.
- Some data must stay (tax records); erasure becomes restriction or anonymization with a recorded reason.

**Show:** a flow: request → identity check → lookup by customer ID across systems → fan-out tasks → confirmation → response and audit record.

**Check:** A customer asks for erasure but an invoice must be kept for tax. What happens? *(Keep the legally required record, minimize and restrict it, erase the rest, and tell the customer.)*

---

## ARC-029-L04 · Residency and cross-border transfers (8 min)
**Goal:** reflect residency and transfer rules in the architecture.

**Key points**
- Ask first: which laws apply to which data, and where may it be stored and processed.
- Residency is about where data lives; transfers are about where it travels, including support access and logs.
- Architectural levers: region selection, regional stores, tokenization before transfer, contractual safeguards.
- Check the SaaS and AI providers' regions and sub-processors (verify before recording).

**Show:** a map of Larkspur's systems with region labels and arrows for flows that cross a border, such as CRM SaaS support access.

**Check:** Is storing data in-region enough? *(No. Remote support access, backups, and analytics flows may still cross borders.)*

---

## ARC-029-L05 · Payment compliance scope (10 min)
**Goal:** reduce PCI DSS scope with tokenization and hosted payment pages.

**Key points**
- PCI DSS applies to systems that store, process, or transmit card data, plus systems connected to them.
- A hosted payment page or fields means card data goes from the customer to the provider, not through Larkspur.
- Tokens let Larkspur keep a reference for refunds and repeat payments without card numbers.
- Fewer systems in scope means less cost, less audit effort, less risk. The exact requirements and version change: verify before recording.

**Show:** two diagrams: card data flowing through the web app (large scope) versus straight from the browser to the provider (small scope).

**Check:** What does Larkspur store after a hosted payment? *(A token, last four digits, and the payment status, never the full card number.)*

---

## ARC-029-L06 · Demo: shrinking Larkspur's PCI DSS scope with a hosted payment page (13 min)
**Goal:** worked scope-reduction session; prepares ARC-029-LAB1.

**Steps**
1. List the current web shop's card flows: form posts to the web server, saved cards in the database, call-center notes with card numbers.
2. Mark every system that touches card data; this is the scope.
3. Redesign: hosted payment fields for web and app; provider-hosted terminal flow for call center; tokens for saved cards.
4. **Planned mistake:** assume the iframe or hosted fields make the whole web app out of scope. Fix: the page that embeds the fields and its scripts still need controls; confirm the scope category with the assessor or acquirer.
5. Confirm no card data reaches logs, analytics, or order notes; add detection (pattern scan of logs).

---

## ARC-029-L07 · Demo: tracing one customer's data for an erasure request (13 min)
**Goal:** run an erasure request end to end across systems; prepares ARC-029-LAB1.

**Steps**
1. Receive the request for customer C-1042; verify identity.
2. Trace C-1042 through the platform database, search index, cache, ERP customer and invoices, CRM profile and cases, email tool, analytics warehouse, backups.
3. Decide per system: delete, anonymize, retain with reason (invoices).
4. **Planned mistake:** delete from the platform only and answer "done". Fix: the fan-out workflow tracks each system, and the analytics copy and CRM marketing list are cleared too.
5. Record the audit entry without storing the customer's personal data, and answer the customer within the legal deadline (verify the deadline with legal).
