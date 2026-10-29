# JNR-049 · Docker fundamentals — Quiz

Outcomes: O1 concepts · O2 Dockerfile · O3 volumes and ports · O4 networks · O5 inspecting.

**Q01 (O1)** A running instance of an image is a: A. Layer B. Registry C. Tag D. Container
**Q02 (O1)** Compared with a VM, a container: A. Shares the host kernel B. Has its own kernel C. Needs a hypervisor always D. Cannot run Java
**Q03 (O2)** The main benefit of a multi-stage build: A. Slower builds B. Final image excludes build tools C. Bigger images D. No need for a JRE
**Q04 (O2)** To run as non-root in a Dockerfile: A. `RUN root` B. `CMD user` C. `USER shop` D. `EXPOSE shop`
**Q05 (O2)** Which tag practice is best? A. `latest` B. No tag C. Random tags D. Pinned version such as `postgres:16`
**Q06 (O3)** Data that must survive container removal belongs in a: A. Volume B. Layer C. Environment variable D. Tag
**Q07 (O3)** `-p 9090:8080` means: A. Container 9090 to host 8080 B. Host 9090 to container 8080 C. Two containers D. A volume
**Q08 (O4)** On a user-defined network, the app reaches the database container `db` using: A. `localhost` B. `127.0.0.1` C. The host's public IP D. The name `db`
**Q09 (O5)** Which shows a container's app output? A. `docker logs` B. `docker images` C. `docker pull` D. `docker tag`
**Q10 (O5)** Which opens a shell inside a running container? A. `docker run` B. `docker build` C. `docker rm` D. `docker exec -it NAME sh`

## Answers
Q01 D · Q02 A · Q03 B · Q04 C · Q05 D · Q06 A · Q07 B · Q08 D · Q09 A · Q10 D

## Practical part
Seven exercises `JNR-049-EX01` to `EX07` plus the lab; for the assessment, review a poor Dockerfile and submit an improved version. Pass: quiz 8/10, at least five exercises correct, image under 300 MB, and data surviving container removal.
