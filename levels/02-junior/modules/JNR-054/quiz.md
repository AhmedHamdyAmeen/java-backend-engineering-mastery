# JNR-054 · Troubleshooting — Quiz

Outcomes: O1 reproduce · O2 logs and stack traces · O3 environment differences · O4 bug report and regression test.

**Q01 (O1)** What comes first when troubleshooting? A. Reproduce the problem B. Rewrite the module C. Restart everything D. Blame a teammate
**Q02 (O1)** Why change one thing at a time? A. To look busy B. To know which change had the effect C. To save typing D. It is faster to guess
**Q03 (O2)** In a stack trace, the root cause is usually: A. The first line B. The class name C. The last "Caused by" D. The timestamp
**Q04 (O2)** A correlation (request) id helps to: A. Encrypt logs B. Delete logs C. Speed up the JVM D. Follow one request through the logs
**Q05 (O2)** Which should never be logged? A. Request ids B. Passwords and secrets C. Order numbers D. Timestamps
**Q06 (O3)** "Works on my machine" is often caused by differences in: A. Keyboard B. Wallpaper C. Config, data, or versions D. Font size
**Q07 (O3)** To check what is really running in production, verify: A. The image tag and commit B. The README C. Your local branch D. The issue title
**Q08 (O4)** The regression test should be written: A. Never B. After release C. Without assertions D. Before the fix, so it fails first
**Q09 (O4)** A good bug report includes: A. Symptom, root cause, fix, regression test B. Only the symptom C. Only the fix D. Only the author
**Q10 (O4)** A good help request includes: A. "It doesn't work." B. A screenshot only C. Expected result, actual result, and what you tried D. Nothing but a link

## Answers
Q01 A · Q02 B · Q03 C · Q04 D · Q05 B · Q06 C · Q07 A · Q08 D · Q09 A · Q10 C

## Practical part
Seven exercises `JNR-054-EX01` to `EX07` plus the lab; assessed in a live troubleshooting session. Pass: quiz 8/10, at least five exercises correct, and root cause, fix, and regression test for each of the three lab faults.
