# 5. Polymorphism

> 🟢 **Level:** Beginner | 🔥 **Interview Frequency:** Very High

---

## 🧠 Concept

**Polymorphism** means **"many forms"**. The same method name behaves **differently**
depending on the situation.

Two types:
1. **Compile-time (Static)** → Method **Overloading**
2. **Runtime (Dynamic)** → Method **Overriding**

---

## 💬 Simple Explanation

The word "cut" means different things:
- Cut a cake 🍰
- Cut hair 💇
- Cut a call 📞

Same word, different action based on context → that's polymorphism.

---

## 🧩 Method Overloading (Compile-time)

Same method name, **different parameters**, in the **same class**.

```java
class Calculator {
    int add(int a, int b) { return a + b; }
    double add(double a, double b) { return a + b; }
    int add(int a, int b, int c) { return a + b + c; }
}
```

## 🧩 Method Overriding (Runtime)

Child class **redefines** a parent method with the **same signature**.

```java
class Animal {
    void sound() { System.out.println("Some sound"); }
}
class Dog extends Animal {
    @Override
    void sound() { System.out.println("Bark"); }
}

Animal a = new Dog();
a.sound();   // Output: Bark  (decided at runtime)
```

---

## 🗺️ Diagram

```
POLYMORPHISM
   |
   ├── Overloading  (same class, different params)   → compile time
   └── Overriding   (child redefines parent method)  → runtime
```

---

## 🌍 Real-World Use Case

A `PaymentService` has method `pay()`. `CreditCardPayment`, `UpiPayment`, and `PaypalPayment`
each **override** `pay()` with their own logic. Code calls `pay()` and the right version runs.

---

## ❓ Interview Questions

1. Difference between overloading and overriding?
2. Can we override a `static` method? (**No** — it's hidden, not overridden)
3. Can we override a `private` or `final` method? (**No**)
4. What is dynamic method dispatch?
5. Can the return type differ in overriding? (**Covariant** return types allowed)

---

## 📋 Overloading vs Overriding

| Feature | Overloading | Overriding |
|---------|-------------|------------|
| Where | Same class | Parent & child |
| Params | Must differ | Must be same |
| Time | Compile-time | Runtime |
| Return type | Can differ | Same or covariant |
| Keyword | — | `@Override` |

---

## ✅ Best Practices
- Always add `@Override` — the compiler catches mistakes.
- Keep overloaded methods logically similar.

## ⚠️ Common Mistakes
- Thinking changing only return type = overloading (it's not).
- Trying to override `static`/`final`/`private` methods.

---

## ⚡ Quick Revision Notes
- Polymorphism = many forms.
- Overloading = compile-time, same class, different params.
- Overriding = runtime, child redefines parent method.

## 🙋 FAQs
**Q: Which OOP pillar makes code flexible/extensible?** Polymorphism.

## 📎 References
- Oracle Docs — Polymorphism

[⬅ Back to Java Index](./README.md)

