# MID-031 · Distributed workflows — Quiz

Outcomes: O1 saga model · O2 choreography vs orchestration · O3 orchestrated saga state · O4 compensation design.

**Q01 (O1)** A saga consists of: A. Local transactions plus compensations B. One global ACID transaction C. Only retries D. Two-phase commit
**Q02 (O1)** A weakness of 2PC across services: A. It is too cheap B. Participants can block holding locks C. It needs no coordinator D. It removes failures
**Q03 (O1)** Sagas lack: A. Atomicity of each step B. Local transactions C. Isolation between steps D. Messages
**Q04 (O2)** In choreography: A. Services react to each other's events B. A central owner sends commands C. There is no messaging D. Only one service exists
**Q05 (O2)** A flow of 6 steps with branching and deadlines usually suits: A. Choreography B. Orchestration C. 2PC D. Cron jobs
**Q06 (O2)** A risk of orchestration: A. Flow is invisible B. The orchestrator turning into a business-logic hub C. No timeouts possible D. No persistence possible
**Q07 (O3)** Why persist saga state? A. For prettier logs B. To resume after restart and detect stuck sagas C. To avoid messages D. To skip idempotency
**Q08 (O3)** A reply arrives for a saga already in `COMPENSATING`. The handler should: A. Proceed with the next forward step B. Crash C. Ignore or handle it based on current state D. Delete the saga
**Q09 (O4)** A compensation must be: A. Idempotent and tolerant of a missing forward step B. A database rollback C. Run exactly once by the broker D. Only manual
**Q10 (O4)** Which is a good compensation for a captured payment? A. Delete the payment row B. Ignore it C. Restart the JVM D. Issue a refund

## Answers
Q01 A · Q02 B · Q03 C · Q04 A · Q05 B · Q06 B · Q07 B · Q08 C · Q09 A · Q10 D

## Practical part
Seven exercises `MID-031-EX01` to `EX07`, the returns saga design, and `MID-031-LAB1`. Pass: at least six exercises, a returns design with compensations and timeouts, and a lab where all failure paths pass.
