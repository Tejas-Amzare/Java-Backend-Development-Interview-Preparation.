# 3. Constructor

> 🟢 **Level:** Beginner | ⭐ **Interview Frequency:** High

---

## 🧠 Concept

A **constructor** is a special method that runs **automatically** when an object is created.
Its job is to **set up (initialize)** the object.

Rules:
- Name is **same as the class name**.
- **No return type** (not even `void`).

---

## 💬 Simple Explanation

When you buy a new phone, it comes **pre-set** with basic settings.
A constructor is that "setup" step that runs the moment your object is born.

---

## 🧩 Types of Constructors

```java
class Student {
    String name;
    int age;

    Student() {                       // 1. Default (no-arg) constructor
        name = "Unknown";
    }

    Student(String n, int a) {        // 2. Parameterized constructor
        name = n;
        age = a;
    }

    Student(Student s) {              // 3. Copy constructor
        this.name = s.name;
        this.age = s.age;
    }
}
```

| Type | Meaning |
|------|---------|
| Default | No parameters, Java adds it if you write none |
| Parameterized | Takes values to set fields |
| Copy | Creates a new object by copying another |

---

## 🌍 Real-World Use Case

When creating a `DatabaseConnection` object, the constructor opens the connection with
the given host, username, and password.

---

## ❓ Interview Questions

1. What is a constructor? Can it be `private`? (**Yes** — used in Singleton pattern)
2. Difference between constructor and method?
3. Can a constructor be `final`, `static`, or `abstract`? (**No**)
4. What is constructor overloading?
5. What is constructor chaining? (`this()` and `super()`)

---

## 💻 Coding Example — Constructor Chaining

```java
class A {
    A() {
        System.out.println("Parent constructor");
    }
}
class B extends A {
    B() {
        super();   // calls A() first
        System.out.println("Child constructor");
    }
}
// Output: Parent constructor -> Child constructor
```

---

## ✅ Best Practices
- Use constructors to set **required** fields.
- Use `this()` to avoid repeating code between constructors.

## ⚠️ Common Mistakes
- Adding a return type (then it becomes a normal method, not a constructor!).
- Forgetting Java removes the default constructor once you write a parameterized one.

---

## ⚡ Quick Revision Notes
- Constructor = same name as class, no return type, runs on object creation.
- Types: default, parameterized, copy.
- `this()` = call another constructor in same class; `super()` = call parent constructor.

## 📋 Cheat Sheet

| Constructor | Method |
|-------------|--------|
| Same name as class | Any name |
| No return type | Has return type |
| Called automatically | Called explicitly |

## 🙋 FAQs
**Q: Does every class have a constructor?** Yes — if you don't write one, Java adds a default.

## 📎 References
- Oracle Docs — Providing Constructors

[⬅ Back to Java Index](./README.md)

