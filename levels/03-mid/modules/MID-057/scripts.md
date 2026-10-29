# MID-057 · Kubernetes foundations — Lecture scripts

**Video:** 106 min · **Analogy used throughout:** a port authority: you declare which ships must be docked and where, and the authority keeps replacing, moving, and counting them until reality matches the plan. Running project: Shop.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-057-L01 · Why Kubernetes (8 min)
**Goal:** know the problems Kubernetes solves and when it is worth its cost.

**Key points**
- It schedules containers across machines, restarts failures, scales, and rolls out updates.
- You describe the desired state in YAML; the system works to match it.
- Cost: complexity and operational skill; a managed cluster reduces it.
- Not every system needs it; a handful of services may run well on simpler platforms.

**Show:** Shop with eight services: what you would script by hand (placement, restarts, rollouts) versus what Kubernetes does.

**Check:** What does "desired state" mean? *(You declare what should run; Kubernetes keeps reality matching it.)*

---

## MID-057-L02 · Architecture and desired state (10 min)
**Goal:** name the components and the reconciliation loop.

**Key points**
- Control plane: API server, etcd (state store), scheduler, controller manager.
- Nodes run the kubelet and a container runtime; pods run on nodes.
- Controllers watch actual state and act to reach the desired state (a reconciliation loop).
- Everything goes through the API server; `kubectl` is a client.

**Show:** diagram: `kubectl apply` → API server → etcd → scheduler → kubelet starts the pod.

**Check:** Which component stores cluster state? *(etcd, via the API server.)*

---

## MID-057-L03 · Pods and Deployments (12 min)
**Goal:** run and update a service with a Deployment.

**Key points**
- A pod is one or more containers sharing a network; pods are disposable.
- A Deployment keeps N replicas and performs rolling updates; it manages ReplicaSets.
- Use an exact image tag or digest, never `latest`.
- Labels and selectors connect Deployments, Services, and other objects.

**Show**
```yaml
apiVersion: apps/v1
kind: Deployment
metadata: { name: orders }
spec:
  replicas: 3
  selector: { matchLabels: { app: orders } }
  template:
    metadata: { labels: { app: orders } }
    spec:
      containers:
        - name: orders
          image: registry.example/shop/orders:3f2a9c1
```

**Check:** Why not use `latest`? *(It is mutable, so you cannot know or reproduce what is running.)*

---

## MID-057-L04 · Services and Ingress (10 min)
**Goal:** give pods a stable address and expose them.

**Key points**
- A Service gives a stable name and virtual IP and load-balances across matching ready pods.
- Types: ClusterIP (internal), NodePort, LoadBalancer (cloud load balancer).
- Ingress (or the Gateway API) routes HTTP by host and path to Services, via an ingress controller.
- Services find each other by DNS: `http://inventory:8080`.

**Show:** Ingress routing `/api/orders` to the `orders` Service and `/api/catalog` to `catalog`.

**Check:** Why a Service instead of pod IPs? *(Pods are replaced and their IPs change; the Service name is stable.)*

---

## MID-057-L05 · ConfigMaps and Secrets (8 min)
**Goal:** separate configuration from images.

**Key points**
- ConfigMap: non-sensitive settings as environment variables or files.
- Secret: sensitive values, base64-encoded (not encrypted by default); enable encryption at rest and strict RBAC.
- Better: an external secrets manager synced by an operator (see MID-054).
- Changing a ConfigMap does not restart pods automatically; plan the rollout.

**Show:** `envFrom: configMapRef` for settings and a Secret mounted as a file for the database password.

**Check:** Is a Kubernetes Secret encrypted by default? *(No, only base64-encoded; enable encryption at rest and RBAC.)*

---

## MID-057-L06 · Probes for JVM services (10 min)
**Goal:** configure the three probes correctly for a Spring Boot service.

**Key points**
- Startup probe: allows slow JVM start before other probes begin.
- Readiness: should this pod receive traffic now; may include dependencies it needs to serve.
- Liveness: should the pod be restarted; keep it simple and never check the database, or a database outage restarts every pod.
- Spring Boot Actuator exposes liveness and readiness health groups (`/actuator/health/liveness`, `/actuator/health/readiness`).
- Set graceful shutdown so in-flight requests finish.

**Show**
```yaml
startupProbe:   { httpGet: { path: /actuator/health/liveness,  port: 8080 }, failureThreshold: 30, periodSeconds: 2 }
readinessProbe: { httpGet: { path: /actuator/health/readiness, port: 8080 } }
livenessProbe:  { httpGet: { path: /actuator/health/liveness,  port: 8080 } }
```

**Check:** Why must liveness not check the database? *(A database outage would restart all pods and worsen the incident.)*

---

## MID-057-L07 · Requests, limits, and autoscaling (12 min)
**Goal:** size JVM pods and scale them.

**Key points**
- Requests are used for scheduling; limits are enforced ceilings.
- Exceeding the memory limit kills the pod (OOMKilled); set the JVM heap relative to the limit (for example `-XX:MaxRAMPercentage=75`); verify flags for your JDK version.
- CPU limits can throttle; many teams set CPU requests and fewer limits. Decide deliberately.
- Horizontal Pod Autoscaler (HPA) adds or removes replicas based on CPU, memory, or custom metrics.
- Rolling update settings (`maxSurge`, `maxUnavailable`) control the pace and capacity.

**Show:** resources block with requests/limits and an HPA targeting 70% CPU, 3 to 10 replicas.

**Check:** What happens when a pod exceeds its memory limit? *(It is OOMKilled and restarted.)*

---

## MID-057-L08 · Debugging pods (10 min)
**Goal:** diagnose a failing pod systematically.

**Key points**
- `kubectl get pods` shows status; `describe pod` shows events (scheduling, image pull, probe failures).
- `kubectl logs <pod>` and `--previous` for the last crashed container.
- `kubectl exec -it` opens a shell; `port-forward` reaches a service locally.
- Common states: `ImagePullBackOff`, `CrashLoopBackOff`, `Pending`, `OOMKilled`.
- Check events cluster-wide: `kubectl get events --sort-by=.lastTimestamp`.

**Show:** table: symptom → first command → likely cause.

**Check:** Which flag shows logs of the crashed container? *(`--previous`.)*

---

## MID-057-L09 · Demo: deploying Shop Platform to a cluster (14 min)
**Goal:** run all services behind the gateway on a cluster. Prepares MID-057-LAB1.

**Steps**
1. Start a kind or k3d cluster (or use the managed one); create the `shop` namespace.
2. Apply ConfigMaps, Secrets, and Deployments for `catalog`, `inventory`, `orders`, and the gateway; install Kafka by operator or point to a managed one.
3. **Planned mistake:** deploy `orders` before PostgreSQL is ready and without a startup probe; pods restart repeatedly. Fix: add a startup probe and readiness checks, and let the app retry the connection.
4. Add Services and an Ingress; call the API through the gateway.
5. Add resource requests and limits and an HPA on `orders`; run a rolling update while a load script runs and confirm no failed requests.

**Check:** What makes a rolling update lose no requests? *(Correct readiness probes, graceful shutdown, and surge capacity.)*

---

## MID-057-L10 · Demo: a crash-looping pod, diagnosed (12 min)
**Goal:** diagnose a broken deployment from evidence. Prepares the assessment debugging exercise.

**Steps**
1. `kubectl get pods` shows `orders` in `CrashLoopBackOff`.
2. `kubectl describe pod` shows restarts and the last state; events show no image problem.
3. `kubectl logs --previous` reveals a missing configuration value (database URL).
4. **Planned mistake:** raise memory limits as a guess because the pod "keeps dying". Fix: read the exit reason first; the exit code and logs point to configuration, not memory.
5. Correct the ConfigMap, roll the Deployment, confirm readiness, and write one line for the runbook.

**Check:** What should you read before changing limits? *(The last state reason, exit code, and previous logs.)*
