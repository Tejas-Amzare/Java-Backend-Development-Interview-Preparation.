# 2. Circuit Breaker, Feign, Kafka, RabbitMQ & Distributed Transactions

> 🔴 **Level:** Advanced | ⭐ **Interview Frequency:** High

---

## 🔌 OpenFeign (easy service-to-service calls)

Instead of writing REST client code, declare an interface and Feign does the HTTP call.
```java
@FeignClient(name = "payment-service")
public interface PaymentClient {
    @PostMapping("/pay")
    PaymentResponse pay(@RequestBody PaymentRequest req);
}
```
Call it like a normal method — Feign + service discovery find the service and make the call.

---

## ⚡ Circuit Breaker (Resilience4j)

### 🧠 Concept
If a service keeps failing, a **circuit breaker** stops calling it for a while (returns a
fallback), so failures don't cascade and bring down the whole system.

### States
```
CLOSED   → calls flow normally
   │ (too many failures)
OPEN     → calls blocked, fallback returned immediately
   │ (after wait time)
HALF-OPEN→ test a few calls → success? CLOSED : OPEN
```

```java
@CircuitBreaker(name = "payment", fallbackMethod = "fallback")
public String callPayment() { return paymentClient.pay(...); }

public String fallback(Exception e) { return "Payment service is down, try later"; }
```

Related patterns: **Retry**, **Timeout**, **Rate Limiter**, **Bulkhead**.

---

## 📨 Messaging: Kafka & RabbitMQ

Async communication — services send **messages/events** without waiting for a reply.

### Kafka
A **distributed event streaming** platform. High throughput, stores events in **topics**,
great for **event-driven** systems and big data.
```
Producer → Topic (partitions) → Consumer groups
```
- **Topic** = a category of messages.
- **Partition** = topic split for parallelism.
- **Consumer group** = consumers sharing the load.
- Keeps messages (log) → can replay.

### RabbitMQ
A **message broker** using **queues** and **exchanges**. Great for traditional task queues and
reliable delivery.

| Kafka | RabbitMQ |
|-------|----------|
| Event streaming, high throughput | Task queues, routing |
| Stores/replays messages | Deletes after consumed (usually) |
| Pull-based | Push-based |
| Big data, logs, analytics | Background jobs, RPC |

---

## 🔄 Distributed Transactions (Saga Pattern)

### 🧠 Problem
With a database per service, you **can't** use one ACID transaction across services.

### Solution: Saga
Break one big transaction into a **series of local transactions**, each with a
**compensating action** to undo if something fails.

```
Order created → Payment done → Stock reduced
      │              │              │ (fails!)
      └── refund ◄── cancel payment ◄─ compensate (undo previous steps)
```

Two styles:
- **Choreography** → services react to each other's events (no central coordinator).
- **Orchestration** → a central coordinator tells each service what to do.

---

## 📊 Monitoring & Observability
- **Centralized logging** → ELK stack (Elasticsearch, Logstash, Kibana).
- **Metrics** → Prometheus + Grafana.
- **Distributed tracing** → Zipkin / Sleuth / OpenTelemetry (follow a request across services).
- **Health checks** → Spring Boot Actuator.

---

## 🌍 Real-World Use Case
Placing an order triggers a Saga: reserve stock → charge payment → confirm order. If payment
fails, the Saga refunds/undoes previous steps. Kafka carries the events between services.

---

## ❓ Interview Questions
1. What is a circuit breaker? Explain its states.
2. What is OpenFeign?
3. Difference between Kafka and RabbitMQ?
4. What is a Kafka topic / partition / consumer group?
5. How do you handle transactions across microservices? (Saga)
6. Choreography vs orchestration Saga?
7. What is eventual consistency?
8. How do you monitor microservices? (Logging, metrics, tracing)
9. Sync vs async communication trade-offs?
10. What is idempotency and why does it matter in messaging?

---

## ✅ Best Practices
- Add circuit breakers, retries, and timeouts to remote calls.
- Prefer async events for loose coupling.
- Make message consumers **idempotent** (handle duplicates safely).
- Use distributed tracing to debug across services.

## ⚠️ Common Mistakes
- No fallback/timeout → one slow service freezes everything.
- Expecting strong consistency across services (it's eventual).
- Non-idempotent consumers → double-processing.

---

## ⚡ Quick Revision Notes
- Feign = declarative REST client. Circuit breaker = stop calling failing services (CLOSED/OPEN/HALF-OPEN).
- Kafka = event streaming (topics, replay); RabbitMQ = queues (task-based).
- Distributed transactions → Saga (local tx + compensations); choreography vs orchestration.
- Monitor with logging (ELK), metrics (Prometheus/Grafana), tracing (Zipkin).

## 🙋 FAQs
**Q: Why not 2-phase commit across microservices?** It's slow, blocking, and tightly couples services — Saga + eventual consistency is preferred.

## 📎 References
- Resilience4j docs, Apache Kafka docs
- microservices.io (patterns)

[⬅ Back to Microservices Index](./README.md)

