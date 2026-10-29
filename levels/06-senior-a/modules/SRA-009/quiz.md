# SRA-009 · Security and compliance — Quiz

Outcomes: O1 privacy by design · O2 auditability · O3 regulation to requirements · O4 reducing compliance scope.

**Q01 (O1)** Data minimization means: A. Compress data B. Keep data forever C. Collect and keep only what a stated purpose needs D. Copy data to many places
**Q02 (O1)** A deletion that removes data only from primary databases is: A. Complete B. Incomplete because derived stores and backups remain C. Required D. Faster and sufficient
**Q03 (O1)** Purpose limitation requires: A. Using data for any new idea B. No logging C. Selling data D. Using data only for its declared purpose, enforced in design
**Q04 (O2)** A good audit log is: A. Append-only and protected from those being audited B. Editable by admins C. Stored in each team's own wiki D. Optional
**Q05 (O2)** Audit trails should cover: A. Only logins B. Only database queries C. Access and also changes through deployment and configuration D. Nothing
**Q06 (O3)** An unclear regulatory interpretation should be: A. Ignored B. Guessed C. Hidden D. Recorded as an open item and resolved with compliance
**Q07 (O3)** A requirement derived from regulation needs: A. A slogan B. An owner, a control, and a test or evidence source C. A new team D. A long document
**Q08 (O3)** Who defines legal obligations? A. Compliance and legal partners B. The newest engineer C. The load balancer D. The cloud vendor only
**Q09 (O4)** Tokenization reduces scope because: A. It encrypts the network B. It deletes logs C. Most systems handle tokens instead of sensitive data D. It speeds queries
**Q10 (O4)** After claiming scope reduction you should: A. Stop B. Scan stores, logs, and exports for remaining sensitive data and add detection C. Delete the tokens D. Add services

## Answers
Q01 C · Q02 B · Q03 D · Q04 A · Q05 C · Q06 D · Q07 B · Q08 A · Q09 C · Q10 B

## Practical part
Six case exercises `SRA-009-EX01` to `EX06` plus the lab, reviewed as a compliance architecture with a role-played compliance officer. Pass: at least five of six exercises correct, quiz at least 8/10, and an architecture covering privacy, audit, scope reduction, and erasure across services.
