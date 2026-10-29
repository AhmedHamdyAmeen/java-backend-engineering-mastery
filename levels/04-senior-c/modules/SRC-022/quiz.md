# SRC-022 · Operating AI in production — Quiz

Outcomes: O1 versioned configuration · O2 gated and progressive release · O3 drift · O4 bad-output incidents.

**Q01 (O1)** A prompt change in production should be treated as: A. A deployment B. A content edit C. A hotfix with no review D. A database migration only
**Q02 (O1)** Which should be logged with each answer? A. Only the user's name B. Nothing, to save cost C. Only the response time D. Config bundle ID, model version, and retrieved sources
**Q03 (O1)** Pinning the model version mainly: A. Reduces surprise changes B. Improves accuracy always C. Removes need for evals D. Speeds responses
**Q04 (O2)** An evaluation gate: A. Replaces canaries B. Blocks a release when candidate scores fall below criteria C. Only measures latency D. Runs after rollout
**Q05 (O2)** Why use per-category thresholds? A. An average can hide a failing category such as refunds B. Averages are illegal C. They are faster D. They remove safety tests
**Q06 (O3)** Quality drift can occur when: A. Nothing at all can change B. Only code is edited C. A model update, data change, or new user behavior occurs D. The server clock changes
**Q07 (O3)** A good drift signal is: A. Scheduled eval runs plus sampled live grading B. CPU temperature C. Number of commits D. Disk usage
**Q08 (O4)** A kill switch should: A. Need a deploy B. Disable the feature or fall back within a minute C. Be untested D. Be known only to one person
**Q09 (O4)** An assistant revealed another customer's data. The strongest fix is: A. A stricter prompt warning B. Lower temperature C. Authorization enforced in code on the data path D. A longer prompt
**Q10 (O4)** After a bad-output incident, you should: A. Add a reproducing case to the eval set B. Delete logs C. Skip the postmortem D. Blame the model

## Answers
Q01 A · Q02 D · Q03 A · Q04 B · Q05 A · Q06 C · Q07 A · Q08 B · Q09 C · Q10 A

## Practical part
Incident simulation on a misbehaving AI feature (SRC-022 assessment), plus `SRC-022-LAB1` evidence. Pass: at least 8/10 on the quiz, kill switch under one minute, a seeded regression blocked by the gate, and a postmortem with systemic actions.
