# 2. Class & Object

> 🟢 **Level:** Beginner | 🔥 **Interview Frequency:** Very High

---

## 🧠 Concept

- **Class** = a blueprint / template. It defines what an object *will have*.
- **Object** = a real thing made from that blueprint. It *actually exists* in memory.

---

## 💬 Simple Explanation

A **class** is like a **house map (design)**.
An **object** is the **actual house** built from that map.

From one map, you can build **many houses** → from one class, you can create **many objects**.

---

## 🧩 Example

```java
class Student {          // CLASS (blueprint)
    String name;
    int age;

    void study() {
        System.out.println(name + " is studying");
    }
}

public class Main {
    public static void main(String[] args) {
        Student s1 = new Student();   // OBJECT 1
        s1.name = "Aman";
        s1.age = 21;
        s1.study();

        Student s2 = new Student();   // OBJECT 2
        s2.name = "Riya";
        s2.study();
    }
}
```

---

## 🌍 Real-World Use Case

In a backend app, `User` is a class. Every person who signs up becomes a **User object**
with their own name, email, and password.

---

## 🗺️ Diagram

```
   CLASS: Student (blueprint)
   ┌─────────────────────────┐
   │ name, age               │
   │ study()                 │
   └─────────────────────────┘
            │  new
   ┌────────┴────────┐
   ▼                 ▼
 Object s1        Object s2
 (Aman, 21)       (Riya, 20)
```

---

## ❓ Interview Questions

1. Difference between class and object?
2. How is an object created in Java? (`new` keyword)
3. Where are objects stored? (**Heap** memory)
4. Can we create an object without `new`? (Yes — via `newInstance()`, cloning, deserialization, factory)
5. What is a `this` keyword?

---

## 💻 Coding Example — `this` keyword

```java
class Student {
    String name;
    Student(String name) {
        this.name = name;   // "this" points to current object's field
    }
}
```

---

## ✅ Best Practices

- Use meaningful class names (nouns): `Order`, `Invoice`, `Customer`.
- Keep one public class per file, matching the file name.

## ⚠️ Common Mistakes

- Thinking a class takes memory (it doesn't — only **objects** do).
- Forgetting `new` while creating an object.

---

## ⚡ Quick Revision Notes

- Class = blueprint (no memory). Object = real instance (heap memory).
- Object created with `new`.
- `this` = current object reference.

## 📋 Cheat Sheet

| Term | Memory | Created by |
|------|--------|-----------|
| Class | Method area (metadata) | writing code |
| Object | Heap | `new` |

## 🙋 FAQs

**Q: How many objects can one class create?** Unlimited.

## 📎 References
- Oracle Docs — Classes and Objects

[⬅ Back to Java Index](./README.md)

