# JNR-037 · Password security — Lecture scripts

**Video:** 45 min · **Analogy used throughout:** a meat grinder: you can turn steak into mince, but never mince back into steak.
Format: **Goal** · **Key points** · **Show** · **Check**.

Note: verify version and recommended algorithm settings (bcrypt cost, Argon2 parameters) before recording.

---

## JNR-037-L01 · How passwords get stolen (8 min)
**Goal:** know the common ways passwords are lost, so the controls make sense.

**Key points**
- Database leak: attackers copy the user table and try to crack hashes offline.
- Guessing: brute force against the login endpoint.
- Credential stuffing: trying passwords leaked from other sites, because people reuse them.
- Phishing and malware steal passwords outside your system; you limit damage, not prevent it.
- Logs, backups, and error messages can leak passwords by accident.

**Show:** a table: attack / where it happens / main defense.

**Check:** Why does a leak at another website threaten your Shop? *(People reuse passwords, so attackers try them on Shop.)*

---

## JNR-037-L02 · Hashing, salting, and slow hashes (10 min)
**Goal:** explain why passwords are hashed, salted, and hashed slowly.

**Key points**
- Encryption can be reversed with a key. Hashing is one-way; you store the hash, never the password.
- To log in, hash the attempt and compare.
- A salt is random data added per user, so equal passwords get different hashes and precomputed tables fail.
- Fast hashes (MD5, SHA-256) let attackers try billions of guesses per second. Password hashes are deliberately slow and costly: bcrypt, scrypt, Argon2.
- The slowness is tunable (cost factor) and can be raised over time.

**Show:** `bcrypt("secret")` twice gives two different strings, both starting `$2a$` or `$2b$` with the cost embedded.

**Check:** Why is SHA-256 a poor choice for passwords? *(It is too fast, so guessing is cheap.)*

---

## JNR-037-L03 · `PasswordEncoder` and upgrades (7 min)
**Goal:** store and check passwords with Spring's `PasswordEncoder`.

**Key points**
- `PasswordEncoder` has `encode(raw)` and `matches(raw, stored)`.
- Use `BCryptPasswordEncoder` or `Argon2PasswordEncoder`.
- `PasswordEncoderFactories.createDelegatingPasswordEncoder()` stores an id prefix like `{bcrypt}`, so you can change algorithms later.
- `upgradeEncoding` tells you when a stored hash is weaker than the current setting; re-hash on the next successful login.
- Expose the encoder as a `@Bean`; Spring Security picks it up.

**Show**
```java
@Bean
PasswordEncoder passwordEncoder() {
    return PasswordEncoderFactories.createDelegatingPasswordEncoder();
}
```

**Check:** What does the `{bcrypt}` prefix make possible? *(Moving to a new algorithm later while old hashes still work.)*

---

## JNR-037-L04 · Brute force, lockout, and throttling (10 min)
**Goal:** slow down guessing without handing attackers a new weapon.

**Key points**
- Count failed logins per account and per IP; after a limit (for example 5), delay or block for a time.
- Per-account lockout can be abused to lock real users out: a denial-of-service trade-off.
- Prefer temporary lockouts or growing delays over permanent ones.
- Combine with per-IP limits and, later, extra checks like MFA.
- Answer the same way whether the email exists or not: "invalid email or password".
- Password rules: favor length (for example 12 or more) over complex symbols; check against known breached passwords where possible (concept).

**Show:** a state diagram: attempt fails → counter + 1 → at 5, locked for 15 minutes → counter resets after success or timeout.

**Check:** What is the risk of locking an account after 5 failures? *(An attacker can lock out real users on purpose.)*

---

## JNR-037-L05 · Demo: registration with password hashing and throttling (10 min)
**Goal:** build registration and a safe login. Prepares `JNR-037-LAB1`.

**Steps**
1. Add the encoder bean and a `POST /api/auth/register` endpoint with validation (length, email format).
2. Hash the password in the service; store only the hash.
3. Return the same response whether or not the email already exists (or a generic message).
4. Add a simple in-memory throttle: 5 failures per account and IP, then 429 for a period.
5. **Planned mistake:** logging the whole request body, which prints the password. Fix: log only the email and mask or skip bodies.
6. Search logs and database for any plaintext password.
