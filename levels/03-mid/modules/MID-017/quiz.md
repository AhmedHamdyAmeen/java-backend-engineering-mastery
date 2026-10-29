# MID-017 · Connection pooling — Quiz

Outcomes: O1 why pools exist, HikariCP · O2 sizing · O3 timeouts and diagnosis · O4 more is not faster.

**Q01 (O1)** A connection pool mainly saves: A. Disk space B. Connection setup cost C. SQL parsing D. Index builds
**Q02 (O1)** Calling `close()` on a pooled connection: A. Closes the socket B. Does nothing ever C. Rolls back the schema D. Returns it to the pool
**Q03 (O2)** Little's law for a pool: connections needed ≈ A. Requests per second × hold time B. Latency ÷ throughput C. Cores × 100 D. Threads × instances only
**Q04 (O2)** With 8 app instances of pool size 20, the database sees up to: A. 20 B. 28 C. 160 D. 8
**Q05 (O2)** Best first step when the pool is exhausted: A. Raise the size to 500 B. Disable timeouts C. Restart the database D. Find why connections are held so long
**Q06 (O3)** `connectionTimeout` controls: A. Query runtime B. How long a thread waits for a pooled connection C. SSL handshake only D. Idle session lifetime on the server
**Q07 (O3)** Thread dumps showing many threads in `HikariPool.getConnection` indicate: A. Pool exhaustion B. CPU idle C. Disk failure D. DNS errors
**Q08 (O3)** `leakDetectionThreshold` helps to find: A. Memory leaks in heap B. Slow indexes C. Connections not returned in time D. Deadlocks
**Q09 (O4)** Why can more connections slow the database? A. Bigger tables B. Contention for CPU, locks, and cache C. Fewer indexes D. Slower network cables
**Q10 (O4)** A pool of 200 for a 4-core database is: A. Ideal B. Impossible C. Required for HTTP D. Likely too large

## Answers
Q01 B · Q02 D · Q03 A · Q04 C · Q05 D · Q06 B · Q07 A · Q08 C · Q09 B · Q10 D

## Practical part
Sizing scenarios: three cases with request rates, hold times, instance counts, and a database limit; choose pool sizes and explain. Pass: quiz 8/10, scenarios within reasonable bounds with correct reasoning, and the lab chart and recommendation.
