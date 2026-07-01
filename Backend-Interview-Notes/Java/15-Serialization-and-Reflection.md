# 15. Serialization & Reflection

> 🔴 **Level:** Advanced | ✅ **Interview Frequency:** Medium

---

## Part A — Serialization

### 🧠 Concept
**Serialization** = converting an object into a **stream of bytes** so it can be **saved to a file**
or **sent over a network**. **Deserialization** = turning those bytes back into an object.

### 💬 Simple Explanation
Like **packing** furniture into a flat box to move it (serialize), then **assembling** it back
at the new house (deserialize).

### 🧩 Example
```java
class User implements Serializable {   // must implement Serializable
    private static final long serialVersionUID = 1L;
    String name;
    transient String password;         // 'transient' = NOT serialized
}

// Serialize
ObjectOutputStream out = new ObjectOutputStream(new FileOutputStream("user.ser"));
out.writeObject(user);

// Deserialize
ObjectInputStream in = new ObjectInputStream(new FileInputStream("user.ser"));
User u = (User) in.readObject();
```

### 🔑 Key Points
- Must implement `Serializable` (a marker interface — no methods).
- `transient` fields are **skipped** (e.g., passwords).
- `serialVersionUID` = version check between save & load.

### 🌍 Real-World Use Case
Storing session data, caching objects, sending objects between microservices.

### ❓ Interview Questions
1. What is serialization?
2. What is the `transient` keyword?
3. What is `serialVersionUID` and why use it?
4. Difference between `Serializable` and `Externalizable`?
5. Are `static` fields serialized? (**No**)

---

## Part B — Reflection

### 🧠 Concept
**Reflection** lets a program **inspect and change** classes, methods, and fields **at runtime**,
even private ones.

### 💬 Simple Explanation
It's like an **X-ray** 🩻 that lets code look inside another class while it's running.

### 🧩 Example
```java
Class<?> c = Class.forName("com.app.User");
Object obj = c.getDeclaredConstructor().newInstance();

Method[] methods = c.getDeclaredMethods();   // list all methods
Field f = c.getDeclaredField("name");
f.setAccessible(true);                        // access private field
f.set(obj, "Aman");
```

### 🌍 Real-World Use Case
Frameworks like **Spring** and **Hibernate** use reflection to create beans, inject
dependencies, and map database rows to objects — without you writing that wiring.

### ❓ Interview Questions
1. What is reflection?
2. Where is reflection used in real frameworks?
3. Disadvantages of reflection? (Slow, breaks encapsulation, security risk)
4. How does Spring use reflection?

---

## ✅ Best Practices
- Use `transient` for sensitive/derived fields.
- Always define `serialVersionUID`.
- Avoid reflection in normal code — it's slow and unsafe; let frameworks use it.

## ⚠️ Common Mistakes
- Forgetting `Serializable` → `NotSerializableException`.
- Overusing reflection (performance + maintainability hit).

---

## ⚡ Quick Revision Notes
- Serialization = object → bytes; Deserialization = bytes → object.
- `transient` skips a field; `static` also not serialized.
- `serialVersionUID` = version safety.
- Reflection = inspect/modify classes at runtime; powers Spring/Hibernate.

## 🙋 FAQs
**Q: Why is reflection slow?** It bypasses compile-time checks and JVM optimizations.

## 📎 References
- Oracle Docs — Serializable, Reflection API

[⬅ Back to Java Index](./README.md)

