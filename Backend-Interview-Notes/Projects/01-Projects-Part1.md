# Backend Projects — Part 1

Tech stack (all projects): **Java 17, Spring Boot, Spring Security, Spring Data JPA,
MySQL/PostgreSQL, Redis, Docker**.

---

## 1. 🔐 Authentication System

### Overview
User registration, login, and secure access using **JWT**.

### Entities
```
User(id, username, email, password_hash, role, enabled, created_at)
Role(id, name)            // USER, ADMIN
RefreshToken(id, token, user_id, expiry)
```

### Key APIs
| Method | Endpoint | Purpose |
|--------|----------|---------|
| POST | /auth/register | Create account |
| POST | /auth/login | Get JWT + refresh token |
| POST | /auth/refresh | New access token |
| POST | /auth/logout | Invalidate token |
| GET | /users/me | Current user profile |

### Architecture
```
Client → Controller → Security Filter (JWT) → Service → Repository → DB
                          │
                   validates token, sets SecurityContext
```

### Flow
1. Register → password hashed with **BCrypt** → saved.
2. Login → verify → return **JWT (access)** + **refresh token**.
3. Each request → `JwtFilter` validates token → allows/denies.
4. Access token expires → use refresh token to get a new one.

### Challenges & Solutions
- **Token expiry** → short-lived access + refresh tokens.
- **Password security** → BCrypt hashing + salting.
- **Role-based access** → `@PreAuthorize("hasRole('ADMIN')")`.

---

## 2. 🛒 E-Commerce Backend

### Overview
Products, cart, orders, payments — like a mini Amazon.

### Entities
```
User, Product(id, name, price, stock, category)
Cart(id, user_id), CartItem(id, cart_id, product_id, qty)
Order(id, user_id, total, status), OrderItem(...)
Payment(id, order_id, status, method)
```

### Key APIs
```
GET  /products?page=&size=&category=      # list + pagination + filter
POST /cart/items                          # add to cart
POST /orders                              # place order
GET  /orders/{id}                         # track order
POST /payments                            # pay
```

### Architecture
```
Client → API Gateway → [Product, Cart, Order, Payment services]
                              │
                    MySQL + Redis (cache products)
                    Message Queue → email/invoice
```

### Flow (place order)
1. Add products to cart.
2. Checkout → create Order → reduce stock (transaction).
3. Process Payment → on success mark Order PAID.
4. Publish event → send confirmation email (async).

### Challenges & Solutions
- **Stock race conditions** → DB transactions + optimistic locking (`@Version`).
- **Slow product reads** → Redis cache.
- **Order + payment consistency** → transactional + Saga (if microservices).

---

## 3. 🏦 Banking Backend

### Overview
Accounts, deposits, withdrawals, and secure money transfers.

### Entities
```
Account(id, user_id, account_no, balance, type)
Transaction(id, from_acc, to_acc, amount, type, status, timestamp)
```

### Key APIs
```
POST /accounts                      # open account
POST /accounts/{id}/deposit
POST /accounts/{id}/withdraw
POST /transfers                     # A → B
GET  /accounts/{id}/transactions    # statement
```

### Flow (transfer)
1. Validate both accounts + sufficient balance.
2. In **one transaction**: debit sender, credit receiver.
3. If any step fails → **rollback** (no money lost).
4. Record transaction + audit log (trigger/event).

### Challenges & Solutions
- **Atomicity** → ACID transactions (all-or-nothing).
- **Concurrency** → pessimistic/optimistic locking on balance.
- **Security & audit** → strict auth, immutable transaction log.
- **Idempotency** → prevent double transfers with request IDs.

```
Transfer = BEGIN → debit A → credit B → COMMIT (or ROLLBACK)
```

---

## 4. 📱 Social Media Backend

### Overview
Users, posts, likes, comments, follow, and a news feed.

### Entities
```
User, Post(id, user_id, content, created_at)
Follow(follower_id, following_id)
Like(user_id, post_id), Comment(id, post_id, user_id, text)
```

### Key APIs
```
POST /posts
POST /posts/{id}/like
POST /users/{id}/follow
GET  /feed?page=&size=              # posts from people you follow
```

### Architecture
```
Client → LB → App servers (stateless)
                 │
          MySQL (data) + Redis (feed cache, counters)
          CDN (images/videos)
          Message Queue (notifications)
```

### Feed Generation
- **Pull model** → build feed when user opens app (good for most).
- **Push (fan-out)** → precompute feed on new post (good for read-heavy).

### Challenges & Solutions
- **Feed at scale** → cache feeds in Redis, pagination.
- **Media storage** → S3 + CDN.
- **High read load** → read replicas + caching.
- **Notifications** → async via message queue.

---

## 🎤 Common Project Interview Questions
1. Walk me through your project's architecture.
2. How did you handle authentication/security?
3. How did you ensure data consistency (e.g., orders, transfers)?
4. How would you scale this to 1M users?
5. What was the hardest bug/challenge and how did you solve it?
6. Which design patterns did you use?
7. How did you test it?

[⬅ Back to Projects Index](./README.md)

