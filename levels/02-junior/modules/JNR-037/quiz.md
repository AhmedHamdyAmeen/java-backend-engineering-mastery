# JNR-037 · Password security — Quiz

Outcomes: O1 hashing, salts, slow algorithms · O2 `PasswordEncoder` and upgrades · O3 registration rules · O4 throttling and lockout.

**Q01 (O1)** Passwords should be stored: A. Encrypted with a key B. As plain text C. Hashed with a slow salted algorithm D. Base64-encoded
**Q02 (O1)** A salt is: A. A secret key B. Random per-user data added before hashing C. A hash algorithm D. A password rule
**Q03 (O1)** Why not SHA-256 for passwords? A. It is too slow B. It is too fast for guessing resistance C. It is encrypted D. It has no output
**Q04 (O2)** `PasswordEncoder.matches(raw, stored)`: A. Decrypts the stored value B. Hashes raw and compares C. Returns the password D. Deletes the hash
**Q05 (O2)** The `{bcrypt}` prefix in a delegating encoder allows: A. Faster logins B. Changing algorithms later C. Plain text storage D. No salt
**Q06 (O3)** A sensible password rule is: A. Must contain a symbol, max length 8 B. Length first (for example 12 or more) C. Change every week D. No rules at all
**Q07 (O3)** On failed login, the message should be: A. "No such email" B. "Wrong password" C. "Invalid email or password" D. The stack trace
**Q08 (O4)** A permanent lockout after 5 failures risks: A. Faster logins B. Attackers locking out real users C. Weaker hashes D. Larger tokens
**Q09 (O4)** A good status for too many attempts is: A. 200 B. 404 C. 429 D. 201
**Q10 (O4)** Throttling is best keyed by: A. Account only B. IP only C. Account and IP D. Browser color

## Answers
Q01 C · Q02 B · Q03 B · Q04 B · Q05 B · Q06 B · Q07 C · Q08 B · Q09 C · Q10 C

## Practical part
Seven exercises `JNR-037-EX01` to `EX07` plus the lab; the flawed-flow review is the assessment. Pass: at least six exercises correct, all flaws in EX07 found, and no plaintext password in the database or logs.
