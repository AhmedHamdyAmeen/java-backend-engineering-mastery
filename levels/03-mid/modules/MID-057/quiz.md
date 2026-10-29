# MID-057 · Kubernetes foundations — Quiz

Outcomes: O1 architecture and desired state · O2 core objects · O3 probes and resources · O4 scaling and rolling updates · O5 debugging.

**Q01 (O1)** Kubernetes stores cluster state in: A. The kubelet B. The scheduler C. Each pod D. etcd
**Q02 (O1)** Controllers work by: A. Reconciling actual state toward desired state B. Editing images C. Restarting nodes nightly D. Reading logs
**Q03 (O2)** A Deployment provides: A. Persistent disks B. Replicas and rolling updates C. DNS only D. TLS certificates
**Q04 (O2)** Why call a Service by name? A. Pod IPs change when pods are replaced B. It is shorter C. IPs are illegal D. It encrypts traffic
**Q05 (O2)** A Kubernetes Secret by default is: A. Strongly encrypted B. Hidden from admins C. Base64-encoded, so enable encryption at rest and RBAC D. Stored outside the cluster
**Q06 (O3)** A liveness probe should: A. Check the database B. Stay simple and not depend on external systems C. Run a full test suite D. Never exist
**Q07 (O3)** A startup probe helps JVM services by: A. Skipping readiness B. Allowing time to start before liveness begins C. Raising heap D. Logging more
**Q08 (O3)** A pod exceeding its memory limit is: A. Slowed down B. Moved to another node C. OOMKilled D. Ignored
**Q09 (O4)** The HPA changes: A. Image tags B. Memory limits only C. Secrets D. The number of replicas based on metrics
**Q10 (O5)** To see logs of the container that just crashed: A. `kubectl logs --previous` B. `kubectl apply` C. `kubectl scale` D. `kubectl label`

## Answers
Q01 D · Q02 A · Q03 B · Q04 A · Q05 C · Q06 B · Q07 B · Q08 C · Q09 D · Q10 A

## Practical part
Debugging exercise (`MID-057-EX06`) plus lab `MID-057-LAB1`. Pass: quiz at least 8/10, all Shop services running with probes, limits, and HPA, and a rolling update under load with zero failed requests.
