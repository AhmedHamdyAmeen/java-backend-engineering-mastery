# MID-054 · Secrets and cryptography — Lecture scripts

**Video:** 62 min · **Analogy used throughout:** a building with master keys: locks are public knowledge, keys are guarded, and nobody copies the master key into every room. Running project: Shop.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-054-L01 · Cryptography for engineers (12 min)
**Goal:** pick the right primitive for each job and never invent your own.

**Key points**
- Hashing: one-way fingerprint; passwords use a slow salted hash (Argon2, bcrypt, scrypt), not plain SHA.
- Symmetric encryption: one shared key, fast (AES-GCM); gives confidentiality and integrity.
- Asymmetric: key pair; used for key exchange and signatures (RSA, ECDSA, Ed25519).
- Signatures prove who produced data and that it was not changed (for example JWTs).
- Use vetted libraries and modes; never write your own algorithm; never reuse a nonce or IV.

**Show:** table: job → primitive (store password, encrypt a column, sign a token, verify a download).

**Check:** Which is right for storing passwords? *(A slow salted password hash such as Argon2 or bcrypt.)*

---

## MID-054-L02 · TLS in practice (10 min)
**Goal:** configure TLS correctly everywhere data crosses a network.

**Key points**
- TLS gives encryption, server identity, and optionally client identity (mutual TLS, mTLS).
- Certificates are issued by a CA and expire; automate renewal (for example cert-manager or a cloud service).
- Encrypt service-to-service traffic and database connections too, with verification of the server certificate (`sslmode=verify-full` for PostgreSQL).
- Never disable certificate validation to "make it work"; fix the trust store instead.
- Use current TLS versions; verify the recommended minimum before recording.

**Show:** JDBC URL `jdbc:postgresql://db:5432/shop?sslmode=verify-full&sslrootcert=/certs/ca.pem`.

**Check:** What is wrong with a client that trusts every certificate? *(Anyone can impersonate the server.)*

---

## MID-054-L03 · Encryption at rest (8 min)
**Goal:** protect stored data at the right layer.

**Key points**
- Layers: disk or volume encryption (provider default), database encryption, application-level (column) encryption.
- Disk encryption protects lost disks, not a compromised application or SQL user.
- Encrypt sensitive fields (phone numbers, national IDs) in the application when the database admin must not read them.
- Trade-off: encrypted columns cannot be searched or sorted directly; use deterministic encryption or a blind index only when needed.

**Show:** `customers.phone_enc` stored as ciphertext with a key ID; searching by hashed `phone_idx` (blind index).

**Check:** What does disk encryption not protect against? *(A compromised application or database account that reads data normally.)*

---

## MID-054-L04 · Key management and envelope encryption (10 min)
**Goal:** manage keys without ever handling the master key.

**Key points**
- A key management service (KMS) holds master keys; they never leave it.
- Envelope encryption: a data key encrypts the data; the KMS master key encrypts the data key; store the encrypted data key beside the data.
- Benefits: rotate the master key cheaply, audit every decrypt, restrict who may use which key.
- Store a key ID or version with each ciphertext so old data stays readable during rotation.

**Show:** flow: generate data key → encrypt phone with AES-GCM → store ciphertext + encrypted data key + key ID; to read, ask KMS to decrypt the data key.

**Check:** Why encrypt the data key instead of the data directly with the master key? *(Master keys stay in the KMS and rotate cheaply; bulk data is encrypted locally.)*

---

## MID-054-L05 · Secrets managers and rotation (10 min)
**Goal:** keep secrets out of code, images, and Git, and rotate them.

**Key points**
- Secrets: database passwords, API keys, signing keys, certificates.
- Store them in a secrets manager (Vault, AWS Secrets Manager, Azure Key Vault) with access by workload identity, not shared passwords.
- Apps fetch secrets at start or on refresh; avoid long-lived static credentials; prefer dynamic short-lived credentials.
- Rotate regularly and after any suspicion; design for two valid credentials during rotation.
- Environment variables leak into dumps and logs; mounted files or direct API fetch are safer.

**Show:** a pod identity reading `shop/orders/db` from the secrets manager; a secret scanner (such as gitleaks) in CI.

**Check:** Why avoid secrets in environment variables? *(They show up in dumps, process listings, and debug output.)*

---

## MID-054-L06 · Demo: rotating a database password without downtime (12 min)
**Goal:** rotate the `orders` database credential while traffic runs. Prepares MID-054-LAB1.

**Steps**
1. Show the current setup: the password is stored in the secrets manager and read by `orders` via workload identity.
2. Create a second database user (or a second password) so two credentials are valid at once.
3. Update the secret; let `orders` pick up the new value and rebuild its connection pool.
4. **Planned mistake:** change the database password first, before the app has the new one; connections fail. Fix: add the new credential, switch the app, then revoke the old one.
5. Confirm no failed requests in the dashboard and run a scan showing no secret in the image, manifests, or Git.

**Check:** What is the safe order of a rotation? *(Add new credential, switch the app, revoke the old.)*
