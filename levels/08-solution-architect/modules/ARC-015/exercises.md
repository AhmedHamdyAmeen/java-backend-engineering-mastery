# ARC-015 · Storage architecture — Exercises and lab

## Lab
### ARC-015-LAB1 · Larkspur storage design
**Outcomes:** 1–4 · **Time:** ~2.5 h
1. Inventory the data sets: product images, invoices, logs, database and file backups.
2. Choose storage type per data set.
3. Define lifecycle rules, retention periods, and backup and restore-test schedule.
4. Define encryption, key ownership, and access roles.
5. Show how backup copies are isolated from production credentials.
**Acceptance:** retention meets requirements; backup copies are isolated from production credentials.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| ARC-015-EX01 | 1 | Choose object, block, or file storage for: product images, the order database volume, a shared folder used by a legacy label printer tool. |
| ARC-015-EX02 | 2 | Ransomware encrypts production and deletes backups in the same account. Redesign the backup path. |
| ARC-015-EX03 | 2 | Define retention for invoices (assume seven years), logs (assume one year), and order exports; state the assumptions. |
| ARC-015-EX04 | 3 | Write lifecycle rules for application logs and estimate qualitatively the cost effect. |
| ARC-015-EX05 | 4 | Review a bucket with public read access and no encryption; list the fixes. |
| ARC-015-EX06 | 4 | Decide provider-managed versus customer-managed keys for invoices and justify. |

## Solutions
- **EX01** Images: object; database volume: block; shared folder: file (or modernize the tool to use object storage).
- **EX02** Copy backups to a separate account with separate credentials, immutable retention, and no delete rights for production roles; test restore from that copy.
- **EX03** Invoices: seven years with retention lock; logs: one year with tiering; exports: shortest period required by finance. State that legal confirms the numbers.
- **EX04** Hot for 30 days, infrequent access for 90, archive to the retention end, delete afterwards; storage cost falls because most data sits in cheaper tiers; verify retrieval fees before recording.
- **EX05** Block public access, serve via CDN with controlled access if needed, enable encryption and versioning, restrict roles, enable access logging.
- **EX06** Customer-managed keys for invoices when audit demands key control and revocation; accept the added operating work; provider-managed is fine for non-sensitive media.

**Workplace evidence:** a storage or backup design you implemented.

---
Outcome coverage: all outcomes covered by exercises and the lab.
