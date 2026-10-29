# MID-057 · Kubernetes foundations — Exercises and lab

## Lab
### MID-057-LAB1 · Shop on Kubernetes
**Outcomes:** 1–5 · **Time:** ~4 h
Deploy all Shop services, Kafka (operator or managed), and the gateway to a cluster (kind, k3d, or managed). Use Deployments, Services, an Ingress, ConfigMaps, and Secrets. Configure startup, readiness, and liveness probes and resource requests and limits for each JVM service, and an HPA on `orders`.
**Acceptance:** a rolling update under load with zero failed requests.

## Exercises (assessment: debugging a broken manifest set)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-057-EX01 | 1 | Explain what happens between `kubectl apply` and a running pod. |
| MID-057-EX02 | 2 | Write the Deployment, Service, and ConfigMap for `inventory`. |
| MID-057-EX03 | 3 | Fix this probe set: liveness calls an endpoint that queries the database; no startup probe. |
| MID-057-EX04 | 3 | Set requests, limits, and JVM heap flags for a service using about 600 MB of heap. |
| MID-057-EX05 | 4 | Add an HPA to `orders` and a rolling update strategy with no lost capacity. |
| MID-057-EX06 | 5 | Debug the provided manifests: `ImagePullBackOff`, a wrong Service selector, and an OOMKilled pod. |

## Solutions
- **EX01** API server stores the object in etcd; a controller creates a ReplicaSet and pods; the scheduler assigns a node; the kubelet pulls the image and starts containers.
- **EX02** Deployment with a pinned image and labels; Service selecting `app: inventory`; ConfigMap via `envFrom`.
- **EX03** Liveness checks only that the process is alive (`/actuator/health/liveness`); readiness may reflect dependencies; add a startup probe with a generous failure threshold.
- **EX04** Example: memory request and limit 1 Gi, `-XX:MaxRAMPercentage=70`, CPU request 500m; verify by observing the pod under load.
- **EX05** `HorizontalPodAutoscaler` minReplicas 3, maxReplicas 10, CPU 70%; `maxSurge: 1`, `maxUnavailable: 0`.
- **EX06** `describe` shows the wrong tag or registry credentials; compare Service selector with pod labels (`kubectl get endpoints` is empty); OOMKilled: raise the limit or reduce heap after checking usage.

**Outcome 1** is also covered by quiz Q01–Q02; the other outcomes by the lab and the debugging exercise.
