# 🎤 Detailed Spoken Answers — Spring, Spring Boot & Hibernate

> Model answers to **speak out loud**. Formula: `Definition → Example → Why it matters.`

---

## 1. What is Dependency Injection and IoC? 🔥

> "Inversion of Control, or IoC, means that instead of my code creating its own objects with
> `new`, the **Spring container creates and manages them** for me — the control is inverted from
> my code to the framework.
>
> **Dependency Injection** is how IoC is achieved — Spring **injects** the objects a class needs,
> rather than the class building them itself. For example, instead of my `OrderService` doing
> `new PaymentService()`, Spring passes a `PaymentService` into its constructor.
>
> The big benefit is **loose coupling** — my classes don't depend on concrete implementations, so
> they're easy to test with mocks and easy to change. I prefer **constructor injection** with
> final fields because it makes dependencies clear and the object immutable."

---

## 2. Difference between @Component, @Service, @Repository, @Controller? 🔥

> "All four tell Spring to **create and manage that class as a bean** — and technically,
> `@Service`, `@Repository`, and `@Controller` are all **specializations of `@Component`**. The
> difference is about **intent and layer**.
>
> I use **`@Component`** for a general-purpose bean. **`@Service`** marks the **business logic**
> layer. **`@Repository`** marks the **data access** layer, and it adds a bonus — it translates
> database exceptions into Spring's cleaner `DataAccessException`. **`@Controller`** marks the
> **web layer** that handles requests, and **`@RestController`** is `@Controller` plus
> `@ResponseBody` for building REST APIs that return JSON.
>
> So functionally similar, but using the right one makes the code's **purpose clear** and enables
> layer-specific features."

---

## 3. What is the default bean scope? Explain singleton vs prototype 🔥

> "The **default scope in Spring is singleton**, which means the container creates **one shared
> instance** of that bean for the whole application, and everyone gets the same one.
>
> **Prototype** scope creates a **new instance every time** the bean is requested.
>
> There are also web scopes — **request** creates one bean per HTTP request, and **session** one
> per user session.
>
> One important point: because singleton beans are shared, I keep them **stateless** — I don't
> store per-user mutable data in them, otherwise I'd get concurrency bugs. Something like a
> shopping cart tied to a user is better as a prototype or session-scoped bean."

---

## 4. What is @SpringBootApplication and auto-configuration? 🔥

> "`@SpringBootApplication` is a convenience annotation that combines **three** annotations:
> `@Configuration`, which lets the class define beans; `@ComponentScan`, which scans the package
> for components; and `@EnableAutoConfiguration`, which turns on Spring Boot's auto-configuration.
>
> **Auto-configuration** means Spring Boot looks at the libraries on my **classpath** and
> automatically sets up sensible default beans. For example, if it sees JPA and a database driver,
> it auto-creates a DataSource and an EntityManager, so I don't wire all that by hand.
>
> It works using conditional annotations like `@ConditionalOnClass`, and I can always **override**
> any default by defining my own bean. That's the magic that makes Spring Boot so fast to start
> with."

---

## 5. Explain the layered architecture of a Spring Boot REST API 🔥

> "I structure a Spring Boot app in clear layers so each has one responsibility.
>
> The **Controller** layer receives HTTP requests and returns responses — it's thin. It calls
> the **Service** layer, which holds the **business logic**. The Service calls the **Repository**
> layer, which talks to the **database** using Spring Data JPA. My database tables are mapped by
> **Entity** classes, but I never expose entities directly — I convert them to **DTOs** for the
> API, so I control exactly what data goes in and out.
>
> On top of that, I add **validation** with `@Valid`, and a **global exception handler** with
> `@RestControllerAdvice` so all errors return a consistent JSON response with the right status
> code. This separation keeps the code clean, testable, and easy to maintain."

---

## 6. Why use DTOs instead of exposing entities? ⭐

> "A DTO — Data Transfer Object — is a simple object I use to send and receive data in the API,
> separate from my database entity.
>
> I use DTOs for a few reasons. First, **security** — I can hide internal fields like passwords
> or audit columns. Second, **decoupling** — my API doesn't break every time the database schema
> changes. Third, it **avoids lazy-loading problems** with Hibernate, because I'm not serializing
> a live entity with proxies. And fourth, I control **exactly** the shape of the request and
> response.
>
> To convert between entity and DTO, I use a mapper — either manually or with a library like
> MapStruct."

---

## 7. How do you handle exceptions globally in Spring Boot? 🔥

> "I use a class annotated with **`@RestControllerAdvice`**, which lets me handle exceptions for
> **all controllers in one place**, instead of repeating try-catch everywhere.
>
> Inside it, I write methods annotated with **`@ExceptionHandler`** for specific exceptions —
> for example, one for a `ResourceNotFoundException` that returns a **404**, and one for
> validation errors that returns a **400**. Each method returns a clean, consistent JSON error
> body using `ResponseEntity`, with a proper HTTP status code.
>
> This keeps my controllers focused on the happy path and centralizes all error handling, which
> is much easier to maintain."

---

## 8. What is @Transactional and how does it work? 🔥

> "`@Transactional` wraps a method in a **database transaction** — if the method finishes
> successfully, Spring **commits**; if it throws a runtime exception, Spring **rolls back** all
> the changes automatically.
>
> I usually put it on the **service layer**, because that's where a business operation like
> 'place an order' spans multiple database writes that must succeed or fail together.
>
> Under the hood, it works through **Spring AOP proxies** — Spring wraps my bean in a proxy that
> starts and ends the transaction around my method. One thing to remember: because it's
> proxy-based, it doesn't apply to **private methods** or **self-invoked** calls within the same
> class."

---

## 9. What is the N+1 problem in Hibernate and how do you fix it? 🔥 (senior favorite)

> "The N+1 problem is a common performance issue. Say I load a list of 10 users, and each user
> has orders that are fetched **lazily**. Hibernate runs **1 query** to get the users, and then
> **one extra query per user** to fetch their orders — so 1 plus N queries, 11 in total instead
> of 1 or 2. With large data, that's a huge number of database round trips.
>
> I fix it a few ways. The most common is a **JOIN FETCH** in JPQL, which loads users and their
> orders in a **single query**. I can also use an **`@EntityGraph`** to specify what to fetch
> eagerly for that query, or enable **batch fetching** so Hibernate loads related data in groups.
>
> The key is to detect it early — I watch the SQL logs — and fetch related data deliberately
> instead of letting lazy loading fire many small queries."

---

## 10. Difference between EAGER and LAZY fetching? ⭐

> "This controls **when** Hibernate loads related data.
>
> **EAGER** loads the related data **immediately**, along with the parent entity. **LAZY** loads
> it **only when I actually access it**.
>
> By default, `@ManyToOne` and `@OneToOne` are EAGER, while `@OneToMany` and `@ManyToMany` are
> LAZY. In practice, I **prefer LAZY** almost everywhere, because EAGER can pull in huge amounts
> of data I don't need and cause performance problems. Then, when I *do* need the related data, I
> fetch it explicitly with a join fetch. The one gotcha with LAZY is the
> `LazyInitializationException`, which happens if I access lazy data after the Hibernate session
> is closed — so I make sure to fetch it within the transaction."

---

## 11. What is the difference between JPA, Hibernate, and Spring Data JPA? ⭐

> "These three work together but are different things.
>
> **JPA** is just a **specification** — a set of interfaces and rules for object-relational
> mapping. It doesn't do anything by itself.
>
> **Hibernate** is the most popular **implementation** of that specification — it's the actual
> engine that maps objects to tables and generates SQL.
>
> **Spring Data JPA** is a **layer on top** that removes boilerplate. Instead of writing repository
> code, I just declare an interface extending `JpaRepository`, and Spring generates the
> implementation and even builds queries from method names like `findByEmail`.
>
> So: JPA is the standard, Hibernate implements it, and Spring Data JPA makes it effortless to
> use."

---

## 12. What are the different bean lifecycle callbacks? ⭐

> "When Spring manages a bean, it goes through a lifecycle: it **instantiates** the bean, then
> **injects its dependencies**, then runs any **initialization** logic, the bean is **used**, and
> finally it's **destroyed** on shutdown.
>
> I can hook into two key points. **`@PostConstruct`** runs **after** dependencies are injected —
> I use it for setup like initializing a cache or opening a connection. **`@PreDestroy`** runs
> **before** the bean is destroyed — I use it for cleanup like closing resources.
>
> This gives me a clean place to put initialization and teardown code without cluttering the
> constructor."

---

## 🗣️ Speaking Tips for Spring/Hibernate Rounds
- Tie answers to **real project structure** (Controller → Service → Repository).
- When explaining an annotation, say **what it does + where you put it + why**.
- For Hibernate, always mention **performance awareness** (LAZY, N+1) — it signals experience.
- If asked "how does it work internally", mention **proxies/AOP** for Spring features.

[⬅ Back to Questions Index](./README.md) · [Full Spring/Boot/Hibernate Q Bank](./03-Spring-Boot-Hibernate.md)

