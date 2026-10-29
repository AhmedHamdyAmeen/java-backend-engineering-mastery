# SRC-012 · SLO engineering — Quiz

Outcomes: O1 deriving SLOs · O2 error-budget policy · O3 burn-rate alerts · O4 SLO review.

**Q01 (O1)** An SLI is best defined as: A. A contract with penalties B. A measured ratio of good to valid events C. A dashboard color D. A team goal
**Q02 (O1)** Where should an availability SLI ideally be measured? A. Inside the database B. Only in unit tests C. Close to the user, such as the gateway D. On a developer laptop
**Q03 (O1)** Three serial hard dependencies at 99.9% each give about: A. 99.9% B. 99.97% C. 99.99% D. 99.7%
**Q04 (O2)** The error budget for a 99.95% SLO is: A. 0.5% B. 0.05% C. 5% D. 0.95%
**Q05 (O2)** An error-budget policy is credible when it: A. Has pre-agreed consequences B. Is kept secret C. Has no thresholds D. Only applies to juniors
**Q06 (O3)** Burn rate 1 means: A. Budget is exhausted at once B. No errors C. Budget is consumed exactly over the window D. Ten times too fast
**Q07 (O3)** The short window in a multi-window alert mainly: A. Raises the burn rate B. Confirms the problem is still happening so alerts reset quickly C. Hides outages D. Replaces the SLO
**Q08 (O3)** A fast-burn alert should typically: A. Create a low-priority ticket B. Be ignored C. Page someone D. Run weekly
**Q09 (O4)** An SLO that is always 100% met and unused should be: A. Kept forever B. Made looser C. Hidden D. Tightened or retired
**Q10 (O4)** An incident that breached no SLO suggests: A. A missing or poorly defined SLI B. SLOs are perfect C. Alerts are too sensitive D. No action needed

## Answers
Q01 B · Q02 C · Q03 D · Q04 B · Q05 A · Q06 C · Q07 B · Q08 C · Q09 D · Q10 A

## Practical part
SLO and policy review (SRC-012 assessment): critique a given SLO set and policy, and show `SRC-012-LAB1` alert simulation results. Pass: at least 8/10 on the quiz, composition arithmetic correct, and a policy with real consequences.
