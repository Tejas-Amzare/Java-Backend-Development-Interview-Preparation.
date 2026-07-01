# 4. Inheritance

> 🟢 **Level:** Beginner | 🔥 **Interview Frequency:** Very High

---

## 🧠 Concept

**Inheritance** lets one class **reuse** the fields and methods of another class.
- **Parent** class (super class) = gives features.
- **Child** class (sub class) = receives features using `extends`.

---

## 💬 Simple Explanation

A child inherits qualities from parents. Similarly, a child class gets the code of the parent
class for **free** and can add its own extra features.

This avoids writing the same code again → **code reuse**.

---

## 🧩 Example

```java
class Animal {
    void eat() { System.out.println("This animal eats food"); }
}

class Dog extends Animal {          // Dog inherits Animal
    void bark() { System.out.println("Dog barks"); }
}

public class Main {
    public static void main(String[] args) {
        Dog d = new Dog();
        d.eat();    // inherited from Animal
        d.bark();   // own method
    }
}
```

---

## 🗺️ Types of Inheritance

```
Single:        A → B
Multilevel:    A → B → C
Hierarchical:  A → B, A → C
Multiple:      (NOT allowed with classes in Java, only via interfaces)
```

> ❗ Java does **not** support multiple inheritance with classes (to avoid the *Diamond Problem*).
> It is allowed using **interfaces**.

---

## 🌍 Real-World Use Case

`BaseEntity` class holds common fields like `id`, `createdAt`, `updatedAt`.
All entities (`User`, `Order`, `Product`) extend it → no repeated code.

---

## ❓ Interview Questions

1. What is inheritance and why use it?
2. Why doesn't Java support multiple inheritance with classes?
3. What is the Diamond Problem?
4. What does `super` keyword do?
5. Difference between `this` and `super`?

---

## 💻 Coding Example — `super`

```java
class Vehicle {
    int speed = 50;
}
class Car extends Vehicle {
    int speed = 100;
    void show() {
        System.out.println(super.speed);  // 50 (parent)
        System.out.println(this.speed);   // 100 (child)
    }
}
```

---

## ✅ Best Practices
- Use inheritance only for a true **"is-a"** relationship (Dog **is an** Animal).
- Prefer **composition** ("has-a") when unsure.

## ⚠️ Common Mistakes
- Using inheritance just to reuse code when there's no real "is-a" link.
- Deep inheritance chains (hard to maintain).

---

## ⚡ Quick Revision Notes
- Inheritance = reuse parent code with `extends`.
- Types: single, multilevel, hierarchical (no multiple with classes).
- `super` = access parent; `this` = current object.

## 📋 Cheat Sheet

| Keyword | Use |
|---------|-----|
| `extends` | Inherit a class |
| `super()` | Call parent constructor |
| `super.x` | Access parent field/method |

## 🙋 FAQs
**Q: Are constructors inherited?** No, but child can call parent's via `super()`.

## 📎 References
- Oracle Docs — Inheritance

[⬅ Back to Java Index](./README.md)

