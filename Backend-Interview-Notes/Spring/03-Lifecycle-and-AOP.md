# 3. Bean Lifecycle & AOP

> 🔴 **Level:** Advanced | ⭐ **Interview Frequency:** High

---

## Part A — Bean Lifecycle

### 🧠 Concept
The **bean lifecycle** is the series of steps Spring follows to **create, use, and destroy** a bean.

### 🗺️ Lifecycle Steps
```
1. Instantiate bean (constructor)
2. Inject dependencies (DI)
3. @PostConstruct  → custom init logic runs
4. Bean is READY and used by the app
5. @PreDestroy     → cleanup before shutdown
6. Bean destroyed
```

```java
@Component
public class CacheService {
    @PostConstruct
    public void init() { System.out.println("Cache warmed up"); }

    @PreDestroy
    public void cleanup() { System.out.println("Cache cleared"); }
}
```

- `@PostConstruct` → runs **after** dependencies are injected (setup).
- `@PreDestroy` → runs **before** the bean is destroyed (cleanup).

---

## Part B — AOP (Aspect-Oriented Programming)

### 🧠 Concept
**AOP** lets you add **common behavior** (logging, security, transactions) to many methods
**without** changing their code. This common behavior is called a **cross-cutting concern**.

### 💬 Simple Explanation
Instead of writing "log start / log end" in **every** method, you write it **once** in an
**aspect**, and Spring applies it automatically. Like a **security guard** checking everyone
entering a building.

### 🔑 AOP Terms
| Term | Meaning |
|------|---------|
| **Aspect** | the reusable extra behavior (e.g., logging) |
| **Advice** | the actual code + when it runs |
| **Join point** | a point where advice can run (a method call) |
| **Pointcut** | expression selecting *which* methods |
| **Weaving** | linking aspects into the target code |

### Advice Types
| Advice | Runs |
|--------|------|
| `@Before` | before the method |
| `@After` | after the method (always) |
| `@AfterReturning` | after success |
| `@AfterThrowing` | after an exception |
| `@Around` | before **and** after (most powerful) |

### 🧩 Example
```java
@Aspect
@Component
public class LoggingAspect {

    @Before("execution(* com.app.service.*.*(..))")   // pointcut
    public void logBefore(JoinPoint jp) {
        System.out.println("Calling: " + jp.getSignature().getName());
    }

    @Around("execution(* com.app.service.*.*(..))")
    public Object measureTime(ProceedingJoinPoint pjp) throws Throwable {
        long start = System.currentTimeMillis();
        Object result = pjp.proceed();                // run the real method
        System.out.println("Took " + (System.currentTimeMillis() - start) + "ms");
        return result;
    }
}
```

---

## 🌍 Real-World Use Case
- `@Transactional` is built on AOP — Spring wraps your method in begin/commit/rollback.
- Centralized **logging**, **security checks**, **performance monitoring**.

---

## ❓ Interview Questions
1. Explain the Spring bean lifecycle.
2. What do `@PostConstruct` and `@PreDestroy` do?
3. What is AOP? Why use it?
4. What is a cross-cutting concern?
5. Explain aspect, advice, pointcut, join point.
6. Difference between `@Before` and `@Around` advice?
7. How does `@Transactional` use AOP?
8. How does Spring AOP work internally? (Proxies — JDK dynamic proxy / CGLIB)

---

## ✅ Best Practices
- Use AOP for genuinely cross-cutting concerns only (logging, security, tx).
- Keep aspects simple and fast (they run on every matched call).
- Use `@PostConstruct` for initialization that needs injected dependencies.

## ⚠️ Common Mistakes
- Putting business logic in aspects.
- Broad pointcuts that accidentally match too many methods.
- Expecting AOP to work on `private`/self-invoked methods (proxy limitation).

---

## ⚡ Quick Revision Notes
- Lifecycle: construct → inject → `@PostConstruct` → use → `@PreDestroy` → destroy.
- AOP = add cross-cutting behavior without touching code.
- Terms: aspect, advice, pointcut, join point, weaving.
- `@Around` = most powerful advice; Spring AOP uses proxies.
- `@Transactional` is powered by AOP.

## 🙋 FAQs
**Q: Why doesn't AOP work on private methods?** Spring uses proxies; only public, externally-called methods are intercepted.

## 📎 References
- Spring docs — Aspect Oriented Programming

[⬅ Back to Spring Index](./README.md)

