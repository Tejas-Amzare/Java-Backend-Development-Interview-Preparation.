# 12. Stream API, Lambda & Optional

> 🟡 **Level:** Intermediate | 🔥 **Interview Frequency:** Very High

---

## 🧠 Concept

- **Lambda** = a short way to write a function (no name, just logic).
- **Stream API** = process collections in a clean, readable, "pipeline" style (filter, map, collect).
- **Optional** = a box that may or may not hold a value — helps avoid `NullPointerException`.

All introduced in **Java 8**.

---

## 💬 Simple Explanation

Old way = write a long loop.
Stream way = tell Java **what** you want, not **how** to loop.

Think of a **factory conveyor belt** 🏭: data flows → filter → transform → collect.

---

## 🧩 Lambda Expression

```java
// Old way
Runnable r = new Runnable() {
    public void run() { System.out.println("Hi"); }
};

// Lambda way
Runnable r2 = () -> System.out.println("Hi");

// With params
Comparator<Integer> c = (a, b) -> a - b;
```

Syntax: `(parameters) -> { body }`

---

## 🧩 Stream API

```java
List<Integer> nums = List.of(1, 2, 3, 4, 5, 6);

int sum = nums.stream()
              .filter(n -> n % 2 == 0)   // keep even: 2,4,6
              .map(n -> n * n)           // square: 4,16,36
              .reduce(0, Integer::sum);  // add: 56
```

### Common Stream Operations

| Operation | Use | Type |
|-----------|-----|------|
| `filter()` | keep matching items | intermediate |
| `map()` | transform each item | intermediate |
| `sorted()` | sort | intermediate |
| `distinct()` | remove duplicates | intermediate |
| `limit(n)` | first n items | intermediate |
| `collect()` | gather to list/set/map | terminal |
| `forEach()` | do something with each | terminal |
| `count()` | how many | terminal |
| `reduce()` | combine into one value | terminal |
| `anyMatch()` | true if any matches | terminal |

> **Intermediate** operations are lazy (build the pipeline). **Terminal** operations trigger execution.

```java
// Collect to a list
List<String> upper = names.stream()
                          .map(String::toUpperCase)
                          .collect(Collectors.toList());

// Group by
Map<Integer, List<String>> byLen =
    names.stream().collect(Collectors.groupingBy(String::length));
```

---

## 🧩 Optional

```java
Optional<String> name = Optional.ofNullable(getName());

name.ifPresent(n -> System.out.println(n));      // run only if present
String result = name.orElse("Default");          // fallback value
String value  = name.orElseThrow();              // throw if empty
```

---

## 🌍 Real-World Use Case

- Filter active users from a list, get their emails, and collect into a list — **1 stream line**.
- Return `Optional<User>` from a repository so callers safely handle "not found".

---

## ❓ Interview Questions

1. What is a lambda expression?
2. What is a functional interface? (Exactly one abstract method — `@FunctionalInterface`)
3. Difference between `map()` and `filter()`?
4. Intermediate vs terminal operations?
5. What is `Optional` and why use it?
6. Difference between `Collection` and `Stream`? (Stream doesn't store data; single-use)
7. What are method references? (`String::toUpperCase`)
8. Difference between `findFirst()` and `findAny()`?
9. What does `reduce()` do?
10. Is a stream reusable? (**No** — once consumed, it's closed)

---

## ✅ Best Practices
- Use streams for **readability**, not for everything (simple loops can be clearer).
- Return `Optional` instead of `null` from methods.
- Prefer method references (`Class::method`) when cleaner.

## ⚠️ Common Mistakes
- Reusing a stream after a terminal operation → `IllegalStateException`.
- Calling `optional.get()` without checking `isPresent()`.
- Side effects inside `map()` (should be pure transformations).

---

## ⚡ Quick Revision Notes
- Lambda = anonymous function: `(x) -> x*2`.
- Stream pipeline = source → intermediate ops → terminal op.
- Intermediate = lazy (`filter`, `map`); terminal = triggers (`collect`, `forEach`).
- Optional avoids null; use `orElse`, `ifPresent`, `orElseThrow`.
- Streams are single-use.

## 📋 Common Functional Interfaces

| Interface | Method | Meaning |
|-----------|--------|---------|
| `Function<T,R>` | `apply` | T → R |
| `Predicate<T>` | `test` | T → boolean |
| `Consumer<T>` | `accept` | T → void |
| `Supplier<T>` | `get` | () → T |

## 🙋 FAQs
**Q: Are streams faster than loops?** Not always — they're about readability; parallel streams can help for big data.

## 📎 References
- Oracle Docs — Stream, Lambda Expressions

[⬅ Back to Java Index](./README.md)

