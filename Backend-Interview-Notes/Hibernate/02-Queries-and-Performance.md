# 2. Queries, N+1 Problem, Locking & Performance

> 🔴 **Level:** Advanced | ⭐ **Interview Frequency:** High

---

## 🔎 Ways to Query Data

### 1. Derived Query Methods (Spring Data JPA)
Just name the method — Spring writes the query.
```java
public interface UserRepository extends JpaRepository<User, Long> {
    List<User> findByName(String name);
    List<User> findByAgeGreaterThan(int age);
    Optional<User> findByEmail(String email);
}
```

### 2. JPQL (Java Persistence Query Language)
Object-oriented queries (uses **entity names**, not table names).
```java
@Query("SELECT u FROM User u WHERE u.age > :age")
List<User> findOlderThan(@Param("age") int age);
```

### 3. Native Query (raw SQL)
```java
@Query(value = "SELECT * FROM users WHERE age > ?1", nativeQuery = true)
List<User> findOlder(int age);
```

### 4. Criteria API (programmatic, type-safe)
Build queries in Java code — good for **dynamic** queries.

### 5. Specifications
Reusable, combinable query conditions (great for dynamic filters/search).
```java
repo.findAll(Specification.where(hasName("Aman")).and(olderThan(18)));
```

| Approach | When to use |
|----------|-------------|
| Derived methods | Simple queries |
| JPQL | Custom, portable queries |
| Native SQL | DB-specific features |
| Criteria / Specifications | Dynamic queries built at runtime |

---

## 🐛 The N+1 Problem (very important!)

### What is it?
When loading a list and its related data **lazily**, Hibernate runs **1 query for the list +
N queries** (one per item) for the related data → many round trips → slow.

```
1 query : SELECT * FROM users;              (10 users)
+10 queries: SELECT * FROM orders WHERE user_id = ?  (for each user!)
= 11 queries instead of 1-2
```

### How to fix
```java
// 1. JOIN FETCH - loads users + orders in ONE query
@Query("SELECT u FROM User u JOIN FETCH u.orders")
List<User> findAllWithOrders();

// 2. @EntityGraph
@EntityGraph(attributePaths = "orders")
List<User> findAll();

// 3. Batch fetching (application.properties)
// spring.jpa.properties.hibernate.default_batch_fetch_size=20
```

---

## 🔒 Locking (concurrency control)

Prevents two transactions from corrupting the same data.

| Type | Idea | Use when |
|------|------|----------|
| **Optimistic** | No lock; check a `@Version` field on update | Low conflict |
| **Pessimistic** | Lock the row until done | High conflict |

```java
@Entity
public class Account {
    @Version                     // optimistic locking
    private int version;
}
```
If two users update the same row, the second gets an `OptimisticLockException` → retry.

---

## ⚡ Performance Optimization Tips
1. Use **LAZY** fetching + `JOIN FETCH` / `@EntityGraph` to avoid N+1.
2. Use **pagination** (`Pageable`) for large lists.
3. Enable **second-level cache** for read-heavy, rarely-changing data.
4. Select only needed columns via **DTO projections**.
5. Batch inserts/updates (`hibernate.jdbc.batch_size`).
6. Avoid EAGER on collections.
7. Use **read-only** transactions for queries.

---

## ❓ Interview Questions
1. Difference between JPQL and native query?
2. What is the N+1 problem? How to fix it?
3. What is `JOIN FETCH` / `@EntityGraph`?
4. Difference between optimistic and pessimistic locking?
5. What is `@Version` used for?
6. First-level vs second-level cache? (L1 = session scope, on by default; L2 = across sessions)
7. What are DTO projections?
8. How to improve Hibernate performance?
9. Difference between `get()` and `load()` in Hibernate? (get = eager/null; load = lazy proxy)

---

## ✅ Best Practices
- Always watch for and fix N+1 problems.
- Use optimistic locking for most web apps.
- Paginate; never load huge tables at once.
- Use projections/DTOs for read queries.

## ⚠️ Common Mistakes
- Ignoring N+1 until production slows down.
- EAGER collections causing giant joins.
- Not handling `OptimisticLockException`.

---

## ⚡ Quick Revision Notes
- Query options: derived methods, JPQL, native SQL, Criteria, Specifications.
- N+1 = 1 query for list + N for children → fix with JOIN FETCH / @EntityGraph / batch.
- Optimistic lock = `@Version` (retry on conflict); pessimistic = lock the row.
- Performance: LAZY + fetch joins, pagination, caching, projections, batching.

## 🙋 FAQs
**Q: Best default locking for web apps?** Optimistic (via `@Version`) — no DB locks, good for low-conflict cases.

## 📎 References
- Vlad Mihalcea's blog (Hibernate performance)
- Hibernate ORM docs

[⬅ Back to Hibernate Index](./README.md)

