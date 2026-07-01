# 1. OOP Concepts (Object-Oriented Programming)

> 🟢 **Level:** Beginner | 🔥 **Interview Frequency:** Very High

---

## 🧠 Concept

**OOP** is a way of writing programs using **objects**. An object is a real-world thing
that has **data** (fields) and **actions** (methods).

Java has **4 pillars** of OOP:

1. **Encapsulation** — hide data, protect it
2. **Inheritance** — reuse code from a parent
3. **Polymorphism** — one name, many forms
4. **Abstraction** — hide details, show only what matters

Remember them with **A PIE** → **A**bstraction, **P**olymorphism, **I**nheritance, **E**ncapsulation.

---

## 💬 Simple Explanation

Think of a **Car**.
- It has data: color, speed, model → these are **fields**.
- It has actions: start(), brake(), accelerate() → these are **methods**.

Instead of writing loose code, we group related data + actions into one unit (a **class**).
This makes code **clean, reusable, and easy to manage**.

---

## 🧩 Example

```java
class Car {
    String color;          // data
    int speed;             // data

    void start() {         // action
        System.out.println("Car started");
    }
    void accelerate() {    // action
        speed += 10;
        System.out.println("Speed is " + speed);
    }
}

public class Main {
    public static void main(String[] args) {
        Car myCar = new Car();   // object created
        myCar.color = "Red";
        myCar.start();
        myCar.accelerate();
    }
}
```

---

## 🌍 Real-World Use Case

- **Banking app:** `Account` object holds balance and methods `deposit()`, `withdraw()`.
- **E-commerce:** `Product`, `Cart`, `Order` are all objects.
- OOP keeps large backend systems **organized and maintainable**.

---

## 🗺️ Diagram

```
        OBJECT-ORIENTED PROGRAMMING
                    |
   ------------------------------------
   |          |            |          |
Encapsul-  Inheritance Polymorphism Abstraction
 ation     (reuse)     (many forms) (hide details)
 (protect)
```

---

## ❓ Interview Questions

1. What are the 4 pillars of OOP? Explain each in one line.
2. Why is Java called an object-oriented language?
3. Difference between OOP and procedural programming?
4. Can you write a real-life example of encapsulation?
5. Is Java 100% object-oriented? (**No** — it uses primitive types like `int`, `char`.)

---

## ✅ Best Practices

- Keep fields **private**, expose them via methods (getters/setters).
- One class should do **one job** (Single Responsibility).
- Prefer **composition** over inheritance when possible.

---

## ⚠️ Common Mistakes

- Making all fields `public` (breaks encapsulation).
- Putting too much logic in one giant class.
- Confusing **class** (blueprint) with **object** (real thing).

---

## ⚡ Quick Revision Notes

- OOP = programming with **objects** (data + actions).
- 4 pillars: **A PIE** → Abstraction, Polymorphism, Inheritance, Encapsulation.
- Class = blueprint, Object = real instance.
- Java is **not 100%** OO (has primitives).

---

## 📋 Cheat Sheet

| Pillar | One-line meaning | Keyword |
|--------|------------------|---------|
| Encapsulation | Hide & protect data | `private` + getters/setters |
| Inheritance | Reuse parent code | `extends` |
| Polymorphism | One name, many forms | overloading / overriding |
| Abstraction | Hide details | `abstract`, `interface` |

---

## 🙋 FAQs

**Q: Is abstraction same as encapsulation?**
No. Abstraction hides **complexity** (what to show). Encapsulation hides **data** (how to protect).

**Q: Why use OOP in backend?**
It makes code modular, reusable, testable, and easy for teams to maintain.


---

## 📎 References

- Oracle Java Tutorials: OOP concepts
- *Head First Java* — beginner friendly
- Baeldung.com — practical Java articles

[⬅ Back to Java Index](./README.md)

