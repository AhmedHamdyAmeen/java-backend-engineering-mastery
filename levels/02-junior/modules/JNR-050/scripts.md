# JNR-050 · Docker Compose — Lecture scripts

**Video:** 45 min · **Analogy used throughout:** a stage manager's cue sheet that brings every actor on in the right order.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## JNR-050-L01 · Compose files (10 min)
**Goal:** describe a multi-service environment in one file.

**Key points**
- Compose runs several containers together from `compose.yaml`; one command starts or stops them all.
- Each entry under `services:` is a container: `image` or `build`, `ports`, `environment`, `volumes`.
- Compose creates a network for the project; services reach each other by service name.
- Named volumes go under `volumes:`.
- Commands: `docker compose up -d`, `ps`, `logs -f`, `down` (add `-v` to delete volumes).

**Show**
```yaml
services:
  db:
    image: postgres:16
    environment:
      POSTGRES_PASSWORD: dev
    volumes: [pgdata:/var/lib/postgresql/data]
  app:
    build: .
    ports: ["8080:8080"]
volumes:
  pgdata:
```

**Check:** What does `docker compose down -v` do beyond `down`? *(It also deletes the named volumes and their data.)*

---

## JNR-050-L02 · Health checks and startup order (8 min)
**Goal:** make services start in a usable order.

**Key points**
- `depends_on` alone only waits for the container to start, not to be ready.
- A `healthcheck` runs a command repeatedly to mark a service healthy.
- `depends_on: db: condition: service_healthy` makes the app wait for a healthy database.
- Postgres check: `pg_isready`. Tune `interval`, `timeout`, `retries`.
- Apps should still retry connections; startup order is a convenience, not a guarantee.

**Show**
```yaml
db:
  healthcheck:
    test: ["CMD-SHELL", "pg_isready -U postgres"]
    interval: 5s
    retries: 10
app:
  depends_on:
    db: { condition: service_healthy }
```

**Check:** Why is plain `depends_on` not enough? *(It does not wait until the database accepts connections.)*

---

## JNR-050-L03 · Environment and secrets (7 min)
**Goal:** supply configuration without committing secrets.

**Key points**
- Use `${VAR}` in `compose.yaml`; values come from your shell or an `.env` file.
- Commit `.env.example` with fake values; add `.env` to `.gitignore`.
- `env_file:` loads many variables into one service.
- Environment variables are for local development; real secrets use a secret manager in deployed environments.
- Never commit real passwords, even "temporary" ones.

**Show:** `POSTGRES_PASSWORD: ${DB_PASSWORD}` with `.env.example` containing `DB_PASSWORD=change-me`.

**Check:** Which file is committed: `.env` or `.env.example`? *(`.env.example`.)*

---

## JNR-050-L04 · Spring Boot's Compose integration (10 min)
**Goal:** let Spring Boot start the stack during development.

**Key points**
- Spring Boot (3.1 or later; verify version before recording) can detect `compose.yaml` and run `docker compose up` when the app starts.
- Add the `spring-boot-docker-compose` dependency (development scope).
- It creates connection details for known services such as PostgreSQL, so you need not hard-code URLs.
- On shutdown it stops the containers, controlled by `spring.docker.compose.lifecycle-management`.
- It is a development tool; production uses the real configuration.

**Show:** the Maven dependency and the app logs "Started docker compose" and then connecting to the database port chosen by Compose.

**Check:** Is Compose integration meant for production? *(No; it is for development.)*

---

## JNR-050-L05 · Demo: one-command Shop stack (10 min)
**Goal:** start Shop, PostgreSQL, and Keycloak with one command. Prepares `JNR-050-LAB1`.

**Steps**
1. Write `compose.yaml` with `db`, `keycloak`, and `app`.
2. Add health checks for `db` and `keycloak`; use `service_healthy` conditions.
3. Move passwords to `.env`; commit `.env.example`; add `.env` to `.gitignore`.
4. Mount seed SQL into the database init folder (`/docker-entrypoint-initdb.d`) and run `docker compose up`.
5. **Planned mistake:** `depends_on` without health checks, so the app crashes with "connection refused"; fix with `condition: service_healthy`.
6. Write the README steps and have a partner follow them.
