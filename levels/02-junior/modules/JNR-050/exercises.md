# JNR-050 · Docker Compose — Exercises and lab

## Lab
### JNR-050-LAB1 · One-command Shop
**Outcomes:** 1–4 · **Time:** ~2 h
`docker compose up` starts the whole stack (Shop, PostgreSQL, Keycloak) with seeded data, health checks, and env-file configuration. Write a README.
**Acceptance:** a new teammate runs the stack in under 10 minutes using only the README.

## Exercises (assessment: lab check)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-050-EX01 | 1 | Write a `compose.yaml` with PostgreSQL (named volume) and the Shop app built from the Dockerfile. |
| JNR-050-EX02 | 1 | Add Keycloak and expose it on a host port; list which service names reach which. |
| JNR-050-EX03 | 2 | Add a `pg_isready` health check and make the app wait with `service_healthy`. |
| JNR-050-EX04 | 2 | Explain why the app can still fail even with `service_healthy`, and what the app should do about it. |
| JNR-050-EX05 | 3 | Move the database password to `.env`, add `.env.example`, and update `.gitignore`. |
| JNR-050-EX06 | 4 | Add the Spring Boot Docker Compose dependency and run the app from the IDE without starting Compose manually. |

## Solutions
- **EX01** Services `db` (`image: postgres:16`, `volumes: [pgdata:/var/lib/postgresql/data]`) and `app` (`build: .`, `ports: ["8080:8080"]`), plus top-level `volumes: pgdata:`.
- **EX02** `keycloak` service with its image and `ports`; `app` reaches `db:5432` and `keycloak:8080` by service name; the browser uses the mapped host port.
- **EX03** `healthcheck: test: ["CMD-SHELL","pg_isready -U postgres"]` and `depends_on: db: condition: service_healthy`.
- **EX04** Healthy means ready at that moment; the database can restart later. The app should use connection retries (and a pool that recovers).
- **EX05** `POSTGRES_PASSWORD: ${DB_PASSWORD}`; `.env.example` has `DB_PASSWORD=change-me`; `.gitignore` lists `.env`.
- **EX06** Add `spring-boot-docker-compose` (verify the artifact and Boot version); starting the app launches the stack and wires the datasource.
- Common mistakes (committed `.env`, `depends_on` without health) are checked in the lab.
