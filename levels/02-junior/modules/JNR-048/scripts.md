# JNR-048 · Linux basics — Lecture scripts

**Video:** 65 min · **Analogy used throughout:** a building's control room: the staff list, door keys, floor plan, and logbook.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## JNR-048-L01 · Linux for backend engineers (7 min)
**Goal:** see why a backend engineer needs the Linux command line.

**Key points**
- Production servers and containers almost always run Linux.
- You work through a shell (bash) by typing commands; there is often no screen or mouse.
- Everything is a file or a process; commands do one job and combine with pipes (`|`).
- Use a Linux VM or WSL for the labs.
- Learn to read a command's help: `man ls` or `ls --help`.

**Show:** `pwd`, `ls -la`, `cd /var/log`, `cat app.log | grep ERROR | tail -5`.

**Check:** What does `|` do? *(Passes one command's output to the next as input.)*

---

## JNR-048-L02 · Processes and resources (10 min)
**Goal:** see what is running and how much it uses, and stop it safely.

**Key points**
- A process is a running program with a PID (process id).
- `ps aux` lists processes; `top` shows live use of CPU and memory.
- `free -h` shows memory; `df -h` shows disk space; `du -sh *` shows folder sizes.
- `kill PID` asks politely (SIGTERM); `kill -9 PID` forces (SIGKILL) and should be a last resort.
- A full disk or out-of-memory state is a common cause of "the app just died".

**Show**
```bash
ps aux | grep java
free -h
df -h
kill 4242
```

**Check:** Which command shows free disk space? *(`df -h`.)*

---

## JNR-048-L03 · Users, permissions, ownership (10 min)
**Goal:** read and set file permissions without using `chmod 777`.

**Key points**
- Every file has an owner, a group, and three permission sets: owner, group, others, each with read, write, execute.
- `ls -l` shows them: `-rwxr-x---`.
- `chmod 640 file` or `chmod u+x file` changes permissions; `chown user:group file` changes ownership.
- Run services as a dedicated, unprivileged user, not root.
- `sudo` runs one command with admin rights; use it sparingly.

**Show:** `-rw-r----- shop shop app.env` means the owner reads and writes, the group reads, others get nothing.

**Check:** What does `chmod 777` do and why is it bad? *(Gives everyone full access; a security risk.)*

---

## JNR-048-L04 · SSH and keys (10 min)
**Goal:** log in to a server with a key instead of a password.

**Key points**
- SSH opens an encrypted shell on a remote machine: `ssh user@host`.
- A key pair has a private key (keep secret) and a public key (put on the server).
- Create with `ssh-keygen -t ed25519`; copy with `ssh-copy-id` or by adding it to `~/.ssh/authorized_keys`.
- Never share or commit the private key; protect it with a passphrase.
- Disable password login on servers once keys work.

**Show**
```bash
ssh-keygen -t ed25519 -C "me@laptop"
ssh-copy-id deploy@203.0.113.10
ssh deploy@203.0.113.10
```

**Check:** Which key goes on the server? *(The public key.)*

---

## JNR-048-L05 · Ports and networking tools (8 min)
**Goal:** find which process listens on a port.

**Key points**
- A port is a numbered door on a machine; one process can listen on a port at a time.
- `ss -tlnp` lists listening TCP ports with the process (may need `sudo`).
- `lsof -i :8080` shows what uses port 8080.
- `curl -v localhost:8080/actuator/health` tests an endpoint.
- "Address already in use" means another process holds the port.

**Show**
```bash
ss -tlnp | grep 8080
lsof -i :8080
curl -i localhost:8080/actuator/health
```

**Check:** What does "Address already in use" mean? *(Another process is already listening on that port.)*

---

## JNR-048-L06 · Logs and services (10 min)
**Goal:** read logs and control a service with systemd.

**Key points**
- `tail -f file` follows a log live; `grep` filters it.
- systemd runs services described by unit files in `/etc/systemd/system/`.
- `systemctl start|stop|restart|status shop` manages a service; `enable` starts it at boot.
- `journalctl -u shop -f` follows that service's logs; add `--since "10 min ago"`.
- In a unit file, `Restart=on-failure` and `User=shop` matter.

**Show**
```bash
sudo systemctl status shop
journalctl -u shop --since "10 min ago"
tail -f /var/log/shop/app.log
```

**Check:** Which command follows a service's logs? *(`journalctl -u <service> -f`.)*

---

## JNR-048-L07 · Demo: running Shop as a systemd service (10 min)
**Goal:** run the Shop JAR as a managed service. Prepares `JNR-048-LAB1`.

**Steps**
1. Create a `shop` system user and copy the JAR to `/opt/shop`.
2. Write `/etc/systemd/system/shop.service` with `User=shop`, `ExecStart=java -jar /opt/shop/shop.jar`, `Restart=on-failure`.
3. `systemctl daemon-reload`, `enable --now shop`, then check `status` and `journalctl -u shop`.
4. Find the port with `ss -tlnp` and call the health endpoint with `curl`.
5. **Planned mistake:** the JAR is owned by root with mode 600, so the service fails with "permission denied"; fix with `chown` and `chmod 640`, not `777`.
6. `kill` the process and show systemd restarting it.
