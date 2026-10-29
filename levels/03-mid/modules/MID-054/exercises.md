# MID-054 · Secrets and cryptography — Exercises and lab

## Lab
### MID-054-LAB1 · Secrets in Shop
**Outcomes:** 1–4 · **Time:** ~2 h
Move every Shop secret into a secrets manager (Vault or the cloud equivalent), fetched by workload identity. Rotate the database credentials live under load. Encrypt stored customer phone numbers with envelope encryption. Enable TLS to the database with certificate verification. Add a secret scanner to CI.
**Acceptance:** no secret in images, manifests, or Git; live rotation with no failed requests.

## Exercises (assessment: quiz plus lab)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-054-EX01 | 1 | Choose hash, symmetric, asymmetric, or signature for: passwords, a phone column, a JWT, key exchange. |
| MID-054-EX02 | 2 | Write the JDBC URL and explain each part for a verified TLS connection to PostgreSQL. |
| MID-054-EX03 | 2 | A teammate sets `trustAll=true` in a dev client. Explain the risk and the correct fix. |
| MID-054-EX04 | 4 | Describe envelope encryption and how rotating the master key affects stored data. |
| MID-054-EX05 | 3 | Write the rotation steps for a database password with two valid credentials. |
| MID-054-EX06 | 3 | Find a leaked secret in a sample repository history and state the response. |

## Solutions
- **EX01** Passwords: slow salted hash. Phone column: symmetric (AES-GCM) via envelope encryption. JWT: signature (asymmetric or HMAC). Key exchange: asymmetric.
- **EX02** `?sslmode=verify-full&sslrootcert=/certs/ca.pem`: encrypt, verify the certificate chain and host name against the given CA.
- **EX03** Man-in-the-middle exposure; add the CA to the trust store or use the proper dev certificate.
- **EX04** Data key encrypts data, KMS key encrypts the data key; rotating the master key re-wraps data keys only, not the data.
- **EX05** Create credential B, store it, let the app reload, verify, revoke credential A, repeat later in the other direction.
- **EX06** Treat as compromised: rotate the secret first, then remove it from history and add a scanner; deleting the commit alone is not enough.

**Outcome 3** is also covered by lab criterion "live rotation with no failed requests" and quiz Q07–Q09.
