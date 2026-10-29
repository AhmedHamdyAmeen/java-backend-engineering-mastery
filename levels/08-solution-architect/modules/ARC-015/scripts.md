# ARC-015 · Storage architecture — Lecture scripts

**Video:** 58 min · **Running case:** *Larkspur Retail* — a fictional 120-store retailer replacing its dated on-premises web shop with a web and mobile platform (inventory, payments, fulfillment, customer service, reporting) integrated with the existing ERP and CRM. You are the solution architect.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## ARC-015-L01 · Object, block, and file storage (12 min)
**Goal:** pick the right storage type per use case.

**Key points**
- Object storage: files addressed by key over an HTTP API; huge scale, cheap, ideal for media, documents, logs, backups; not a disk.
- Block storage: raw disks attached to one VM or container; fast, for databases and boot volumes.
- File storage: shared network file systems with folders and permissions; for lift-and-shift apps needing shared files.
- Default to object storage; use block or file only when the workload demands them.
- Durability (not losing data) and availability (reaching data) are different promises.

**Show:** a three-row table: storage type, access method, typical Larkspur use (product images: object; database volume: block; legacy label tool shared folder: file).

**Check:** Which storage type suits millions of product images served via CDN? *(Object storage.)*

---

## ARC-015-L02 · Backups, retention, and immutability (12 min)
**Goal:** design backups that survive mistakes and ransomware.

**Key points**
- Backup is a copy you can restore; replication copies mistakes and ransomware too.
- Retention comes from requirements: legal, business, and recovery needs.
- Immutability (write-once, cannot be deleted for a period) defeats attackers who obtain admin credentials.
- Isolate backups: separate account, separate credentials, ideally another region.
- Untested backups are hopes; schedule restore tests.

**Show:** diagram: production account writes backups to a separate backup account with immutable retention; admins of production cannot delete them.

**Check:** Why keep backups in a separate account? *(Compromised production credentials then cannot delete them.)*

---

## ARC-015-L03 · Lifecycle policies and tiers (10 min)
**Goal:** control cost by moving or deleting data over time.

**Key points**
- Tiers trade price for access speed and fees: hot, infrequent, archive.
- Lifecycle rules move data between tiers or delete it after a set age.
- Retrieval and minimum-storage-duration charges apply to colder tiers; verify before recording.
- Align rules with retention requirements so you never delete what law requires.
- Without rules, storage only grows.

**Show:** a timeline: logs hot 30 days, infrequent to 90 days, archive until seven years, then delete (example; use Larkspur's real requirement).

**Check:** What happens to cost when no lifecycle rules exist? *(Storage grows without limit.)*

---

## ARC-015-L04 · Securing stored data (10 min)
**Goal:** protect stored data with encryption and access controls.

**Key points**
- Encrypt at rest by default; decide who manages keys: provider-managed or customer-managed keys.
- Encrypt in transit with TLS.
- Block public access by default; grant by role with least privilege; use short-lived credentials.
- Log access to sensitive stores and review.
- Classify data so controls match sensitivity.

**Show:** a control checklist per bucket: public access blocked, encryption on, key owner, access roles, logging, versioning, retention.

**Check:** What is the safest default for storage public access? *(Blocked.)*

---

## ARC-015-L05 · Demo: storage design for product media, documents, and backups (14 min)
**Goal:** design storage for four Larkspur data sets and prepare `ARC-015-LAB1`.

**Steps**
1. List data sets: product images, invoices (statutory retention), application logs, database backups.
2. Choose: object storage with CDN for images; object storage with retention lock for invoices; object storage with lifecycle for logs; separate account for backups.
3. Define lifecycle and retention from requirements (invoice years from the finance and legal requirement).
4. **Planned mistake:** backups placed in the production account with the same admin role. Fix: replicate to an isolated backup account with immutable retention.
5. Set encryption, key ownership, and access roles per data set.
6. Write the backup and restore-test schedule.

---
