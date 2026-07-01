# 1. Spring Core: IoC & Dependency Injection

> 🟡 **Level:** Intermediate | 🔥 **Interview Frequency:** Very High

---

## 🧠 Concept

- **Spring Framework** = a toolkit to build Java apps. Its core job is to **create and manage
  your objects** for you.
- **IoC (Inversion of Control)** = you don't create objects with `new`; **Spring creates them**.
  Control is "inverted" from you → to Spring.
- **DI (Dependency Injection)** = Spring **gives** an object the other objects it needs.

---

## 💬 Simple Explanation

Normally **you** cook your own food (create objects with `new`).
With Spring, it's like a **restaurant** — you just ask, and the kitchen (IoC container)
prepares and **serves** everything you need (DI).

---

## 🧩 Without vs With DI

```java
// ❌ Without DI - tightly coupled (you create the dependency)
class OrderService {
    private PaymentService payment = new PaymentService();  // hard-coded
}

// ✅ With DI - loosely coupled (Spring injects it)
@Service
class OrderService {
    private final PaymentService payment;
    public OrderService(PaymentService payment) {   // Spring passes it in
        this.payment = payment;
    }
}
```

Now you can easily swap `PaymentService` for a mock in tests → **testable & flexible**.

---

## 🗺️ The IoC Container

```
        ┌──────── IoC Container (ApplicationContext) ────────┐
        │  reads config/annotations                          │
        │  creates beans → injects dependencies → manages    │
        │  their whole lifecycle                             │
        └────────────────────────────────────────────────────┘
             │            │             │
          UserService  OrderService  PaymentService  (beans)
```

- **BeanFactory** = basic container (lazy).
- **ApplicationContext** = full-featured container (most used).

---

## 💉 Types of Dependency Injection

| Type | How | Recommended? |
|------|-----|--------------|
| **Constructor injection** | via constructor | ✅ Best (immutable, testable) |
| **Setter injection** | via setter method | OK for optional deps |
| **Field injection** | `@Autowired` on field | ❌ Avoid (hard to test) |

```java
// Constructor injection (preferred)
@Service
public class UserService {
    private final UserRepository repo;
    public UserService(UserRepository repo) { this.repo = repo; }
}
```

---

## 🌍 Real-World Use Case
Every Spring Boot app uses DI: Controllers get Services injected, Services get Repositories
injected — all wired automatically by Spring.

---

## ❓ Interview Questions
1. What is IoC? What is DI? Difference?
2. Types of dependency injection? Which is best and why?
3. Difference between BeanFactory and ApplicationContext?
4. Why is field injection discouraged?
5. What problem does DI solve? (Tight coupling)
6. What is loose coupling?

---

## ✅ Best Practices
- Prefer **constructor injection** with `final` fields.
- Program to interfaces, not concrete classes.
- Keep beans stateless when possible.

## ⚠️ Common Mistakes
- Using field injection (`@Autowired` on fields) — hard to test.
- Creating objects manually with `new` instead of letting Spring inject.
- Circular dependencies between beans.

---

## ⚡ Quick Revision Notes
- IoC = Spring controls object creation (not you).
- DI = Spring injects dependencies into your beans.
- Prefer constructor injection (immutable + testable).
- ApplicationContext = the main IoC container.

## 🙋 FAQs
**Q: IoC vs DI?** IoC is the concept (Spring is in control); DI is *how* IoC is achieved (injecting dependencies).

## 📎 References
- Spring Framework docs — Core Technologies

[⬅ Back to Spring Index](./README.md)

