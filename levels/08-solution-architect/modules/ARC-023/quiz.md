# ARC-023 · Data architecture — Quiz

Outcomes: O1 operational vs analytical · O2 data lifecycle · O3 warehouse, lake, lakehouse · O4 conceptual model and data flow.

**Q01 (O1)** A weekly margin report scans three years of orders and slows the web shop. The best fix is: A. Add more web servers B. Ask users not to run reports C. Delete old orders D. Feed a separate analytical store and report from it
**Q02 (O1)** Which workload pattern is typical of OLTP? A. Many small reads and writes B. Few huge scans C. Batch-only writes D. Read-only history
**Q03 (O2)** Which lifecycle stage do teams most often forget? A. Creation B. Use C. Deletion D. Sharing
**Q04 (O2)** Why record all copies of a data set? A. For prettier diagrams B. To increase storage C. Because deletion and sharing rules need every copy known D. To skip retention
**Q05 (O3)** Which store best fits finance-signed KPI reporting with modeled, reconciled data? A. Raw lake B. File share C. Message broker D. Warehouse
**Q06 (O3)** What does a lakehouse add to a lake? A. A message queue B. Table features such as transactions and schemas over lake storage C. A CRM D. Lower security needs
**Q07 (O4)** A conceptual data model shows: A. Column types B. Indexes C. Business entities and relationships D. Partitions
**Q08 (O4)** On a data-flow view, an arrow into a system that is not the system of record represents: A. A copy B. The master write C. A deletion D. A backup only
**Q09 (O1)** Your data architecture review finds reporting running on the production database. Which common mistake is this? A. Over-normalization B. Too many owners C. Missing tests D. Reporting directly off production databases
**Q10 (O2)** Where should the retention period for a data set come from? A. The developer's guess B. Disk size C. The newest team member D. Law, contract, and business need, with the source recorded

## Answers
Q01 D · Q02 A · Q03 C · Q04 C · Q05 D · Q06 B · Q07 C · Q08 A · Q09 D · Q10 D

## Practical part
Data architecture review of the Larkspur lab: the reviewer checks one system of record and a defined retention for every data set. Pass: quiz at least 8/10, at least five of six exercises correct, and a lab with no data set missing an owner or retention.
