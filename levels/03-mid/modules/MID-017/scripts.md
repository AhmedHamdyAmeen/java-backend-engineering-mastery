# MID-017 · Connection pooling — Lecture scripts

**Video:** 50 min · **Running project:** Shop Platform (load-tested checkout endpoint)
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-017-L01 · The cost of a database connection (8 min)
**Goal:** explain why applications reuse connections.

**Key points**
- Opening a PostgreSQL connection costs a TCP handshake, authentication, optional TLS, and a new server process (PostgreSQL uses one process per connection).
- Each connection uses memory on the server; many idle connections waste it.
- A pool keeps a fixed set of open connections and lends them out per transaction.
- The database does useful work only on as many queries as it has CPU cores and disks; extra connections queue inside it.

**Show:** a diagram: 200 request threads, a pool of 10 connections, one database; requests wait in the pool queue rather than inside the database.

**Check:** Why not open a new connection per request? *(Setup is slow and each connection costs server memory and a process.)*

---

## MID-017-L02 · HikariCP internals (10 min)
**Goal:** know how HikariCP lends and manages connections.

**Key points**
- HikariCP is the default pool in Spring Boot.
- `getConnection()` takes an idle connection or waits up to `connectionTimeout`; then it throws.
- Connections are validated and retired after `maxLifetime` (set below any database or proxy limit) and `idleTimeout` (only relevant when `minimumIdle < maximumPoolSize`).
- `close()` on a pooled connection returns it to the pool; it does not close the socket.
- Metrics (active, idle, pending, timeouts) are exposed through Micrometer.

**Show**
```yaml
spring:
  datasource:
    hikari:
      maximum-pool-size: 10
      connection-timeout: 3000
      max-lifetime: 1500000
```
Verify property names and defaults for your Boot version before recording.

**Check:** What does `close()` do on a pooled connection? *(Returns it to the pool.)*

---

## MID-017-L03 · Sizing a pool (12 min)
**Goal:** size a pool from capacity, not by guesswork.

**Key points**
- Start with the database: total connections across all app instances must stay under what the server can serve (cores and disks, and `max_connections`).
- A common starting rule: `connections ≈ (core_count × 2) + effective_spindle_count`; treat it as a start, then measure.
- Little's law: concurrent connections needed ≈ requests per second × average time a connection is held.
- Multiply the pool by the number of app instances; autoscaling can overload the database.
- Shorter transactions need fewer connections; fix slow queries before enlarging the pool.

**Show:** a worked example: 400 req/s × 25 ms hold = 10 connections on average; add headroom; three instances means 4–6 per instance.

**Check:** 200 req/s, each holds a connection 50 ms. About how many connections are busy on average? *(10.)*

---

## MID-017-L04 · Timeouts and leak detection (8 min)
**Goal:** configure timeouts that fail fast, and find leaks.

**Key points**
- `connectionTimeout`: how long a thread waits for a connection (a few seconds, not 30 s default for APIs; verify default).
- Database side: `statement_timeout`, `lock_timeout`, `idle_in_transaction_session_timeout`.
- A leak is a borrowed connection never returned; `leakDetectionThreshold` logs a stack trace when one is held too long.
- Pool exhaustion signs: threads blocked in `HikariPool.getConnection` in thread dumps, `pending` threads metric above zero.
- Do not hold a connection across remote calls; `spring.jpa.open-in-view` can hold one for a whole request (consider turning it off).

**Show:** a thread dump excerpt with many threads waiting in `HikariPool.getConnection`.

**Check:** What does `leakDetectionThreshold` report? *(A stack trace for connections held longer than the threshold.)*

---

## MID-017-L05 · Demo: pool exhaustion under load (12 min)
**Goal:** reproduce exhaustion, diagnose it, and fix the cause.

**Steps**
1. Run Shop with pool size 5 and a load test of 100 concurrent users on checkout.
2. Watch metrics: `hikaricp_connections_active` at max, `pending` growing, latencies climbing, then timeout errors.
3. Take a thread dump and find threads waiting in `getConnection` and the holders inside a slow remote call.
4. **Planned mistake:** raise the pool to 200 to "fix" it; database CPU saturates and latency does not improve. Revert.
5. Real fix: move the remote call out of the transaction; reduce hold time; right-size the pool.
6. Re-run the load test and compare.

Prepares MID-017-LAB1.

**Check:** What was the real cause of exhaustion? *(Connections held during a slow call inside a transaction.)*
