# 1. Spring Boot Architecture, Auto-Config, Starters, Properties & Profiles

> 🟡 **Level:** Intermediate | 🔥 **Interview Frequency:** Very High

---

## 🧠 Concept

**Spring Boot** = Spring + auto-configuration + embedded server + starters.
It removes boilerplate so you can build production apps quickly.

---

## 🗺️ Architecture (layers)

```
   Client (browser / mobile / Postman)
              │  HTTP
   ┌──────────▼───────────┐
   │   Controller layer   │  ← handles requests (REST endpoints)
   ├──────────────────────┤
   │   Service layer      │  ← business logic
   ├──────────────────────┤
   │   Repository layer   │  ← database access (JPA)
   ├──────────────────────┤
   │   Database           │
   └──────────────────────┘
```

The **entry point**:
```java
@SpringBootApplication      // = @Configuration + @EnableAutoConfiguration + @ComponentScan
public class App {
    public static void main(String[] args) {
        SpringApplication.run(App.class, args);
    }
}
```

---

## ⚙️ Auto-Configuration

Spring Boot **automatically configures** beans based on the libraries on your classpath.
Add the JPA + H2 dependencies → Boot auto-creates a DataSource, EntityManager, etc.

- Driven by `@EnableAutoConfiguration`.
- Uses **conditional** beans (`@ConditionalOnClass`, `@ConditionalOnMissingBean`).
- You can override any default by defining your own bean.

---

## 📦 Starter Dependencies

A **starter** is a bundle of dependencies for a feature. One line pulls everything needed.

| Starter | Gives you |
|---------|-----------|
| `spring-boot-starter-web` | REST APIs + embedded Tomcat |
| `spring-boot-starter-data-jpa` | JPA + Hibernate |
| `spring-boot-starter-security` | Security |
| `spring-boot-starter-test` | JUnit, Mockito |
| `spring-boot-starter-validation` | Bean validation |

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

---

## 📝 Configuration: properties vs yml

Spring Boot reads config from `application.properties` **or** `application.yml`.

```properties
# application.properties
server.port=8081
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
spring.jpa.hibernate.ddl-auto=update
```

```yaml
# application.yml (same thing, nicer for nesting)
server:
  port: 8081
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/mydb
  jpa:
    hibernate:
      ddl-auto: update
```

Read a value in code:
```java
@Value("${server.port}")
private int port;
```

---

## 🌗 Profiles (dev / test / prod)

Profiles let you keep **different settings per environment**.

```
application.properties          ← common
application-dev.properties      ← development DB
application-prod.properties     ← production DB
```

Activate a profile:
```properties
spring.profiles.active=dev
```
```java
@Profile("dev")
@Bean
public DataSource devDataSource() { ... }   // only loads in dev
```

---

## 🌍 Real-World Use Case
Use `dev` profile with an H2 in-memory database locally, and `prod` profile with a real MySQL/
Postgres in production — same code, different config.

---

## ❓ Interview Questions
1. What is Spring Boot? How is it different from Spring?
2. What does `@SpringBootApplication` do? (Combines 3 annotations)
3. What is auto-configuration and how does it work?
4. What are starter dependencies?
5. Difference between `application.properties` and `application.yml`?
6. What are Spring profiles? How to activate them?
7. How does the embedded server work? Can you change it? (Yes — Jetty/Undertow)
8. How to change the default port?
9. How to disable a specific auto-configuration? (`exclude` in `@SpringBootApplication`)

---

## ✅ Best Practices
- Use **profiles** for environment-specific config.
- Never hardcode secrets — use env variables / secret managers.
- Keep `application.yml` clean and organized.

## ⚠️ Common Mistakes
- Committing production passwords in properties files.
- Using `ddl-auto=update` in production (risky schema changes).
- Forgetting to activate the right profile.

---

## ⚡ Quick Revision Notes
- Spring Boot = Spring + auto-config + starters + embedded server.
- `@SpringBootApplication` = `@Configuration` + `@EnableAutoConfiguration` + `@ComponentScan`.
- Starters bundle dependencies; auto-config sets sensible defaults.
- Profiles = per-environment config (dev/test/prod).

## 🙋 FAQs
**Q: Spring vs Spring Boot?** Spring is the framework; Spring Boot removes boilerplate config and adds an embedded server.

## 📎 References
- Spring Boot Reference Documentation

[⬅ Back to Spring Boot Index](./README.md)

