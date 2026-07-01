# Backend Projects — Part 2

Tech stack: **Java 17, Spring Boot, Spring Security, JPA, MySQL/PostgreSQL, Redis, Docker**.

---

## 5. 🔗 URL Shortener (like bit.ly)

### Overview
Turn a long URL into a short code and redirect users.

### Entities
```
UrlMapping(id, short_code, long_url, created_at, expiry, click_count)
```

### Key APIs
```
POST /shorten        { "url": "https://very-long-url..." }  → returns short code
GET  /{shortCode}    → 301 redirect to the long URL
GET  /{shortCode}/stats
```

### How the short code is generated
- **Base62 encoding** of an auto-increment ID (`[a-zA-Z0-9]` → 62 chars).
- Or a **hash** (MD5) of the URL, take first 6-8 chars.

```
long URL → save → id=125 → Base62(125) = "cb" → short URL /cb
```

### Architecture
```
Client → LB → App → Redis (cache code→url) → DB
                        │
             redirect (301) using cached mapping
```

### Flow
1. POST long URL → generate unique short code → store mapping.
2. GET /shortCode → look up (Redis first, then DB) → **301 redirect**.
3. Increment click count (async).

### Challenges & Solutions
- **Fast redirects** → cache mappings in Redis (read-heavy).
- **Unique codes** → Base62 of DB id (no collisions).
- **Scale** → cache + read replicas; codes are short and indexed.
- **Analytics** → track clicks asynchronously.

---

## 6. 🏨 Hotel Booking

### Overview
Search hotels, check availability, book rooms, and pay.

### Entities
```
Hotel(id, name, city), Room(id, hotel_id, type, price, count)
Booking(id, user_id, room_id, check_in, check_out, status)
Payment(id, booking_id, amount, status)
```

### Key APIs
```
GET  /hotels?city=&checkIn=&checkOut=
POST /bookings                 # reserve room
POST /payments
DELETE /bookings/{id}          # cancel
```

### Flow (booking)
1. Search available rooms for the date range.
2. Reserve room → check availability in a **transaction** (prevent double-booking).
3. Pay → confirm booking.
4. Send confirmation (async).

### Challenges & Solutions
- **Double booking** → pessimistic lock / transaction on room availability.
- **Date-range availability** → query overlapping bookings.
- **Payment + booking consistency** → hold booking until payment, timeout to release.
- **Concurrency spikes** → queue + optimistic locking.

```
Availability check: no booking overlaps [checkIn, checkOut] for that room
```

---

## 7. 💳 Payment Gateway

### Overview
Process payments securely between customers and merchants.

### Entities
```
Payment(id, order_id, amount, currency, status, method, idempotency_key)
Transaction(id, payment_id, gateway_ref, status)
Refund(id, payment_id, amount, status)
```

### Key APIs
```
POST /payments        { order_id, amount, method, idempotency_key }
GET  /payments/{id}
POST /payments/{id}/refund
POST /webhooks/gateway  # provider notifies payment result
```

### Flow
1. Client requests payment with an **idempotency key**.
2. Gateway calls external provider (Stripe/Razorpay).
3. Provider processes → sends result via **webhook**.
4. Update payment status → notify order service.

### Challenges & Solutions
- **Double charges** → **idempotency keys** (same key = same result).
- **Reliability** → webhooks + retries; store every state change.
- **Security** → PCI compliance, never store raw card data, tokenization.
- **Async result** → status: PENDING → SUCCESS/FAILED via webhook.

---

## 8. 💼 Job Portal (like Naukri/LinkedIn Jobs)

### Overview
Employers post jobs; candidates search and apply.

### Entities
```
User(role: CANDIDATE/EMPLOYER)
Job(id, employer_id, title, description, location, skills, salary)
Application(id, job_id, candidate_id, resume_url, status)
Company(id, name, about)
```

### Key APIs
```
POST /jobs                       # employer posts a job
GET  /jobs?skill=&location=&page= # search + filter + pagination
POST /jobs/{id}/apply            # candidate applies (upload resume)
GET  /applications               # track applications
```

### Architecture
```
Client → LB → App → MySQL (jobs, users)
                   → Elasticsearch (fast job search)
                   → S3 (resumes) + CDN
                   → Redis (cache popular searches)
```

### Flow
1. Employer posts job → indexed for search.
2. Candidate searches (filters: skill, location, salary) → paginated results.
3. Apply → upload resume (S3) → create application.
4. Employer reviews applications → updates status.

### Challenges & Solutions
- **Fast search/filter** → Elasticsearch instead of SQL LIKE.
- **Resume storage** → S3 + signed URLs.
- **Relevance** → rank by skills match.
- **Scale reads** → cache popular searches in Redis.

---

## 🎤 Project Interview Tips
- Always mention **why** you chose each technology.
- Be ready to discuss **data model**, **key API**, **one hard problem** + solution.
- Know how you'd **scale** it (cache, replicas, queues, CDN).

[⬅ Back to Projects Index](./README.md)

