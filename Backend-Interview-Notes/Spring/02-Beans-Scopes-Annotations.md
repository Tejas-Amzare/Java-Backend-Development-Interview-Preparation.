# 2. Beans, Scopes & Annotations

> 🟡 **Level:** Intermediate | 🔥 **Interview Frequency:** Very High

---

## 🧠 Concept

- A **Bean** is any object that **Spring creates and manages** for you.
- **Scope** decides **how many** instances of a bean exist and how long they live.
- **Annotations** tell Spring which classes to manage and how to wire them.

---

## 🫘 What is a Bean?

```java
@Component                      // Spring now manages this class as a bean
public class EmailService { }
```

You can also define beans manually:
```java
@Configuration
public class AppConfig {
    @Bean
    public EmailService emailService() {
        return new EmailService();   // Spring registers the returned object
    }
}
```

---

## 🏷️ Common Stereotype Annotations

| Annotation | Use on | Meaning |
|------------|--------|---------|
| `@Component` | any class | generic Spring bean |
| `@Service` | service layer | business logic |
| `@Repository` | data layer | DB access (adds exception translation) |
| `@Controller` | web layer | handles web requests |
| `@RestController` | web layer | `@Controller` + `@ResponseBody` (REST APIs) |

> All of `@Service`, `@Repository`, `@Controller` are **specialized `@Component`s**.

---

## 🔌 Wiring Annotations

| Annotation | Meaning |
|------------|---------|
| `@Autowired` | inject a dependency automatically |
| `@Qualifier` | pick a specific bean when many match |
| `@Primary` | default bean when multiple candidates exist |
| `@Value` | inject a value from properties |
| `@Configuration` | class that defines beans |
| `@Bean` | method that produces a bean |

```java
@Service
public class NotificationService {
    private final MessageSender sender;
    public NotificationService(@Qualifier("smsSender") MessageSender sender) {
        this.sender = sender;   // picks the SMS bean specifically
    }
}
```

---

## 📦 Bean Scopes

| Scope | Meaning |
|-------|---------|
| **singleton** (default) | ONE shared instance for the whole app |
| **prototype** | a NEW instance every time it's requested |
| **request** | one per HTTP request (web) |
| **session** | one per HTTP session (web) |
| **application** | one per ServletContext |

```java
@Component
@Scope("prototype")
public class Cart { }   // new cart each time
```

```
singleton:  request1 ─┐
            request2 ─┼──► same Bean instance
            request3 ─┘

prototype:  request1 ──► Bean A
            request2 ──► Bean B (new each time)
```

---

## 🌍 Real-World Use Case
- `UserService` → **singleton** (stateless, shared).
- A shopping `Cart` tied to a user session → **prototype/session** scope.

---

## ❓ Interview Questions
1. What is a Spring bean?
2. Difference between `@Component`, `@Service`, `@Repository`, `@Controller`?
3. What are bean scopes? Default scope? (**singleton**)
4. Difference between singleton and prototype scope?
5. `@Autowired` vs `@Qualifier` vs `@Primary`?
6. Difference between `@Component` and `@Bean`?
7. Are Spring singleton beans thread-safe? (Not automatically — avoid mutable state)
8. What does `@Value` do?

---

## 📋 @Component vs @Bean
| @Component | @Bean |
|------------|-------|
| On a class | On a method |
| Auto-detected by scanning | Manually defined in `@Configuration` |
| Your own classes | Third-party/library classes you can't annotate |

---

## ✅ Best Practices
- Keep singleton beans **stateless**.
- Use `@Qualifier`/`@Primary` to resolve ambiguity.
- Use `@Bean` for classes you can't annotate (third-party).

## ⚠️ Common Mistakes
- Storing mutable state in singleton beans → concurrency bugs.
- Multiple matching beans without `@Qualifier` → `NoUniqueBeanDefinitionException`.
- Forgetting `@Component`/`@Service` → bean not created.

---

## ⚡ Quick Revision Notes
- Bean = object managed by Spring.
- Stereotypes: `@Component`/`@Service`/`@Repository`/`@Controller`.
- Default scope = **singleton**; prototype = new each time.
- `@Autowired` injects; `@Qualifier`/`@Primary` resolve conflicts.
- `@Component` = class-level auto; `@Bean` = method-level manual.

## 🙋 FAQs
**Q: How many instances of a singleton bean exist?** One, shared across the whole application.

## 📎 References
- Spring docs — Beans, Bean Scopes

[⬅ Back to Spring Index](./README.md)

