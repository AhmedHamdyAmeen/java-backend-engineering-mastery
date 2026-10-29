# JNR-049 · Docker fundamentals — Lecture scripts

**Video:** 84 min · **Analogy used throughout:** shipping containers: the same sealed box runs on any ship, truck, or crane.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## JNR-049-L01 · Why containers (8 min)
**Goal:** explain what problem containers solve and how they differ from VMs.

**Key points**
- "Works on my machine" happens because machines differ; a container packs the app with its runtime and libraries.
- A container is an isolated process on the host's kernel; a VM runs a whole separate operating system.
- Containers start in seconds and use less memory than VMs.
- A container is not a security boundary as strong as a VM.
- Docker is the most common tool; the image format is a standard.

**Show:** two stacks side by side: VM (app, guest OS, hypervisor, hardware) versus container (app, container runtime, host OS, hardware).

**Check:** Does a container include its own kernel? *(No; it shares the host's kernel.)*

---

## JNR-049-L02 · Images, layers, registries (10 min)
**Goal:** tell an image from a container and understand layers.

**Key points**
- An image is a read-only template; a container is a running instance of it.
- Images are built from layers; unchanged layers are cached and reused.
- A registry (Docker Hub, GitHub Container Registry) stores images; `docker pull` downloads, `docker push` uploads.
- A tag names a version: `postgres:16`. Avoid `latest` because it changes without notice.
- Verify the current supported PostgreSQL and Java base image tags before recording.

**Show:** `docker pull postgres:16`, `docker images`, and a layer diagram: base OS, JRE, app JAR.

**Check:** Image or container: which one runs? *(The container; the image is the template.)*

---

## JNR-049-L03 · Running containers (10 min)
**Goal:** start, inspect, and stop containers.

**Key points**
- `docker run -d --name db -p 5432:5432 postgres:16` starts a container in the background.
- `-p host:container` maps a port so you can reach the app.
- `-e NAME=value` sets environment variables.
- `docker ps` lists running containers; `docker stop`, `docker rm` stop and remove.
- Containers are disposable: removing one deletes its internal data unless you use a volume.

**Show**
```bash
docker run -d --name db -e POSTGRES_PASSWORD=dev -p 5432:5432 postgres:16
docker ps
docker stop db && docker rm db
```

**Check:** What does `-p 8080:80` do? *(Maps host port 8080 to container port 80.)*

---

## JNR-049-L04 · Writing a Dockerfile for Spring Boot (14 min)
**Goal:** write a small, safe image for a Spring Boot app.

**Key points**
- A Dockerfile lists the build steps; each instruction makes a layer.
- Multi-stage build: stage one builds the JAR with the JDK; stage two copies only the JAR into a JRE image, so the final image has no build tools.
- Run as a non-root user: `USER shop`.
- Order instructions so rarely changing layers come first (dependencies before source) for better caching.
- Use a `.dockerignore`, pin base image versions, and never put secrets in the image.
- Verify the current Temurin/JRE image tags before recording.

**Show**
```dockerfile
FROM eclipse-temurin:21-jdk AS build
WORKDIR /src
COPY . .
RUN ./mvnw -q package -DskipTests

FROM eclipse-temurin:21-jre
RUN useradd -r shop
USER shop
COPY --from=build /src/target/shop.jar /app/shop.jar
ENTRYPOINT ["java","-jar","/app/shop.jar"]
```

**Check:** Why two stages? *(The final image keeps only the JAR and JRE, not the build tools.)*

---

## JNR-049-L05 · Volumes and networks (10 min)
**Goal:** keep data and connect containers.

**Key points**
- A volume is storage managed by Docker that outlives the container: `-v pgdata:/var/lib/postgresql/data`.
- A bind mount maps a host folder; volumes are better for databases.
- On a user-defined network, containers reach each other by name: the app connects to host `db`, not `localhost`.
- The default bridge network does not give name lookup.
- Create with `docker network create shop-net` and `--network shop-net`.

**Show**
```bash
docker network create shop-net
docker run -d --name db --network shop-net -v pgdata:/var/lib/postgresql/data -e POSTGRES_PASSWORD=dev postgres:16
```

**Check:** What hostname does the app use to reach the container named `db`? *(`db`, on a shared user-defined network.)*

---

## JNR-049-L06 · Debugging containers (8 min)
**Goal:** find out why a container misbehaves.

**Key points**
- `docker logs -f NAME` shows the output of the app.
- `docker exec -it NAME sh` opens a shell inside a running container.
- `docker inspect NAME` shows environment, mounts, network, and exit code.
- `docker ps -a` shows stopped containers; check their exit code (137 often means killed, for example out of memory).
- Check the simple things first: wrong port, wrong env var, wrong hostname.

**Show:** `docker logs shop`, `docker exec -it shop sh`, `docker inspect shop --format '{{.State.ExitCode}}'`.

**Check:** Which command opens a shell in a running container? *(`docker exec -it NAME sh`.)*

---

## JNR-049-L07 · Demo: writing a multi-stage Dockerfile for Shop (12 min)
**Goal:** build a small, non-root Shop image. Prepares `JNR-049-LAB1`.

**Steps**
1. Write the two-stage Dockerfile with a `.dockerignore`.
2. Build with `docker build -t shop:1.0 .` and compare the size with a single-stage build.
3. Add a non-root user and confirm with `docker exec shop whoami`.
4. Run PostgreSQL with a volume on a shared network; run Shop against it.
5. **Planned mistake:** the app uses `localhost` for the database and fails to connect; fix with the container name `db` via an environment variable.
6. Remove and recreate the database container to show the data survives.

---

## JNR-049-L08 · Demo: debugging a crashing container (12 min)
**Goal:** diagnose a container that exits at start.

**Steps**
1. Start Shop; `docker ps` shows nothing, and `docker ps -a` shows `Exited (1)`.
2. Read `docker logs` and find the connection error.
3. Use `docker inspect` to see the environment variables and spot the missing password.
4. Start a temporary container with `docker run --rm -it --entrypoint sh shop:1.0` to look around.
5. **Planned mistake:** rebuild the image to change one env var; fix by passing `-e` at run time instead of rebuilding.
6. Run again, confirm health with `curl`, and record the cause in a note.
