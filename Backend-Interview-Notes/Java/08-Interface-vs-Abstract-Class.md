# 8. Interface vs Abstract Class

> 🟡 **Level:** Intermediate | 🔥 **Interview Frequency:** Very High

---

## 🧠 Concept

Both are used for **abstraction**, but they serve different purposes.

- **Abstract class** → a partially built class. Use when classes share **common code**.
- **Interface** → a pure contract (list of methods). Use to define **capabilities/behaviors**.

---

## 💬 Simple Explanation

- **Abstract class** = "is-a" with shared code. `Dog` **is an** `Animal`.
- **Interface** = "can-do" ability. A `Bird` **can** `Fly`, a `Plane` **can** `Fly` too.

---

## 🧩 Example

```java
// Abstract class: shared code + rules
abstract class Animal {
    abstract void sound();          // must implement
    void sleep() {                  // shared code
        System.out.println("Sleeping...");
    }
}

// Interface: a capability
interface Swimmer {
    void swim();                    // just a contract
}

class Dog extends Animal implements Swimmer {
    void sound() { System.out.println("Bark"); }
    public void swim() { System.out.println("Dog paddles"); }
}
```

A class can **extend one** abstract class but **implement many** interfaces.

---

## 📋 Comparison Table

| Feature | Abstract Class | Interface |
|---------|---------------|-----------|
| Keyword | `abstract class` | `interface` |
| Methods | Abstract + concrete | Abstract (+ `default`/`static` since Java 8) |
| Fields | Any (variables) | `public static final` only (constants) |
| Constructor | Yes | No |
| Multiple inheritance | No (one only) | Yes (many) |
| Access modifiers | Any | Methods `public` by default |
| Use when | Share common **code** | Define common **behavior** |

---

## 🆕 Java 8+ Interface Features

```java
interface Payment {
    void pay();                          // abstract
    default void receipt() {             // default method (has body)
        System.out.println("Receipt generated");
    }
    static void info() {                 // static method
        System.out.println("Payment interface");
    }
}
```

---

## 🌍 Real-World Use Case

- `JpaRepository` in Spring Data is an **interface** — you just declare methods.
- A `BaseController` with common logging can be an **abstract class**.

---

## ❓ Interview Questions

1. When to use interface vs abstract class?
2. Can an interface have a constructor? (**No**)
3. Can an interface have method bodies? (**Yes**, `default`/`static` since Java 8)
4. Can an abstract class be `final`? (**No** — contradiction)
5. What is a functional interface? (**One abstract method**, e.g., `Runnable`)
6. Diamond problem with default methods — how resolved? (Override and use `Interface.super.method()`)

---

## ✅ Best Practices
- Prefer **interfaces** for flexibility and testing (mocking).
- Use abstract classes when there's **real shared implementation**.

## ⚠️ Common Mistakes
- Putting state (mutable fields) in interfaces.
- Overusing abstract classes where interfaces fit better.

---

## ⚡ Quick Revision Notes
- Abstract class = shared code, single inheritance, can have constructor.
- Interface = contract, multiple inheritance, `public static final` fields.
- Since Java 8, interfaces can have `default`/`static` methods.
- Functional interface = exactly one abstract method.

## 🙋 FAQs
**Q: Can a class extend a class and implement interfaces together?** Yes.

## 📎 References
- Oracle Docs — Interfaces and Inheritance

[⬅ Back to Java Index](./README.md)

