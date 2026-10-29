# JNR-050 · Docker Compose — Quiz

Outcomes: O1 compose files · O2 health checks · O3 environment and secrets · O4 Spring Boot integration.

**Q01 (O1)** Which file defines a Compose stack? A. `Dockerfile` B. `pom.xml` C. `compose.yaml` D. `.env`
**Q02 (O1)** Services in one Compose project reach each other by: A. Service name B. Random IP C. Host port only D. `localhost`
**Q03 (O1)** `docker compose down -v` also removes: A. Images only B. The source code C. The README D. Named volumes
**Q04 (O2)** Plain `depends_on` waits until the dependency: A. Is healthy B. Has started C. Has data D. Has been backed up
**Q05 (O2)** Which makes the app wait for a ready database? A. `condition: service_healthy` B. `restart: no` C. `ports` D. `build`
**Q06 (O2)** A Postgres health check commonly uses: A. `curl` B. `ls` C. `ping` D. `pg_isready`
**Q07 (O3)** Which should be committed? A. `.env` with real passwords B. `.env.example` with fake values C. Private keys D. Production DB dumps
**Q08 (O3)** `${DB_PASSWORD}` in `compose.yaml` is filled from: A. The shell or `.env` file B. The JAR C. The registry D. The Dockerfile only
**Q09 (O4)** Spring Boot's Compose support is meant for: A. Production B. Development C. Replacing the database D. Building images
**Q10 (O4)** What does it do on app start? A. Deletes volumes B. Starts the services in `compose.yaml` C. Pushes images D. Runs migrations only

## Answers
Q01 C · Q02 A · Q03 D · Q04 B · Q05 A · Q06 D · Q07 B · Q08 A · Q09 B · Q10 B

## Practical part
Six exercises `JNR-050-EX01` to `EX06` plus the lab; the assessment is the lab check. Pass: quiz 8/10, at least five exercises correct, and a teammate starts the stack from the README in under 10 minutes.
