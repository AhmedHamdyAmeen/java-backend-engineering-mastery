# JNR-049 · Docker fundamentals — Exercises and lab

## Lab
### JNR-049-LAB1 · Containerize Shop
**Outcomes:** 1–5 · **Time:** ~3 h
Build a multi-stage, non-root Shop image under 300 MB. Run PostgreSQL in a container with a volume and connect Shop through a user-defined network.
**Acceptance:** data survives container removal.

## Exercises (assessment: review and improve a poor Dockerfile)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-049-EX01 | 1 | Explain in four sentences the difference between an image and a container, and between a container and a VM. |
| JNR-049-EX02 | 2 | Convert a single-stage Dockerfile (JDK, Maven, source, JAR in one image) into a multi-stage build. |
| JNR-049-EX03 | 2 | Add a non-root user and a `.dockerignore`; prove with `docker exec` that the app is not root. |
| JNR-049-EX04 | 3 | Run PostgreSQL with a named volume, insert a row, remove the container, start a new one, and show the row. |
| JNR-049-EX05 | 3 | Map the app to host port 9090 while it listens on 8080 inside. |
| JNR-049-EX06 | 4 | Create a network and make the app reach the database by name. |
| JNR-049-EX07 | 5 | A container exits immediately. List the three commands you use first and what each shows. |

## Solutions
- **EX01** An image is a read-only template of layers; a container is a running instance. A VM has its own OS kernel; a container shares the host kernel and is lighter.
- **EX02** Stage one `FROM eclipse-temurin:<jdk> AS build` runs Maven; stage two `FROM eclipse-temurin:<jre>` does `COPY --from=build` for the JAR only.
- **EX03** `RUN useradd -r shop` and `USER shop`; `docker exec shop whoami` prints `shop`. `.dockerignore` lists `target/`, `.git`, `.env`.
- **EX04** `-v pgdata:/var/lib/postgresql/data`; after `docker rm -f` and a new `docker run` with the same volume, `select` returns the row.
- **EX05** `docker run -p 9090:8080 shop:1.0`.
- **EX06** `docker network create shop-net`; start both with `--network shop-net`; set `SPRING_DATASOURCE_URL=jdbc:postgresql://db:5432/shop`.
- **EX07** `docker ps -a` (exit code), `docker logs NAME` (error message), `docker inspect NAME` (env, mounts, ports).
- Common mistakes (`latest`, secrets baked into images, building inside the final image) are checked in the assessment review.
