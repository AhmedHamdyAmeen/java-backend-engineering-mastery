# JNR-037 · Password security — Exercises and lab

## Lab
### JNR-037-LAB1 · Registration
**Outcomes:** 1–4 · **Time:** ~2 h
Implement registration with hashed passwords; throttle after 5 failed logins per account and IP.
**Acceptance:** no plaintext or reversible password anywhere, including logs.

## Exercises (assessment: review a flawed registration flow)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-037-EX01 | 1 | Explain in three sentences why a database stores hashes, not encrypted passwords. |
| JNR-037-EX02 | 1 | Explain what a salt prevents and why MD5 is wrong for passwords. |
| JNR-037-EX03 | 2 | Configure a delegating `PasswordEncoder` bean and encode and match one password in a test. |
| JNR-037-EX04 | 2 | Describe how you would move from bcrypt to Argon2 without forcing a password reset. |
| JNR-037-EX05 | 3 | Write validation for registration: email format, password length 12 to 128, no composition rules. |
| JNR-037-EX06 | 4 | Implement a failed-login counter and write a test that the sixth attempt gets 429. |
| JNR-037-EX07 | 4 | Review a flawed flow (MD5 hashes, "email not found" message, password in logs) and list every flaw. |

## Solutions
- **EX01** Hashes are one-way, so a stolen database does not reveal passwords; encrypted passwords can be decrypted if the key leaks.
- **EX02** A salt makes equal passwords hash differently and defeats precomputed tables. MD5 is fast and broken for this use, so guessing is cheap.
- **EX03** `assertTrue(encoder.matches("pw", encoder.encode("pw")))` and `assertNotEquals(encode("pw"), encode("pw"))`.
- **EX04** Use the delegating encoder with the new default; old `{bcrypt}` hashes still match; re-encode on successful login when `upgradeEncoding` is true.
- **EX05** `@Email`, `@Size(min = 12, max = 128)` on the password; reject known-breached passwords where a list is available (concept).
- **EX06** Keep a map of key (account + IP) to counters and a lock-until time; return 429 after five failures; reset on success.
- **EX07** MD5 is fast; "email not found" leaks which emails exist; password in logs is plaintext exposure. Fix: delegating encoder, generic message, mask logs.
