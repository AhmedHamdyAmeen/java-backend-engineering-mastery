# MID-049 · Reliability — Quiz

Outcomes: O1 SLIs · O2 SLOs and error budgets · O3 burn-rate alerts · O4 using the budget.

**Q01 (O1)** An SLI is typically: A. Good events divided by valid events B. CPU usage C. A server count D. A log level
**Q02 (O1)** Best place to measure availability for users: A. Inside one class B. At the gateway or load balancer C. In the database only D. In the build
**Q03 (O1)** A latency SLI could be: A. Average CPU B. Number of pods C. Requests under 300 ms divided by all requests D. Heap size
**Q04 (O2)** The error budget of a 99.9% SLO is: A. 99.9% B. 1% C. 0.01% D. 0.1%
**Q05 (O2)** Why not set a 100% SLO? A. It is unaffordable and blocks change B. It is too easy C. Tools do not allow it D. Users prefer 99%
**Q06 (O2)** 99.9% over 30 days allows roughly: A. 4 hours B. 43 minutes C. 7 seconds D. 2 days
**Q07 (O3)** Burn rate 1 means: A. No errors B. The service is down C. The budget is used exactly over the window D. Alerts are off
**Q08 (O3)** Combining a long and a short window in a burn-rate alert: A. Reduces false alarms B. Doubles the budget C. Removes the SLO D. Disables paging
**Q09 (O4)** When budget is nearly spent, teams should: A. Ship faster B. Delete the SLO C. Ignore alerts D. Slow risky releases and fix reliability
**Q10 (O4)** The budget policy should be: A. Decided during an outage B. Secret C. Agreed and written in advance D. Set by the model

## Answers
Q01 A · Q02 B · Q03 C · Q04 D · Q05 A · Q06 B · Q07 C · Q08 A · Q09 D · Q10 C

## Practical part
Seven exercises `MID-049-EX01` to `EX07` (EX07 is the SLO document review) plus the checkout SLO lab. Pass: at least five exercises and a lab with a reviewed SLO document and burn-rate alerts tested by injected errors.
