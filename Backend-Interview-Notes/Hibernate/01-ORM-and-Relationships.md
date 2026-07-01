# 1. ORM, Entity Lifecycle, Fetch & Cascade, Relationships

> 🟡 **Level:** Intermediate | 🔥 **Interview Frequency:** Very High

---

## 🧠 Concept

**ORM (Object-Relational Mapping)** = mapping Java **objects** to database **tables**, so you
work with objects instead of writing SQL.

```
Java Object  ⇄  ORM (Hibernate)  ⇄  Database Table
  User                                users
```

- **JPA** = the standard (interface). **Hibernate** = the implementation.

```java
@Entity
@Table(name = "users")
public class User {
    @Id @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(nullable = false)
    private String name;
}
```

---

## ♻️ Entity Lifecycle (states)

```
Transient → Persistent → Detached → Removed
```

| State | Meaning |
|-------|---------|
| **Transient** | New object, not linked to DB yet (`new User()`) |
| **Persistent** | Managed by Hibernate, changes auto-saved (`save`/`persist`) |
| **Detached** | Was persistent, but session closed |
| **Removed** | Marked for deletion (`delete`) |

Hibernate's **dirty checking**: if a persistent object changes, Hibernate auto-updates the DB
on commit — no explicit `save()` needed.

---

## 🔗 Relationships (mappings)

| Annotation | Meaning | Example |
|------------|---------|---------|
| `@OneToOne` | 1 ↔ 1 | User ↔ Profile |
| `@OneToMany` | 1 → many | User → Orders |
| `@ManyToOne` | many → 1 | Order → User |
| `@ManyToMany` | many ↔ many | Student ↔ Course |

```java
@Entity
public class User {
    @Id @GeneratedValue private Long id;

    @OneToMany(mappedBy = "user", cascade = CascadeType.ALL)
    private List<Order> orders = new ArrayList<>();
}

@Entity
public class Order {
    @Id @GeneratedValue private Long id;

    @ManyToOne(fetch = FetchType.LAZY)
    @JoinColumn(name = "user_id")
    private User user;
}
```

- `mappedBy` = the **non-owning** side (points to the field on the other side).
- `@JoinColumn` = the foreign key column (owning side).

---

## 🚚 Fetch Types

| Type | Meaning | Default for |
|------|---------|-------------|
| **EAGER** | Load related data **immediately** | `@ManyToOne`, `@OneToOne` |
| **LAZY** | Load related data **only when accessed** | `@OneToMany`, `@ManyToMany` |

> ✅ Prefer **LAZY** to avoid loading huge data you don't need. Fetch what you need with a query.

---

## 🌊 Cascade Types

Cascade means: an operation on the parent also applies to its children.

| Cascade | Effect |
|---------|--------|
| `PERSIST` | Save parent → save children |
| `MERGE` | Update parent → update children |
| `REMOVE` | Delete parent → delete children |
| `ALL` | All of the above |

```java
@OneToMany(cascade = CascadeType.ALL, orphanRemoval = true)
private List<Order> orders;
```
`orphanRemoval = true` → removing a child from the list deletes it from the DB.

---

## 🌍 Real-World Use Case
A `User` has many `Orders`. Saving a user with cascade also saves their orders. Loading orders
lazily avoids pulling thousands of rows when you only need the user's name.

---

## ❓ Interview Questions
1. What is ORM? What problem does it solve?
2. Difference between JPA and Hibernate?
3. Explain entity lifecycle states.
4. Difference between EAGER and LAZY fetching?
5. Explain relationship mappings (`@OneToMany`, etc.).
6. What is `mappedBy`? Owning vs non-owning side?
7. What are cascade types?
8. What is dirty checking?
9. `save()` vs `persist()` vs `merge()`?
10. What is `orphanRemoval`?

---

## ✅ Best Practices
- Use **LAZY** fetching by default; fetch joins when needed.
- Set the owning side correctly with `@JoinColumn`.
- Use DTOs, don't expose entities in APIs.
- Use `cascade` carefully (REMOVE can delete more than expected).

## ⚠️ Common Mistakes
- EAGER everywhere → loads too much data (performance hit).
- `LazyInitializationException` — accessing lazy data after session closed.
- Bidirectional relationships without keeping both sides in sync.

---

## ⚡ Quick Revision Notes
- ORM maps objects ↔ tables; JPA = spec, Hibernate = implementation.
- States: Transient → Persistent → Detached → Removed.
- Fetch: EAGER (now) vs LAZY (on access) — prefer LAZY.
- Relationships: OneToOne/OneToMany/ManyToOne/ManyToMany; `mappedBy` = non-owning side.
- Cascade propagates operations to children; `orphanRemoval` deletes removed children.

## 🙋 FAQs
**Q: Why LazyInitializationException?** You accessed a lazy field after the Hibernate session closed. Fetch it in the query or keep the transaction open.

## 📎 References
- Hibernate ORM docs
- Spring Data JPA reference

[⬅ Back to Hibernate Index](./README.md)

