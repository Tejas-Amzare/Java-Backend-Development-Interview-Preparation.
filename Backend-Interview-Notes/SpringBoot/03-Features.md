# 3. Spring Boot Features: Actuator, Caching, Scheduling, Async, File Upload, Email, Swagger

> 🔴 **Level:** Advanced | ⭐ **Interview Frequency:** High

A quick tour of the production features interviewers love to ask about.

---

## 📊 Actuator (monitoring)
Exposes ready-made endpoints to check app **health and metrics**.
```
/actuator/health   → UP/DOWN
/actuator/metrics  → memory, CPU, requests
/actuator/info     → app info
```
```properties
management.endpoints.web.exposure.include=health,info,metrics
```
Use: health checks for Kubernetes/load balancers.

---

## 🛠️ DevTools
Auto-restarts the app when code changes (faster development). Add `spring-boot-devtools`.
Not for production.

---

## 🎁 Lombok
Removes boilerplate (getters/setters/constructors) with annotations.
```java
@Getter @Setter @NoArgsConstructor @AllArgsConstructor @Builder
public class User {
    private Long id;
    private String name;
}
// @Data = @Getter + @Setter + @ToString + @EqualsAndHashCode + @RequiredArgsConstructor
```

---

## ⚡ Caching
Store results in memory to avoid repeated work / DB calls.
```java
@EnableCaching                       // on main class
@Cacheable("users")                  // cache the result
public User getUser(Long id) { ... }
@CacheEvict(value = "users", key = "#id")   // remove from cache on update
public void updateUser(Long id) { ... }
```
Backends: Caffeine, Redis, EhCache. Use: speed up expensive/frequent reads.

---

## ⏰ Scheduling
Run tasks automatically on a schedule.
```java
@EnableScheduling
@Scheduled(cron = "0 0 * * * *")     // every hour
public void cleanup() { ... }
@Scheduled(fixedRate = 5000)         // every 5 seconds
public void poll() { ... }
```
Use: reports, cleanup jobs, sending reminders.

---

## 🔀 Async
Run methods in a separate thread so the caller doesn't wait.
```java
@EnableAsync
@Async
public CompletableFuture<String> sendReport() { ... }
```
Use: sending emails, heavy background work.

---

## 📎 Pagination & Sorting
Return data in pages (not all at once) via Spring Data.
```java
Page<User> users = repo.findAll(PageRequest.of(0, 10, Sort.by("name")));
// GET /users?page=0&size=10&sort=name,asc
```
Use: product listings, search results.

---

## 📤 File Upload
```java
@PostMapping("/upload")
public String upload(@RequestParam("file") MultipartFile file) throws IOException {
    file.transferTo(new File("/uploads/" + file.getOriginalFilename()));
    return "Uploaded";
}
```

---

## 📧 Email Sending
Use `spring-boot-starter-mail` + `JavaMailSender`.
```java
SimpleMailMessage msg = new SimpleMailMessage();
msg.setTo("user@mail.com");
msg.setSubject("Welcome");
msg.setText("Thanks for signing up!");
mailSender.send(msg);
```

---

## 📝 Logging
Uses SLF4J + Logback by default.
```java
private static final Logger log = LoggerFactory.getLogger(MyService.class);
log.info("User {} created", id);
log.error("Failed", ex);
```
Levels: TRACE < DEBUG < INFO < WARN < ERROR.

---

## 📖 OpenAPI / Swagger
Auto-generates interactive API docs. Add `springdoc-openapi-starter-webmvc-ui`.
```
Visit: http://localhost:8080/swagger-ui.html
```
Use: share and test APIs with frontend teams.

---

## ❓ Interview Questions
1. What is Spring Boot Actuator?
2. How does `@Cacheable` work? Difference from `@CacheEvict`?
3. How to schedule a task? Difference between `fixedRate` and `cron`?
4. What does `@Async` do? What's required for it to work? (`@EnableAsync` + separate thread)
5. How to implement pagination in Spring Data JPA?
6. What is Lombok? Name common annotations.
7. How do you document APIs? (Swagger/OpenAPI)
8. Difference between `fixedRate` and `fixedDelay`? (Rate = fixed interval; delay = after previous finishes)

---

## ✅ Best Practices
- Secure Actuator endpoints in production.
- Cache only expensive, frequently-read data; set eviction.
- Keep scheduled/async tasks idempotent and monitored.
- Always paginate large lists.

## ⚠️ Common Mistakes
- Exposing all Actuator endpoints publicly.
- Caching data that changes often (stale results).
- `@Async`/`@Cacheable` on a method called within the **same class** (proxy won't apply).
- Loading all rows instead of paginating.

---

## ⚡ Quick Revision Notes
- Actuator = health/metrics endpoints.
- `@Cacheable` caches; `@CacheEvict` clears.
- `@Scheduled` (cron/fixedRate); `@Async` runs in background.
- Pagination via `PageRequest`; Lombok cuts boilerplate; Swagger documents APIs.

## 🙋 FAQs
**Q: Why doesn't `@Cacheable` work when I call the method from the same class?** Spring uses proxies; self-calls bypass the proxy.

## 📎 References
- Spring Boot docs — Actuator, Caching, Scheduling
- springdoc.org

[⬅ Back to Spring Boot Index](./README.md)

