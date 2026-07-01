# 1. System Design Fundamentals

> 🔴 **Level:** Advanced | ⭐ **Interview Frequency:** High

---

## 🧠 HLD vs LLD

| High-Level Design (HLD) | Low-Level Design (LLD) |
|-------------------------|------------------------|
| Big picture / architecture | Detailed class & method design |
| Components, databases, flow | Classes, interfaces, patterns |
| "What are the parts?" | "How is each part built?" |
| Diagrams of services | UML, code structure |

---

## 📈 Scalability

**Scalability** = the ability to handle **more load** by adding resources.

| Vertical Scaling (Scale Up) | Horizontal Scaling (Scale Out) |
|-----------------------------|--------------------------------|
| Bigger machine (more CPU/RAM) | More machines |
| Simple, but has a limit | Nearly unlimited |
| Single point of failure | Fault tolerant |
| Expensive at the top | Cheaper commodity servers |

```
Vertical:  [small] → [BIG server]
Horizontal:[server] → [server][server][server]
```

Key ideas: **stateless services** scale easily; store state in DB/cache, not in the app.

---

## ⚖️ Load Balancer

Distributes incoming requests across multiple servers so no single server is overwhelmed.

```
             ┌─► Server 1
Client → LB ─┼─► Server 2
             └─► Server 3
```

Algorithms: **Round Robin**, **Least Connections**, **IP Hash**, **Weighted**.
Benefits: high availability, no single point of failure, better performance.

---

## 🚀 Caching

Store frequently-used data in **fast memory** to avoid slow repeated work (DB calls, computations).

```
Request → Cache? ── hit ──► return fast
             │
             miss → DB → store in cache → return
```

- **Cache hit** = found in cache (fast). **Cache miss** = not found (go to DB).
- Strategies: **Cache-aside** (most common), Write-through, Write-back.
- **Eviction**: LRU (Least Recently Used), LFU, TTL (expiry).
- Where: browser, CDN, application (Redis/Memcached), database.

> ⚠️ **Cache invalidation** (keeping cache fresh) is one of the hard problems in CS.

---

## 🧭 CAP Theorem (must know!)

In a distributed system, you can only fully guarantee **2 of 3**:

```
        Consistency
           /  \
          /    \
   Availability──Partition Tolerance
```

| Letter | Meaning |
|--------|---------|
| **C** onsistency | Every read gets the latest write |
| **A** vailability | Every request gets a response |
| **P** artition tolerance | Works despite network failures |

Since network partitions **will** happen, you really choose between **C** and **A**:
- **CP** systems → consistency first (e.g., traditional RDBMS, MongoDB in some modes).
- **AP** systems → availability first (e.g., Cassandra, DynamoDB).

---

## 🌍 Real-World Use Case
A social media feed: load balancer spreads traffic across app servers (horizontal scaling),
Redis caches hot feeds, and the system favors availability (AP) so it never fully goes down.

---

## ❓ Interview Questions
1. Difference between HLD and LLD?
2. Vertical vs horizontal scaling?
3. What is a load balancer? Common algorithms?
4. What is caching? Cache hit vs miss?
5. Explain cache eviction (LRU) and invalidation.
6. Explain the CAP theorem.
7. What does "stateless" mean and why does it help scaling?
8. What is a single point of failure? How to avoid it?
9. Latency vs throughput?
10. What is eventual consistency?

---

## ✅ Best Practices
- Keep services **stateless** to scale horizontally.
- Cache read-heavy data; plan invalidation.
- Add load balancers + multiple instances (no single point of failure).
- Know your consistency needs (CP vs AP).

## ⚠️ Common Mistakes
- Storing session state in the app server (breaks horizontal scaling).
- Caching everything (stale data, complexity).
- Ignoring failure scenarios.

---

## ⚡ Quick Revision Notes
- HLD = architecture; LLD = class-level detail.
- Scale up (bigger box) vs scale out (more boxes); prefer stateless + horizontal.
- Load balancer spreads traffic (round robin, least connections).
- Cache = fast memory for hot data (LRU eviction, cache-aside).
- CAP: pick C or A during a network partition.

## 🙋 FAQs
**Q: Why can't we have all of C, A, and P?** During a network partition you must choose to either stay consistent (reject some requests) or stay available (risk stale data).

## 📎 References
- *Designing Data-Intensive Applications* by Martin Kleppmann
- System Design Primer (GitHub)

[⬅ Back to System Design Index](./README.md)

