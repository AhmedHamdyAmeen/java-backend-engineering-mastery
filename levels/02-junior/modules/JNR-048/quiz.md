# JNR-048 · Linux basics — Quiz

Outcomes: O1 processes and resources · O2 permissions · O3 SSH · O4 ports · O5 logs and services.

**Q01 (O1)** Which command shows free disk space? A. `free -h` B. `ps` C. `df -h` D. `top`
**Q02 (O1)** `kill 4242` sends: A. SIGKILL B. SIGTERM C. A file D. A reboot
**Q03 (O1)** Which shows live CPU and memory use per process? A. `ls` B. `cat` C. `chmod` D. `top`
**Q04 (O2)** `chmod 640 app.env` gives others: A. Read B. Write C. No access D. Execute
**Q05 (O2)** Best practice for a service account: A. Run as root B. Run as a dedicated unprivileged user C. `chmod 777` everything D. Share one admin login
**Q06 (O3)** Which file goes on the server for key login? A. Private key B. Password file C. Public key D. Both keys
**Q07 (O3)** Which command creates a key pair? A. `ssh-keygen` B. `ssh-add` C. `scp` D. `keytool` only
**Q08 (O4)** Find the process on port 8080: A. `df -h` B. `lsof -i :8080` C. `free` D. `chown`
**Q09 (O5)** Follow a systemd service's logs: A. `journalctl -u shop -f` B. `systemctl follow` C. `ss -f` D. `ps -f`
**Q10 (O5)** Which unit-file setting restarts a service after a crash? A. `User=shop` B. `WantedBy=` C. `Restart=on-failure` D. `ExecStop=`

## Answers
Q01 C · Q02 B · Q03 D · Q04 C · Q05 B · Q06 C · Q07 A · Q08 B · Q09 A · Q10 C

## Practical part
Seven exercises `JNR-048-EX01` to `EX07` plus the lab; the assessment is a set of timed troubleshooting tasks on a Linux box. Pass: quiz 8/10, at least five exercises correct, and the service restarting after a kill.
