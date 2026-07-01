# 1. Microservices Architecture & Core Components

> 🔴 **Level:** Advanced | 🔥 **Interview Frequency:** Very High

---

## 🧠 Concept

**Microservices** = building an app as many **small, independent services**, each doing **one
job** and running/deploying separately. Opposite of a **monolith** (one big app).

---

## 💬 Simple Explanation

A **monolith** is one big shop where everything is together — if one section breaks, the shop
closes. **Microservices** are like a mall with separate stores — one store can close/upgrade
without shutting the whole mall.

---

## 📋 Monolith vs Microservices

| Monolith | Microservices |
|----------|---------------|
| One codebase/deploy | Many small services |
| Simple to start | Complex to manage |
| Scale whole app | Scale each service |
| One tech stack | Different stacks allowed |
| One failure can crash all | Failures isolated |
| One DB | DB per service |

---

## 🗺️ Architecture Diagram

```
                 ┌──────────────┐
   Client ─────► │ API Gateway  │  (single entry, routing, auth)
                 └──────┬───────┘
          ┌────────────┼─────────────┐
          ▼            ▼              ▼
     User Service  Order Service  Payment Service
        │             │              │
     User DB       Order DB       Payment DB    (DB per service)

   Supporting infra:
   - Service Discovery (Eureka)  → find services
   - Config Server               → central config
   - Load Balancer               → spread traffic
```

---

## 🧱 Core Components

### 1. API Gateway (Spring Cloud Gateway)
Single entry point for all clients. Handles **routing, authentication, rate limiting, logging**.
```
Client → Gateway → correct microservice
```

### 2. Service Discovery (Eureka)
Services **register** themselves; others **look them up** by name (not hardcoded IPs).
```
Order Service asks Eureka: "Where is Payment Service?" → gets its address
```

### 3. Config Server
Stores configuration **centrally** (often in Git) so all services read from one place.

### 4. Load Balancer
Spreads requests across multiple instances of a service (client-side with Spring Cloud
LoadBalancer, or server-side).

### 5. Communication
- **Synchronous** → REST / OpenFeign (wait for response).
- **Asynchronous** → Kafka / RabbitMQ (fire and forget, events).

---

## 🌍 Real-World Use Case
Amazon/Netflix-style systems: separate services for users, catalog, orders, payments,
recommendations — each scaled and deployed independently by different teams.

---

## ❓ Interview Questions
1. What are microservices? Pros and cons vs monolith?
2. What is an API Gateway? Why use it?
3. What is service discovery? Why not hardcode URLs?
4. How do microservices communicate?
5. Why "database per service"?
6. Synchronous vs asynchronous communication?
7. What is a config server?
8. Challenges of microservices? (Distributed data, network failures, monitoring, complexity)
9. What is the Saga pattern? (Distributed transactions — see next file)

---

## ✅ Best Practices
- One service = one business capability.
- Each service owns its own database.
- Design for failure (retries, timeouts, circuit breakers).
- Centralize logging and monitoring.
- Keep services loosely coupled (events).

## ⚠️ Common Mistakes
- Making services too small ("nano-services") → too much network chatter.
- Sharing a database between services (tight coupling).
- No monitoring/tracing → impossible to debug.
- Ignoring network failures.

---

## ⚡ Quick Revision Notes
- Microservices = small, independent, single-purpose services.
- API Gateway = single entry (routing/auth). Eureka = service discovery.
- Config Server = central config; Load Balancer = spread traffic.
- Communicate via REST/Feign (sync) or Kafka/RabbitMQ (async).
- DB per service; design for failure.

## 🙋 FAQs
**Q: When NOT to use microservices?** Small apps/teams — a monolith is simpler and faster to build.

## 📎 References
- Spring Cloud docs
- *Building Microservices* by Sam Newman

[⬅ Back to Microservices Index](./README.md)

