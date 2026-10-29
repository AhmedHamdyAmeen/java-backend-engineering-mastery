# JNR-048 · Linux basics — Exercises and lab

## Lab
### JNR-048-LAB1 · Run Shop on Linux
**Outcomes:** 1–5 · **Time:** ~3 h
On a Linux VM or WSL, run the Shop JAR as a `systemd` service under a dedicated user, read its logs, and find its port.
**Acceptance:** service restarts automatically after a kill.

## Exercises (assessment: timed troubleshooting tasks on a Linux box)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-048-EX01 | 1 | Find the PID and memory use of a Java process, then stop it gracefully. |
| JNR-048-EX02 | 1 | Report free memory and the three largest directories under `/var`. |
| JNR-048-EX03 | 2 | Given `-rwxr-xr-- alice dev script.sh`, state who can do what, then make it private to alice. |
| JNR-048-EX04 | 3 | Create an ed25519 key pair, install the public key on a VM, and log in without a password. |
| JNR-048-EX05 | 4 | Start two apps on port 8080; find which process holds it. |
| JNR-048-EX06 | 5 | Show the last 50 log lines of a service from the past 10 minutes and follow new ones. |
| JNR-048-EX07 | 5 | Make a service start at boot and restart after failure. |

## Solutions
- **EX01** `ps aux | grep java` (or `pgrep -a java`); `kill <pid>`; `kill -9` only if it ignores SIGTERM.
- **EX02** `free -h`; `du -sh /var/* | sort -h | tail -3`.
- **EX03** Owner reads, writes, executes; group `dev` reads and executes; others only read. `chmod 700 script.sh`.
- **EX04** `ssh-keygen -t ed25519`, `ssh-copy-id user@host`, `ssh user@host`.
- **EX05** `ss -tlnp | grep 8080` or `lsof -i :8080`; stop one app or change its port.
- **EX06** `journalctl -u shop --since "10 min ago" -n 50` then `journalctl -u shop -f`.
- **EX07** `sudo systemctl enable shop` and `Restart=on-failure` in the unit file (then `daemon-reload`).
- Outcome 2 (permissions) is also covered by quiz Q04–Q05 and the lab (non-root service user).
