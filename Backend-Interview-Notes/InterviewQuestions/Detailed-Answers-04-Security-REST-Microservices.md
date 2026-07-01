# 🎤 Detailed Spoken Answers — Security, REST & Microservices

> Model answers to **speak out loud**. Formula: `Definition → Example → Why it matters.`

---

## 1. What is the difference between authentication and authorization? 🔥

> "These two sound similar but are different steps.
>
> **Authentication** answers **'Who are you?'** — it verifies identity, usually with a username
> and password. **Authorization** answers **'What are you allowed to do?'** — it checks
> permissions after we know who the user is.
>
> A simple analogy: at an airport, showing your passport is **authentication**, and your boarding
> pass deciding which flight and seat you can access is **authorization**. In Spring Security,
> authentication happens first, and then authorization rules like `hasRole('ADMIN')` decide what
> endpoints the user can reach."

---

## 2. How does JWT work and why is it stateless? 🔥

> "JWT, a JSON Web Token, is a **signed token** the server gives the client after a successful
> login. It has three parts separated by dots — a **header** with the algorithm, a **payload**
> with the user's claims like id and role, and a **signature** that verifies the token hasn't
> been tampered with.
>
> The flow is: the user logs in, the server returns a JWT, and the client sends it back on every
> request in the `Authorization: Bearer` header. The server just **verifies the signature** —
> it doesn't need to store any session.
>
> That's why it's **stateless** — all the information is inside the token, so the server keeps
> nothing in memory. This makes it **scale beautifully** across multiple servers, because any
> server can validate the token. One caution: the payload is only encoded, not encrypted, so I
> never put secrets in it, and I keep tokens short-lived with a refresh token for renewal."

---

## 3. Why do we hash passwords, and why BCrypt? 🔥

> "I never store passwords in plain text, because if the database is ever leaked, all accounts
> are exposed. Instead, I **hash** them — a one-way transformation that can't be reversed.
>
> I use **BCrypt** specifically because it's **slow by design** and adds a random **salt** to
> each password. The salt means two users with the same password get **different hashes**, which
> defeats precomputed 'rainbow table' attacks. And being slow makes brute-force attacks
> impractical.
>
> On login, I don't decrypt anything — I hash the entered password the same way and compare it to
> the stored hash using `passwordEncoder.matches()`. Hashing is one-way, unlike encryption which
> is two-way and reversible."

---

## 4. What is OAuth2 and how is it different from JWT? ⭐

> "**OAuth2** is an **authorization protocol** that lets users grant an app access to their data
> on another service — without sharing their password. That's what powers 'Login with Google' or
> 'Login with GitHub'. Google authenticates the user and gives my app a token to trust.
>
> **JWT**, on the other hand, is just a **token format** — a way to represent claims in a signed
> token. They're often used together: OAuth2 can issue tokens that happen to be JWTs.
>
> So the key difference is: OAuth2 is the **protocol/flow**, and JWT is a **token format**. One
> is *how* access is delegated, the other is *what the token looks like*."

---

## 5. What is the difference between CORS and CSRF? 🔥 (commonly confused)

> "They sound similar but solve opposite problems.
>
> **CORS**, Cross-Origin Resource Sharing, is about **which other domains are allowed to call my
> API**. Browsers block cross-origin requests by default, so if my React frontend on one domain
> needs to call my backend on another, I configure CORS to allow that specific origin.
>
> **CSRF**, Cross-Site Request Forgery, is a **security attack** where a logged-in user is tricked
> into making an unwanted request using their existing session. Spring protects against it with a
> CSRF token.
>
> The practical rule: for **session-based** apps I keep CSRF **enabled**, but for **stateless JWT
> APIs** I usually **disable** CSRF because there's no session cookie to exploit. So CORS controls
> *who can call*, and CSRF protection prevents *forged requests*."

---

## 6. What are the principles of a RESTful API? 🔥

> "REST is an architectural style for APIs built on top of HTTP. The main principles are:
>
> It's **stateless** — each request contains everything the server needs, and the server stores
> no client session between requests. It's **resource-based** — everything is a resource
> identified by a URL, like `/users/1`. It uses **standard HTTP methods** with clear meaning —
> GET to read, POST to create, PUT and PATCH to update, DELETE to remove. It uses proper **HTTP
> status codes** — 200, 201, 400, 404, 500 — to communicate results. And it has a **uniform
> interface**, so the API is predictable and consistent.
>
> Following these makes the API easy for any client to understand and integrate with."

---

## 7. What are microservices and how do they differ from a monolith? 🔥

> "A **monolith** is a single, large application where all the features live in one codebase and
> deploy together. **Microservices** break that into many **small, independent services**, each
> responsible for one business capability, communicating over the network.
>
> The advantages of microservices are **independent scaling** — I can scale just the payment
> service during a sale — **independent deployment**, **fault isolation** so one service failing
> doesn't crash everything, and **technology flexibility** per service. Each service also owns its
> **own database**.
>
> The trade-off is **complexity** — distributed systems bring network failures, data consistency
> challenges, and harder debugging. So for a small app, a monolith is often the better, simpler
> choice; microservices shine at large scale with multiple teams."

---

## 8. What is a circuit breaker and why is it needed? ⭐

> "In microservices, if one service keeps failing or is slow, calls to it can pile up and drag
> down the whole system. A **circuit breaker** prevents that cascade.
>
> It works like an electrical breaker with three states. In **CLOSED** state, calls flow
> normally. If failures cross a threshold, it trips to **OPEN**, and further calls fail fast and
> return a **fallback** immediately instead of waiting. After a wait period, it moves to
> **HALF-OPEN**, letting a few test calls through — if they succeed, it closes again; if not, it
> reopens.
>
> I implement this with a library like **Resilience4j**, along with retries and timeouts. It
> keeps my system resilient when a dependency is down."

---

## 9. What is the difference between Kafka and RabbitMQ? ⭐

> "Both are messaging systems for **asynchronous** communication, but they're built for different
> use cases.
>
> **Kafka** is a **distributed event-streaming platform**. It stores messages in **topics** as a
> durable log, so consumers can **replay** them, and it handles **very high throughput** — it's
> great for event-driven architectures, analytics, and big data pipelines.
>
> **RabbitMQ** is a traditional **message broker** using **queues** and exchanges, with flexible
> routing. Messages are typically removed once consumed. It's ideal for **task queues** and
> background jobs where reliable delivery and routing matter more than replay.
>
> So I reach for Kafka for high-volume event streaming, and RabbitMQ for classic job/task
> processing."

---

## 10. How do you handle transactions across microservices? ⭐ (advanced)

> "With a database per service, I **can't** use a single ACID transaction across services. So I
> use the **Saga pattern**.
>
> A Saga breaks one big transaction into a **series of local transactions**, one per service, and
> each step has a **compensating action** to undo it if a later step fails. For example, placing
> an order: reserve stock, then charge payment, then confirm the order. If payment fails, the
> Saga triggers a compensation to release the reserved stock.
>
> There are two styles: **choreography**, where services react to each other's events, and
> **orchestration**, where a central coordinator directs each step. This gives **eventual
> consistency** instead of immediate consistency — which is the realistic trade-off in
> distributed systems."

---

## 11. What is Redis and what are its common use cases? ⭐

> "Redis is a **super-fast in-memory key-value data store**. Because the data lives in RAM,
> reads and writes take microseconds — far faster than hitting a disk-based database.
>
> I use it for several things: **caching** frequently-read data to reduce database load,
> **session storage** shared across servers, **rate limiting** by counting requests per user,
> **leaderboards** using its sorted sets, and simple **pub/sub** messaging or distributed locks.
>
> It also supports persistence through snapshots and an append-only log, so data can survive
> restarts. But I treat it as a **cache, not the source of truth** — the real data always lives
> in my primary database."

---

## 🗣️ Speaking Tips for Security & Microservices Rounds
- For security, always mention **best practices** (hash passwords, short-lived tokens, HTTPS).
- For microservices, acknowledge the **trade-offs** — it shows maturity, not just buzzwords.
- Use the phrase **"eventual consistency"** correctly — it impresses senior interviewers.
- When comparing tools (Kafka vs RabbitMQ), give a **clear 'use this when' rule**.

[⬅ Back to Questions Index](./README.md) · [Full Security/REST/Microservices Q Bank](./04-Security-REST-Microservices.md)

