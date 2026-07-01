# 📋 All-in-One Quick Revision Cheat Sheet

The fastest way to revise everything before an interview.

---

## ☕ Java Core

- **OOP (A PIE):** Abstraction, Polymorphism, Inheritance, Encapsulation.
- **Class** = blueprint, **Object** = instance (heap). Objects created with `new`.
- **Overloading** = compile-time (same class, diff params); **Overriding** = runtime (child redefines).
- **Abstract class** = shared code, single inheritance; **Interface** = contract, multiple.
- `==` compares references; `.equals()` compares values.
- **String** immutable → use `StringBuilder` for edits.
- **Checked** = compile-time (must handle); **Unchecked** = runtime.
- `final` (constant) vs `finally` (always runs) vs `finalize` (before GC).

### Collections
| Need | Use |
|------|-----|
| Ordered + duplicates | ArrayList |
| Fast add/remove | LinkedList |
| Unique | HashSet |
| Unique + sorted | TreeSet |
| Key-value | HashMap |
| Key-value sorted | TreeMap |
| Priority | PriorityQueue |

- HashMap: hashCode → bucket, equals → key match, load factor 0.75.
- ArrayList = O(1) access; LinkedList = O(1) insert/delete.
- Comparable (`compareTo`, 1 order) vs Comparator (`compare`, many orders).

### Concurrency
- `Runnable` > extending `Thread`. Use `start()`, not `run()`.
- `synchronized` prevents race conditions; deadlock = mutual waiting.
- Use `ExecutorService` (thread pools). `ConcurrentHashMap` for thread-safe maps.

### Streams / JVM
- Stream: source → intermediate (lazy: filter/map) → terminal (collect/forEach).
- `Optional` avoids null. Lambda = `(x) -> x*2`.
- JDK ⊃ JRE ⊃ JVM. `.java` → bytecode → JVM. Heap = objects, Stack = calls.
- GC auto-frees unreferenced objects (Young → Old gen).

---

## 🗄️ SQL

- CRUD = INSERT / SELECT / UPDATE / DELETE.
- **PK** = unique + not null (one); **FK** = links to another table's PK.
- DELETE (rows, rollback) vs TRUNCATE (all, fast) vs DROP (table).
- **Joins:** INNER (match), LEFT (all left + match), RIGHT, FULL.
- **Normalization:** 1NF (atomic), 2NF (full PK dependency), 3NF (no transitive dep).
- **ACID:** Atomicity, Consistency, Isolation, Durability.
- **Index** = fast lookup (B-tree), speeds reads, slows writes.
- WHERE (before grouping) vs HAVING (after grouping).
- 2nd highest salary: `SELECT MAX(salary) WHERE salary < (SELECT MAX(salary)...)`.
- Window: `RANK() OVER (PARTITION BY dept ORDER BY salary DESC)`.

---

## 🌱 Spring / Spring Boot

- **IoC** = Spring controls object creation; **DI** = injects dependencies (prefer constructor).
- Stereotypes: `@Component`/`@Service`/`@Repository`/`@Controller`.
- Default bean scope = **singleton**; prototype = new each time.
- `@SpringBootApplication` = `@Configuration` + `@EnableAutoConfiguration` + `@ComponentScan`.
- Layers: Controller → Service → Repository → DB. Use **DTOs**.
- `@RestController` = `@Controller` + `@ResponseBody`.
- `@PathVariable` (path), `@RequestParam` (query), `@RequestBody` (JSON).
- Global errors: `@RestControllerAdvice` + `@ExceptionHandler`.
- Status: 200 OK, 201 Created, 400 Bad Request, 401, 403, 404, 500.
- AOP = cross-cutting concerns (logging, `@Transactional`).

---

## 🐘 Hibernate / JPA

- ORM = objects ↔ tables. JPA = spec, Hibernate = implementation.
- States: Transient → Persistent → Detached → Removed.
- Fetch: EAGER (now) vs LAZY (on access) — prefer LAZY.
- Relationships: `@OneToMany`, `@ManyToOne`, `@ManyToMany`; `mappedBy` = non-owning side.
- **N+1 problem** → fix with `JOIN FETCH` / `@EntityGraph`.
- Optimistic lock = `@Version`; Pessimistic = lock row.

---

## 🔐 Security

- AuthN (who you are) vs AuthZ (what you can do).
- Hash passwords with **BCrypt** (salted, one-way).
- **JWT** = `header.payload.signature`, stateless, sent as `Bearer`.
- OAuth2 = login via Google/GitHub.
- `@PreAuthorize("hasRole('ADMIN')")` for method security.
- CORS = who can call API; CSRF = block forged requests (disable for stateless JWT).

---

## 🧩 Microservices / System Design

- Microservices = small independent services; API Gateway = entry; Eureka = discovery.
- Circuit breaker: CLOSED → OPEN → HALF-OPEN.
- Kafka = event streaming; RabbitMQ = queues.
- Saga = distributed transactions (local tx + compensation).
- Scale: vertical (bigger) vs horizontal (more); keep **stateless**.
- Cache (Redis) for hot data; LB spreads traffic; CDN for static.
- **CAP:** pick C or A during a partition.

---

## 🧮 DSA Complexity

- O(1) < O(log n) < O(n) < O(n log n) < O(n²) < O(2ⁿ) < O(n!).
- HashMap O(1), Binary search O(log n), nested loop O(n²).
- Patterns: Two Pointer (sorted), Sliding Window (subarray), Binary Search (sorted).
- BFS = queue (shortest path), DFS = recursion/stack.
- DP = store subproblems; Greedy = best local pick; Backtracking = choose/explore/undo.

---

## 🌿 Git

- Flow: edit → `add` → `commit` → `push`.
- Merge (keeps history) vs Rebase (linear). Reset (rewrites) vs Revert (safe undo).
- `cherry-pick` = one commit; `stash` = shelve changes; PR = reviewed merge.
- `fetch` (download) vs `pull` (download + merge).

---

## 🐳 Docker / ☸️ K8s

- Docker: Dockerfile → Image → Container. Volumes = persistence, Compose = multi-container.
- K8s: Pod (smallest) → Deployment (manages/heals) → Service (stable access).
- ConfigMap (config), Secret (sensitive), Ingress (HTTP routing), HPA (autoscaling).

---

> ⭐ Read this twice and you're interview-ready. Good luck!

[⬅ Back to Cheat Sheets Index](./README.md)

