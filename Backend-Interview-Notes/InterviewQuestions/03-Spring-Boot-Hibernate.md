# 03 — Spring, Spring Boot & Hibernate Interview Questions (110+)

---

## 🌱 Spring Core (1–30)

1. **What is the Spring Framework?** A Java framework for building loosely-coupled, testable apps.
2. **What is IoC?** Inversion of Control — Spring creates and manages objects.
3. **What is Dependency Injection?** Spring injects an object's dependencies for it.
4. **IoC vs DI?** IoC is the concept; DI is how it's achieved.
5. **Types of DI?** Constructor, setter, field.
6. **Which DI is best?** Constructor injection (immutable, testable).
7. **Why avoid field injection?** Hard to test, hides dependencies.
8. **What is the IoC container?** ApplicationContext — creates/manages beans.
9. **BeanFactory vs ApplicationContext?** Basic lazy container vs full-featured.
10. **What is a bean?** An object managed by Spring.
11. **How to define a bean?** `@Component`/`@Bean` or XML.
12. **What is `@Component`?** Marks a class as a Spring-managed bean.
13. **@Component vs @Bean?** Class-level auto vs method-level manual.
14. **@Service, @Repository, @Controller?** Specialized components for layers.
15. **What does @Repository add?** Exception translation for data access.
16. **What is @Autowired?** Injects a matching bean automatically.
17. **What is @Qualifier?** Picks a specific bean when several match.
18. **What is @Primary?** Marks a default bean among candidates.
19. **What is @Value?** Injects values from properties.
20. **What are bean scopes?** singleton, prototype, request, session, application.
21. **Default bean scope?** Singleton.
22. **Singleton vs prototype?** One shared instance vs new each time.
23. **Are singleton beans thread-safe?** Not automatically — avoid mutable state.
24. **What is the bean lifecycle?** Instantiate → inject → @PostConstruct → use → @PreDestroy → destroy.
25. **What does @PostConstruct do?** Runs init logic after DI.
26. **What is AOP?** Adds cross-cutting concerns without changing code.
27. **What is a cross-cutting concern?** Logging, security, transactions.
28. **AOP terms?** Aspect, advice, pointcut, join point, weaving.
29. **Advice types?** Before, After, AfterReturning, AfterThrowing, Around.
30. **How does Spring AOP work?** Via proxies (JDK dynamic / CGLIB).

---

## 🚀 Spring Boot (31–70)

31. **What is Spring Boot?** Spring + auto-config + starters + embedded server.
32. **Spring vs Spring Boot?** Boot removes boilerplate and adds an embedded server.
33. **What does @SpringBootApplication do?** Combines @Configuration + @EnableAutoConfiguration + @ComponentScan.
34. **What is auto-configuration?** Auto-sets beans based on classpath.
35. **How to disable an auto-config?** `exclude` in @SpringBootApplication / @EnableAutoConfiguration.
36. **What are starter dependencies?** Bundles of dependencies for a feature.
37. **Name common starters?** web, data-jpa, security, test, validation.
38. **What is the embedded server?** Tomcat by default (Jetty/Undertow optional).
39. **properties vs yml?** Same config, YAML is nicer for nesting.
40. **How to read a property?** `@Value("${key}")` or `@ConfigurationProperties`.
41. **What are profiles?** Environment-specific config (dev/test/prod).
42. **How to activate a profile?** `spring.profiles.active=dev`.
43. **What is @RestController?** @Controller + @ResponseBody.
44. **@Controller vs @RestController?** View-returning vs JSON-returning.
45. **@RequestMapping vs @GetMapping?** Generic vs GET-specific shortcut.
46. **@PathVariable vs @RequestParam?** URL path segment vs query parameter.
47. **@RequestBody?** Maps JSON body to a Java object.
48. **What is a DTO?** Data Transfer Object — decouples API from entities.
49. **Why use DTOs?** Hide internal fields, control API shape.
50. **What is ResponseEntity?** Controls status code, headers, body.
51. **How to validate input?** `@Valid` + annotations (@NotNull, @Email...).
52. **How to handle exceptions globally?** @RestControllerAdvice + @ExceptionHandler.
53. **Common status codes?** 200, 201, 204, 400, 401, 403, 404, 500.
54. **PUT vs PATCH?** Full update vs partial update.
55. **What is Actuator?** Health/metrics/monitoring endpoints.
56. **What is DevTools?** Auto-restart on code changes (dev only).
57. **What is Lombok?** Reduces boilerplate (getters/setters/etc.).
58. **@Data in Lombok?** Getters+setters+toString+equals+RequiredArgsConstructor.
59. **How to enable caching?** @EnableCaching + @Cacheable.
60. **@Cacheable vs @CacheEvict?** Store result vs clear cache.
61. **How to schedule tasks?** @EnableScheduling + @Scheduled.
62. **fixedRate vs fixedDelay?** Fixed interval vs after previous finishes.
63. **What is @Async?** Runs a method in a background thread.
64. **How to paginate?** `PageRequest.of(page, size, sort)`.
65. **How to upload files?** `MultipartFile` parameter.
66. **How to send email?** JavaMailSender + starter-mail.
67. **What is logging default?** SLF4J + Logback.
68. **What is Swagger/OpenAPI?** Auto-generated interactive API docs.
69. **How to change the port?** `server.port=8081`.
70. **Why doesn't @Cacheable work on self-call?** Proxy is bypassed for internal calls.

---

## 🐘 Hibernate / JPA (71–110)

71. **What is ORM?** Mapping Java objects to database tables.
72. **JPA vs Hibernate?** JPA is the spec; Hibernate is an implementation.
73. **What is Spring Data JPA?** A layer that auto-generates repositories.
74. **What is @Entity?** Marks a class as a DB table mapping.
75. **What is @Id?** Marks the primary key field.
76. **What is @GeneratedValue?** Auto-generates the PK.
77. **What is JpaRepository?** Interface with ready CRUD methods.
78. **Entity lifecycle states?** Transient, Persistent, Detached, Removed.
79. **What is dirty checking?** Auto-updating changed persistent entities on commit.
80. **save() vs persist()?** save returns id (Hibernate) vs persist returns void (JPA).
81. **get() vs load()?** Eager/null vs lazy proxy.
82. **Fetch types?** EAGER (immediate) vs LAZY (on access).
83. **Default fetch for @OneToMany?** LAZY.
84. **Default fetch for @ManyToOne?** EAGER.
85. **What is LazyInitializationException?** Accessing lazy data after session closed.
86. **Relationship annotations?** @OneToOne, @OneToMany, @ManyToOne, @ManyToMany.
87. **What is mappedBy?** Marks the non-owning side of a relationship.
88. **What is @JoinColumn?** Defines the foreign key column (owning side).
89. **What are cascade types?** PERSIST, MERGE, REMOVE, ALL, etc.
90. **What is orphanRemoval?** Deletes children removed from the collection.
91. **What is JPQL?** Object-oriented query language (uses entity names).
92. **JPQL vs native query?** Portable object query vs raw SQL.
93. **What is Criteria API?** Programmatic, type-safe query building.
94. **What are Specifications?** Reusable, combinable query conditions.
95. **What is the N+1 problem?** 1 query for list + N for children (slow).
96. **How to fix N+1?** JOIN FETCH, @EntityGraph, batch fetching.
97. **What is @Query?** Custom JPQL/native query on a repository method.
98. **What are derived query methods?** Method names Spring turns into queries.
99. **First-level cache?** Session-scoped, on by default.
100. **Second-level cache?** Across sessions (EhCache, etc.), optional.
101. **What is @Transactional?** Wraps a method in a DB transaction.
102. **Where does @Transactional go?** Usually the service layer.
103. **What is optimistic locking?** `@Version` field, retry on conflict.
104. **What is pessimistic locking?** Locks the row until done.
105. **What is a projection?** Selecting only needed columns/DTO.
106. **What is @Modifying?** Marks an update/delete @Query.
107. **What is flush?** Sync persistence context to DB.
108. **What is a detached entity?** Was persistent, now outside the session.
109. **How to improve Hibernate performance?** LAZY + fetch joins, pagination, caching, batching.
110. **What is @Embeddable / @Embedded?** Reuse a value object inside an entity.

[⬅ Back to Questions Index](./README.md)

