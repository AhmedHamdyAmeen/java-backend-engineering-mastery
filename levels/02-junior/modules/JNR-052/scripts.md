# JNR-052 · Deployment basics — Lecture scripts

**Video:** 69 min · **Analogy used throughout:** opening a shop for customers: stock arrives, doors open, a sign shows open or closed, and there is a way to go back to the old layout.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## JNR-052-L01 · From artifact to running service (8 min)
**Goal:** see the steps between a built image and a live URL.

**Key points**
- The pipeline produces an artifact (a tagged image); deployment runs it somewhere.
- Needs: a host to run the container, a database, configuration, and a public address.
- Typical flow: pull image, stop old container, start new one, check health.
- Keep build and deploy separate: the same image goes to every environment.
- The database is managed state; the app container is disposable.

**Show:** a flow: registry, server (pulls image), container, managed PostgreSQL, public URL.

**Check:** What stays the same between environments? *(The image; only configuration changes.)*

---

## JNR-052-L02 · Deployment targets compared (10 min)
**Goal:** pick a simple target for Shop.

**Key points**
- A VM (virtual machine) with Docker: most control, most work (updates, security).
- A PaaS (platform as a service, such as a managed app host): you push an image; the platform runs it. Easiest start.
- A managed container service from a cloud provider: more features, more setup.
- Kubernetes: powerful, usually too much for a first deployment (covered later).
- Compare cost, control, effort, and lock-in. Verify current free tiers and prices before recording.

**Show:** a table: VM / PaaS / managed containers / Kubernetes against effort, control, cost.

**Check:** Which option is the easiest first deployment? *(A PaaS.)*

---

## JNR-052-L03 · Configuration in deployed environments (8 min)
**Goal:** configure the app without rebuilding it.

**Key points**
- Spring Boot reads environment variables: `SPRING_DATASOURCE_URL` maps to `spring.datasource.url`.
- Put database credentials and keys in the platform's secret store, never in the image or Git.
- Use profiles (`SPRING_PROFILES_ACTIVE=prod`) for non-secret differences.
- Config that changes per environment is passed at run time.
- Log which profile is active at startup, but not any secret values.

**Show**
```bash
docker run -d -p 8080:8080 \
  -e SPRING_PROFILES_ACTIVE=prod \
  -e SPRING_DATASOURCE_URL=jdbc:postgresql://db.example.internal:5432/shop \
  -e SPRING_DATASOURCE_PASSWORD="$DB_PASSWORD" shop:1.0
```

**Check:** Where do database passwords belong? *(In the platform's secret store, passed as environment variables, never in the image.)*

---

## JNR-052-L04 · Health checks: liveness vs readiness (10 min)
**Goal:** expose and use the two health signals.

**Key points**
- Liveness asks: "is the process stuck and in need of a restart?"
- Readiness asks: "can the app take traffic now?" (for example, the database is reachable).
- Spring Boot Actuator exposes `/actuator/health/liveness` and `/actuator/health/readiness` (enable the probes; verify properties for your version).
- Do not check the database in liveness: a database outage would restart healthy apps and make things worse.
- Expose only the health endpoint publicly; keep other actuator endpoints private.

**Show**
```yaml
management:
  endpoint.health.probes.enabled: true
  endpoints.web.exposure.include: health
```

**Check:** Which probe should fail when the database is down? *(Readiness.)*

---

## JNR-052-L05 · Graceful shutdown and rollback (9 min)
**Goal:** stop and revert without dropping requests.

**Key points**
- On SIGTERM a graceful shutdown finishes in-flight requests: `server.shutdown=graceful` plus a timeout.
- The platform sends SIGTERM, waits, then SIGKILL; set the timeout under that grace period.
- Roll back by redeploying the previous image tag; this is why tags must be unique and old images kept.
- Database changes complicate rollback: make migrations backward compatible.
- Practice the rollback before you need it.

**Show**
```yaml
server.shutdown: graceful
spring.lifecycle.timeout-per-shutdown-phase: 20s
```

**Check:** What is the fastest rollback for a bad release? *(Redeploy the previous image tag.)*

---

## JNR-052-L06 · Demo: deploying Shop and its database (12 min)
**Goal:** put Shop on a public URL. Prepares `JNR-052-LAB1`.

**Steps**
1. Create a managed PostgreSQL instance and note its connection string.
2. Create the app service from the tagged image in the registry.
3. Set environment variables and secrets; enable the readiness probe as the platform health check.
4. Deploy from the pipeline; open the public URL and call the health endpoint.
5. **Planned mistake:** the app starts in a loop because liveness checks the database, which is not reachable yet; move the database check to readiness.
6. Place an order through the live API.

---

## JNR-052-L07 · Demo: rolling back a bad release (12 min)
**Goal:** return quickly to the last good version. Prepares `JNR-052-LAB1`.

**Steps**
1. Deploy version 1.1 with a deliberate bug.
2. Notice the failing health check or error in the logs.
3. Redeploy the previous image tag (for example `1.0`) and time it.
4. Verify with the health endpoint and a test request.
5. **Planned mistake:** the previous image was deleted by a cleanup rule; keep the last several tags.
6. Write the rollback steps into the runbook, aiming for under five minutes.
