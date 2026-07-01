# 6. Abstraction

> 🟢 **Level:** Beginner | ⭐ **Interview Frequency:** High

---

## 🧠 Concept

**Abstraction** means **hiding complex details** and showing only the **important parts**.

Achieved using:
- **Abstract class** (partial abstraction)
- **Interface** (full abstraction, before Java 8)

---

## 💬 Simple Explanation

When you drive a car, you just use the **steering, brake, accelerator**.
You don't need to know how the engine works inside. The complexity is **hidden**.

That's abstraction — show *what* it does, hide *how* it does it.

---

## 🧩 Example — Abstract Class

```java
abstract class Shape {
    abstract double area();          // no body — child must implement

    void describe() {                // normal method allowed too
        System.out.println("I am a shape");
    }
}

class Circle extends Shape {
    double r;
    Circle(double r) { this.r = r; }
    double area() { return 3.14 * r * r; }
}
```

## 🧩 Example — Interface

```java
interface Payment {
    void pay(double amount);   // only "what", not "how"
}

class UpiPayment implements Payment {
    public void pay(double amount) {
        System.out.println("Paid " + amount + " via UPI");
    }
}
```

---

## 🌍 Real-World Use Case

A `NotificationService` interface has `send()`. The caller doesn't care if it's Email, SMS,
or Push — it just calls `send()`. Implementation details are **hidden**.

---

## ❓ Interview Questions

1. What is abstraction? How is it achieved in Java?
2. Difference between abstraction and encapsulation?
3. Can we create an object of an abstract class? (**No**)
4. Can an abstract class have a constructor? (**Yes**)
5. Can an abstract class have non-abstract methods? (**Yes**)

---

## 📋 Abstraction vs Encapsulation

| Abstraction | Encapsulation |
|-------------|---------------|
| Hides **complexity** | Hides **data** |
| Design level (what) | Implementation level (how) |
| Abstract class / interface | `private` + getters/setters |

---

## ✅ Best Practices
- Program to an **interface**, not a concrete class.
- Keep abstract methods focused on behavior.

## ⚠️ Common Mistakes
- Trying to instantiate an abstract class.
- Confusing abstraction (hide complexity) with encapsulation (hide data).

---

## ⚡ Quick Revision Notes
- Abstraction = hide details, show essentials.
- Abstract class = partial; interface = full abstraction.
- Can't create object of abstract class.

## 🙋 FAQs
**Q: When to use abstract class vs interface?** See [Interface vs Abstract Class](./08-Interface-vs-Abstract-Class.md).

## 📎 References
- Oracle Docs — Abstract Methods and Classes

[⬅ Back to Java Index](./README.md)

