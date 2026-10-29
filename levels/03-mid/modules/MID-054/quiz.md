# MID-054 · Secrets and cryptography — Quiz

Outcomes: O1 primitives · O2 TLS · O3 secrets managers and rotation · O4 envelope encryption and KMS.

**Q01 (O1)** For storing passwords use: A. SHA-1 B. AES with a shared key C. A slow salted hash such as Argon2 or bcrypt D. Base64
**Q02 (O1)** A digital signature proves: A. Secrecy B. Speed C. Compression D. Who produced the data and that it is unchanged
**Q03 (O1)** Which is a correct approach to algorithms? A. Write your own cipher B. Use vetted libraries and modes C. Reuse the same nonce D. Obscure the algorithm
**Q04 (O2)** Disabling certificate validation: A. Speeds up TLS safely B. Is required for databases C. Allows impersonation of the server D. Improves logging
**Q05 (O2)** `sslmode=verify-full` makes PostgreSQL clients: A. Skip encryption B. Verify the certificate chain and host name C. Use a password D. Log queries
**Q06 (O3)** Safe rotation order is: A. Revoke old, then add new B. Change the database first C. Delete the app D. Add new, switch the app, revoke old
**Q07 (O3)** Which place is worst for a secret? A. A secrets manager B. A Git repository C. A mounted file from a manager D. Workload identity
**Q08 (O3)** Environment variables are risky for secrets because: A. They show up in dumps and debug output B. They are encrypted C. They are slow D. They are read-only
**Q09 (O4)** In envelope encryption the master key: A. Encrypts all data directly B. Is stored beside the data C. Stays in the KMS and encrypts data keys D. Is printed in logs
**Q10 (O4)** Disk encryption does NOT protect against: A. A stolen disk B. A discarded server C. A lost backup tape D. A compromised application reading data normally

## Answers
Q01 C · Q02 D · Q03 B · Q04 C · Q05 B · Q06 D · Q07 B · Q08 A · Q09 C · Q10 D

## Practical part
Quiz plus lab `MID-054-LAB1`. Pass: quiz at least 8/10, no secret in images, manifests, or Git, and a live database credential rotation without failed requests.
