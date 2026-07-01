# 2. System Design Building Blocks

> 🔴 **Level:** Advanced | ⭐ **Interview Frequency:** High

---

## 🔴 Redis

### 🧠 Concept
**Redis** is a super-fast **in-memory** data store (key-value). Because data lives in RAM, reads/
writes take **microseconds**.

### Uses
| Use | Why |
|-----|-----|
| **Caching** | Store hot data to reduce DB load |
| **Session store** | Fast shared sessions across servers |
| **Rate limiting** | Count requests per user quickly |
| **Leaderboards** | Sorted sets rank scores |
| **Pub/Sub** | Simple messaging |
| **Distributed locks** | Coordinate across services |

Data types: String, List, Set, Sorted Set, Hash.
- **Persistence**: RDB (snapshots) + AOF (append log) so data survives restarts.

```
App → Redis (memory, ~0.1ms) instead of → DB (disk, ~10ms)
```

---

## 🗄️ Database Scaling

### Replication (copies)
```
        ┌─► Read Replica 1
Primary ─┼─► Read Replica 2   (reads spread across replicas)
(writes) └─► Read Replica 3
```
- **Primary** handles writes; **replicas** handle reads → scales reads.

### Sharding (partitioning)
Split data across multiple databases by a **shard key** (e.g., user_id).
```
users 1-1M   → DB Shard 1
users 1M-2M  → DB Shard 2
users 2M-3M  → DB Shard 3
```
Scales writes + storage, but adds complexity (cross-shard queries are hard).

### SQL vs NoSQL
| SQL | NoSQL |
|-----|-------|
| Structured, relations | Flexible schema |
| ACID, strong consistency | Scales horizontally easily |
| Joins | Denormalized |
| MySQL, Postgres | MongoDB, Cassandra, DynamoDB |

---

## 📨 Message Queue

### 🧠 Concept
A **message queue** lets services communicate **asynchronously** — the sender drops a message and
moves on; the receiver processes it later. Decouples services and smooths spikes.

```
Producer → [ Queue ] → Consumer
 (fast)     buffers      (processes at its own pace)
```

Benefits: decoupling, buffering traffic spikes, retries, reliability.
Tools: **Kafka**, **RabbitMQ**, **AWS SQS**.

Use: send emails, process orders, handle notifications without blocking the user.

---

## 🌐 CDN (Content Delivery Network)

### 🧠 Concept
A **CDN** is a network of servers spread worldwide that cache **static content** (images, CSS,
JS, videos) **close to users** → faster load times.

```
User in India → nearest CDN edge (Mumbai)  ← cached copy
                (instead of origin server in the US)
```

Benefits: lower latency, less load on origin, handles traffic spikes.
Providers: CloudFront, Cloudflare, Akamai.

---

## 🗺️ Putting It Together (typical scalable system)

```
        Users
          │
        [ CDN ]  → static content
          │
   [ Load Balancer ]
          │
   ┌──────┼──────┐
  App    App    App   (stateless, horizontally scaled)
   │      │      │
 [ Redis Cache ]      → hot data
   │
 [ DB Primary ] → replicas (reads) + shards (scale)
   │
 [ Message Queue ] → background workers (emails, reports)
```

---

## 🌍 Real-World Use Case
An e-commerce site: CDN serves product images, load balancer spreads traffic, Redis caches
product details, the DB uses read replicas, and a message queue handles order emails.

---

## ❓ Interview Questions
1. What is Redis? Why is it fast? Common use cases?
2. Difference between replication and sharding?
3. SQL vs NoSQL — when to use each?
4. What is a message queue? Benefits?
5. What is a CDN and how does it help?
6. How would you scale a read-heavy system? (Caching + read replicas)
7. How to scale a write-heavy system? (Sharding, queues)
8. What is eventual consistency in replication?
9. How does Redis persist data?
10. Cache-aside vs write-through?

---

## ✅ Best Practices
- Cache hot data in Redis; set TTLs.
- Use read replicas for read-heavy loads; shard for huge data.
- Use queues to decouple and absorb spikes.
- Serve static assets via CDN.

## ⚠️ Common Mistakes
- Treating Redis as the source of truth (it's a cache — can lose data).
- Sharding too early (adds needless complexity).
- Synchronous calls where a queue would be better.

---

## ⚡ Quick Revision Notes
- Redis = in-memory store for caching, sessions, rate limiting, leaderboards.
- Replication = copies for read scaling; sharding = split data for write scaling.
- Message queue = async, decoupled communication (Kafka/RabbitMQ/SQS).
- CDN = cache static content near users for speed.

## 🙋 FAQs
**Q: Redis vs database?** Redis = fast, in-memory cache (volatile); DB = durable source of truth.

## 📎 References
- redis.io/docs
- System Design Primer (GitHub)

[⬅ Back to System Design Index](./README.md)

