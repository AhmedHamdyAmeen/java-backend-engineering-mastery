# MID-036 · Service discovery — Lecture scripts

**Video:** 42 min · **Analogy used throughout:** a phone directory for the shop: you call "inventory", and the directory decides which of several numbers rings, skipping any that are out of service.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-036-L01 · Finding services (8 min)
**Goal:** explain why hard-coded addresses fail and the two discovery styles.

**Key points**
- Instances come and go (scaling, deploys, crashes); their IPs change.
- **Client-side discovery:** the client asks a registry for instances and picks one itself.
- **Server-side discovery:** the client calls a stable name or load balancer, which picks an instance.
- Both need to know which instances are healthy.
- Prefer what the platform already provides; add a registry only if you need one.

**Show**
| Style | Who picks the instance | Example |
| --- | --- | --- |
| Client-side | the caller | Eureka, Consul + client library |
| Server-side | a proxy or platform | Compose DNS, Kubernetes Service |

**Check:** Why is `http://10.0.0.17:8080` a poor service address? *(The instance may move, die, or be replaced.)*

---

## MID-036-L02 · DNS-based discovery (8 min)
**Goal:** use DNS names for service-to-service calls.

**Key points**
- In Docker Compose, every service name is a DNS name on the Compose network: `http://inventory:8080`.
- With several replicas, the name resolves to the replicas' addresses (Docker's internal DNS rotates among them).
- Clients and JVMs may cache DNS results; check the JVM's DNS cache TTL and connection pooling (verify settings before recording).
- Pooled keep-alive connections stay on one replica until closed, which skews balancing.
- No library needed: configuration is just a hostname.

**Show**
```yaml
services:
  inventory:
    image: shop/inventory
    deploy: { replicas: 3 }
  orders:
    environment:
      INVENTORY_URL: http://inventory:8080
```

**Check:** What does `orders` need to know to reach `inventory`? *(Only the name `inventory` and the port.)*

---

## MID-036-L03 · Platform-native discovery (8 min)
**Goal:** see how Kubernetes handles discovery (detail in MID-057).

**Key points**
- A Kubernetes **Service** gives a stable virtual IP and DNS name (`inventory.shop.svc`) in front of changing Pods.
- Only Pods that pass their **readiness probe** receive traffic.
- Rolling deployments add new Pods and remove old ones while keeping the name stable.
- Registries such as Eureka are mostly unnecessary on such a platform.
- A service mesh (SRB-009) can add smarter balancing and retries outside the application.

**Show:** diagram: `orders` Pod → Service `inventory` → Pods A, B, C (C failing readiness and excluded).

**Check:** Which mechanism keeps unhealthy Pods out of rotation? *(Readiness probes.)*

---

## MID-036-L04 · Load-balancing strategies (8 min)
**Goal:** choose a balancing strategy and understand health-driven routing.

**Key points**
- **Round robin:** simple and even for similar requests.
- **Least connections:** better when request durations vary.
- **Random, or power of two choices:** cheap and effective at scale.
- **Sticky sessions:** pins a client to an instance; avoid by keeping services stateless.
- **Health checks:** remove failed instances. In-flight requests to a dying instance can still fail, so use graceful shutdown and connection draining.

**Show**
| Strategy | Good when | Watch for |
| --- | --- | --- |
| Round robin | uniform requests | long requests pile up |
| Least connections | varied durations | needs connection tracking |
| Sticky | stateful legacy | uneven load, failover loss |

**Check:** What limits errors during a deployment? *(Readiness-based routing plus graceful shutdown that drains in-flight requests.)*

---

## MID-036-L05 · Demo: scaling inventory to three replicas (10 min)
**Goal:** scale out behind Compose DNS and watch a replica die. Prepares MID-036-LAB1.

**Steps**
1. Start Shop with `docker compose up --scale inventory=3`; remove fixed host port mappings from `inventory`.
2. Call `inventory` from `orders` repeatedly and log the replica's hostname; show requests spread across three.
3. Run a load test; kill one replica mid-run.
4. **Planned mistake:** hard-code one replica's IP in `orders` config. When that replica dies, every call fails. Fix: use the service name.
5. Show errors limited to requests in flight on the killed replica; explain why (already sent, not yet rerouted) and how retries on idempotent calls plus graceful shutdown reduce it.
