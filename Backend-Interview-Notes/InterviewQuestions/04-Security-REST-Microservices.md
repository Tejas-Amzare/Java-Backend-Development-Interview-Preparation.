# 04 — Security, REST & Microservices Interview Questions (100+)

---

## 🔐 Spring Security (1–30)

1. **Authentication vs authorization?** Who you are vs what you can do.
2. **How does Spring Security work?** A chain of filters before your controller.
3. **What is the SecurityFilterChain?** The ordered filters that process each request.
4. **What is UserDetailsService?** Loads user data for authentication.
5. **What is SecurityContext?** Holds the current authenticated user.
6. **What is AuthenticationManager?** Processes authentication requests.
7. **Why hash passwords?** So stored passwords can't be read if leaked.
8. **What is BCrypt?** A salted, slow one-way hashing algorithm.
9. **Hashing vs encryption?** One-way (irreversible) vs two-way (reversible).
10. **What is a salt?** Random data added so identical passwords hash differently.
11. **Stateful vs stateless auth?** Server sessions vs tokens (JWT).
12. **What is JWT?** A signed stateless token: header.payload.signature.
13. **JWT parts?** Header (algo), payload (claims), signature (verify).
14. **Why is JWT stateless?** Server stores nothing; all info is in the token.
15. **How is JWT sent?** `Authorization: Bearer <token>`.
16. **Where to store JWT on client?** HttpOnly cookie or memory (avoid localStorage).
17. **What is a refresh token?** Long-lived token to get new access tokens.
18. **What is OAuth2?** Delegated login via a provider (Google/GitHub).
19. **OAuth2 vs JWT?** Protocol vs token format.
20. **OAuth2 roles?** Resource owner, client, auth server, resource server.
21. **What is OpenID Connect?** Identity layer on top of OAuth2.
22. **Role vs authority?** Group (ADMIN) vs fine-grained permission.
23. **What is method security?** `@PreAuthorize`/`@PostAuthorize` on methods.
24. **What is @PreAuthorize?** Checks access before a method runs.
25. **What is CORS?** Controls which origins can call your API.
26. **How to enable CORS?** `@CrossOrigin` or a global CORS config.
27. **What is CSRF?** Forged requests using a user's session.
28. **When to disable CSRF?** Stateless APIs (JWT, no cookies/session).
29. **CORS vs CSRF?** Who can call vs preventing forged requests.
30. **How to secure endpoints by role?** `.requestMatchers("/admin/**").hasRole("ADMIN")`.

---

## 🌐 REST API (31–55)

31. **What is REST?** An architecture style using HTTP + resources.
32. **REST principles?** Stateless, client-server, resource-based, uniform interface, cacheable.
33. **Is REST stateless?** Yes — each request is independent.
34. **HTTP methods?** GET, POST, PUT, PATCH, DELETE.
35. **Idempotent methods?** GET, PUT, DELETE (same result if repeated).
36. **Is POST idempotent?** No.
37. **What is a resource?** An entity exposed via a URL (e.g., /users/1).
38. **What is a URI?** The address identifying a resource.
39. **Path param vs query param?** Identify a resource vs filter/options.
40. **What is content negotiation?** Choosing response format (JSON/XML) via headers.
41. **What is HATEOAS?** Responses include links to related actions.
42. **REST vs SOAP?** Lightweight JSON/HTTP vs heavy XML protocol.
43. **REST vs GraphQL?** Fixed endpoints vs client-specified queries.
44. **What is versioning?** URL (/v1), header, or param to evolve APIs.
45. **What status for created?** 201 Created.
46. **What status for validation error?** 400 Bad Request.
47. **What status for not authenticated?** 401 Unauthorized.
48. **What status for no permission?** 403 Forbidden.
49. **What status for not found?** 404 Not Found.
50. **What status for server error?** 500.
51. **What is pagination?** Returning data in pages, not all at once.
52. **What is rate limiting?** Restricting requests per user/time.
53. **What is an API Gateway?** Single entry for routing/auth/rate limiting.
54. **What is idempotency key?** Prevents duplicate processing of the same request.
55. **Best practice for API errors?** Consistent JSON error format + proper status.

---

## 🧩 Microservices, Kafka & Redis (56–100)

56. **What are microservices?** Small, independent, single-purpose services.
57. **Monolith vs microservices?** One app vs many small services.
58. **Pros of microservices?** Independent scaling/deploy, fault isolation, tech flexibility.
59. **Cons of microservices?** Complexity, distributed data, network issues.
60. **What is service discovery?** Services find each other by name (Eureka).
61. **What is a config server?** Central config for all services.
62. **What is a load balancer?** Spreads traffic across instances.
63. **Client vs server-side load balancing?** Caller picks instance vs a central LB.
64. **What is OpenFeign?** Declarative REST client for service calls.
65. **What is a circuit breaker?** Stops calling a failing service (fallback).
66. **Circuit breaker states?** CLOSED, OPEN, HALF-OPEN.
67. **What is Resilience4j?** A library for circuit breaker/retry/rate limiter.
68. **What is a retry pattern?** Automatically re-attempt failed calls.
69. **What is a bulkhead?** Isolate resources so one failure doesn't sink all.
70. **Sync vs async communication?** REST (wait) vs messaging (fire-and-forget).
71. **Why database per service?** Loose coupling and independent scaling.
72. **What is eventual consistency?** Data becomes consistent over time.
73. **What is the Saga pattern?** Distributed tx via local steps + compensation.
74. **Choreography vs orchestration?** Event-driven vs central coordinator.
75. **What is idempotency in messaging?** Safe handling of duplicate messages.
76. **What is Kafka?** A distributed event streaming platform.
77. **What is a Kafka topic?** A named stream of messages.
78. **What is a partition?** A topic split for parallelism.
79. **What is a consumer group?** Consumers sharing a topic's load.
80. **What is an offset?** A message's position in a partition.
81. **Kafka vs RabbitMQ?** Event streaming (replay) vs task queues.
82. **What is a producer/consumer?** Sends / reads messages.
83. **Why use messaging?** Decoupling, buffering, reliability.
84. **What is Redis?** An in-memory key-value data store.
85. **Why is Redis fast?** Data lives in RAM.
86. **Redis use cases?** Caching, sessions, rate limiting, leaderboards, pub/sub.
87. **Redis data types?** String, List, Set, Sorted Set, Hash.
88. **How does Redis persist data?** RDB snapshots + AOF log.
89. **What is cache-aside?** App checks cache, loads from DB on miss.
90. **What is write-through cache?** Write to cache and DB together.
91. **What is TTL?** Time-to-live expiry for a cache entry.
92. **What is LRU eviction?** Remove least recently used items.
93. **What is distributed caching?** Cache shared across servers (Redis cluster).
94. **How to monitor microservices?** Logging (ELK), metrics (Prometheus/Grafana), tracing (Zipkin).
95. **What is distributed tracing?** Following a request across services.
96. **What is Spring Cloud Gateway?** Reactive API gateway for routing/filters.
97. **What is a correlation ID?** An ID to trace one request across services.
98. **How to handle a service failure?** Circuit breaker + fallback + retry + timeout.
99. **What is blue-green deployment?** Two environments to switch traffic safely.
100. **What is canary deployment?** Release to a small % of users first.

[⬅ Back to Questions Index](./README.md)

