# 13. Generics

> 🟡 **Level:** Intermediate | ✅ **Interview Frequency:** Medium

---

## 🧠 Concept

**Generics** let you write classes/methods that work with **any type**, while keeping
**type safety** (catching type errors at compile time instead of runtime).

The `<T>` is a **type placeholder**.

---

## 💬 Simple Explanation

A **box** can hold anything. But a **labeled box** ("only books") makes sure you don't
put shoes in it by mistake. Generics are that label for your code.

---

## 🧩 Example

```java
// Without generics - unsafe (needs casting, can crash)
List list = new ArrayList();
list.add("Hello");
String s = (String) list.get(0);   // manual cast

// With generics - safe
List<String> names = new ArrayList<>();
names.add("Hello");
String name = names.get(0);        // no cast, type-checked
```

### Generic Class

```java
class Box<T> {
    private T value;
    public void set(T value) { this.value = value; }
    public T get() { return value; }
}

Box<Integer> intBox = new Box<>();
intBox.set(10);
```

### Generic Method

```java
public <T> void printAll(List<T> items) {
    for (T item : items) System.out.println(item);
}
```

---

## 🔠 Wildcards

| Symbol | Meaning |
|--------|---------|
| `<?>` | Any type (unknown) |
| `<? extends T>` | T or its subclasses (read) |
| `<? super T>` | T or its parents (write) |

```java
void printNumbers(List<? extends Number> list) { ... }  // accepts Integer, Double...
```

**PECS rule:** *Producer Extends, Consumer Super.*

---

## 🌍 Real-World Use Case

Spring's `JpaRepository<User, Long>` uses generics — the same repository code works for
any entity type (`User`, `Order`, `Product`).

---

## ❓ Interview Questions

1. What are generics and why use them?
2. What is type erasure? (Generics info is removed at runtime)
3. What are bounded types? (`<T extends Number>`)
4. Difference between `<?>`, `<? extends T>`, `<? super T>`?
5. Can we use primitives with generics? (**No** — use wrappers like `Integer`)

---

## ✅ Best Practices
- Use generics for reusable, type-safe collections and utilities.
- Follow **PECS** for wildcards.

## ⚠️ Common Mistakes
- Using raw types (`List` instead of `List<String>`).
- Trying to create `new T()` (not allowed due to type erasure).

---

## ⚡ Quick Revision Notes
- Generics = type-safe, reusable code with `<T>`.
- Compile-time checking, no manual casting.
- Type erasure removes generic info at runtime.
- Wildcards: `? extends` (read), `? super` (write) — PECS.

## 🙋 FAQs
**Q: Do generics exist at runtime?** No — erased to `Object` (type erasure).

## 📎 References
- Oracle Docs — Generics

[⬅ Back to Java Index](./README.md)

