# 9. Collections Framework

> 🟡 **Level:** Intermediate | 🔥 **Interview Frequency:** Very High

The Collections Framework is a set of ready-made classes to **store and manage groups of objects**
(lists, sets, maps, queues). This is one of the **most asked** Java interview topics.

---

## 🗺️ Big Picture Diagram

```
                Iterable
                    │
              Collection ───────────────┐
              /     │      \            (Map is separate!)
           List    Set     Queue          Map
            │       │        │             │
       ArrayList  HashSet  PriorityQueue  HashMap
       LinkedList TreeSet   Deque         TreeMap
       Vector     LinkedHS  ArrayDeque    LinkedHashMap
       Stack                              Hashtable
```

> ⚠️ **Map is NOT a child of Collection** — common interview trick!

---

## 1️⃣ List — ordered, allows duplicates

Keeps insertion order, index-based (like a resizable array).

```java
List<String> names = new ArrayList<>();
names.add("Aman");
names.add("Aman");   // duplicates allowed
names.get(0);        // access by index
```

### ArrayList vs LinkedList 🔥

| Feature | ArrayList | LinkedList |
|---------|-----------|------------|
| Internal | Dynamic array | Doubly linked list |
| Access by index | Fast O(1) | Slow O(n) |
| Insert/delete middle | Slow O(n) | Fast O(1) (at known node) |
| Memory | Less | More (stores pointers) |
| Best for | Reading/searching | Frequent add/remove |

**Vector** = like ArrayList but **synchronized** (thread-safe, slower, legacy).
**Stack** = LIFO, extends Vector (legacy — prefer `ArrayDeque`).

---

## 2️⃣ Set — no duplicates

```java
Set<Integer> s = new HashSet<>();
s.add(1); s.add(1);   // stored only once
```

| Set Type | Order | Notes |
|----------|-------|-------|
| **HashSet** | No order | Fastest, allows one `null` |
| **LinkedHashSet** | Insertion order | Slightly slower |
| **TreeSet** | Sorted order | Uses Red-Black tree, no `null` |

---

## 3️⃣ Map — key → value pairs

```java
Map<String, Integer> ages = new HashMap<>();
ages.put("Aman", 21);
ages.get("Aman");          // 21
ages.getOrDefault("Riya", 0);
```

| Map Type | Order | Null keys | Thread-safe |
|----------|-------|-----------|-------------|
| **HashMap** | No order | 1 null key | No |
| **LinkedHashMap** | Insertion order | 1 null key | No |
| **TreeMap** | Sorted by key | No null key | No |
| **Hashtable** | No order | No null | Yes (legacy) |
| **ConcurrentHashMap** | No order | No null | Yes (modern) |

### How HashMap works (very common!) 🔥
1. Computes `hashCode()` of the key → decides the **bucket**.
2. If two keys land in same bucket (collision), they form a **linked list**.
3. In Java 8+, if a bucket gets too big (>8), it becomes a **balanced tree** (O(log n)).
4. `equals()` decides if a key already exists.

```
key --hashCode()--> bucket index --equals()--> find/replace value
```

---

## 4️⃣ Queue — FIFO (First In, First Out)

```java
Queue<Integer> q = new LinkedList<>();
q.offer(1); q.offer(2);
q.poll();    // removes 1 (front)
```

- **PriorityQueue** → elements come out in **priority (sorted) order**, not insertion order.
- **ArrayDeque** → double-ended queue, best for stack & queue use.

```java
PriorityQueue<Integer> pq = new PriorityQueue<>();  // min-heap by default
pq.offer(5); pq.offer(1); pq.offer(3);
pq.poll();   // 1 (smallest first)
```

---

## 5️⃣ Iterator — walk through a collection

```java
Iterator<String> it = names.iterator();
while (it.hasNext()) {
    String n = it.next();
    if (n.equals("Aman")) it.remove();  // safe removal
}
```

> ⚠️ Removing while using a normal for-each loop causes `ConcurrentModificationException`.
> Use `Iterator.remove()` or `removeIf()`.

---

## 6️⃣ Comparable vs Comparator 🔥

Used to **sort** objects.

| Comparable | Comparator |
|------------|------------|
| `compareTo()` | `compare()` |
| Inside the class | Separate class/lambda |
| **One** natural order | **Many** custom orders |
| `Collections.sort(list)` | `Collections.sort(list, comparator)` |

```java
// Comparable - natural order (by age)
class Student implements Comparable<Student> {
    int age;
    public int compareTo(Student o) { return this.age - o.age; }
}

// Comparator - custom order (by name)
Comparator<Student> byName = (a, b) -> a.name.compareTo(b.name);
list.sort(byName);
list.sort(Comparator.comparingInt(s -> s.age));   // modern style
```

---

## 🌍 Real-World Use Cases
- **ArrayList** → list of products on a page.
- **HashMap** → cache of userId → user data.
- **HashSet** → unique visitor IDs.
- **PriorityQueue** → task scheduler (highest priority first).
- **TreeMap** → leaderboard sorted by score.

---

## ❓ Interview Questions
1. Difference between ArrayList and LinkedList?
2. How does HashMap work internally?
3. Difference between HashMap and ConcurrentHashMap?
4. HashSet vs TreeSet?
5. Comparable vs Comparator?
6. What is the load factor of HashMap? (**0.75** — resizes when 75% full)
7. Why is Map not part of the Collection interface?
8. What is fail-fast vs fail-safe iterator?
9. How to make a collection thread-safe? (`Collections.synchronizedList`, concurrent classes)
10. Difference between `Iterator` and `ListIterator`?

---

## ✅ Best Practices
- Program to the **interface**: `List<String> list = new ArrayList<>();`
- Choose the right structure for the job (read-heavy → ArrayList, key lookup → HashMap).
- Use `ConcurrentHashMap` for multithreaded maps, not `Hashtable`.
- Override **both** `hashCode()` and `equals()` when using objects as keys.

## ⚠️ Common Mistakes
- Modifying a list inside a for-each loop → `ConcurrentModificationException`.
- Using objects as HashMap keys without overriding `equals()`/`hashCode()`.
- Assuming HashMap keeps insertion order (it doesn't).

---

## ⚡ Quick Revision Notes
- **List** = ordered + duplicates. **Set** = unique. **Map** = key-value. **Queue** = FIFO.
- ArrayList = fast read; LinkedList = fast insert/delete.
- HashMap = no order; TreeMap = sorted; LinkedHashMap = insertion order.
- Comparable = 1 natural order (`compareTo`); Comparator = many custom orders (`compare`).
- HashMap load factor = 0.75; treeifies bucket after 8 collisions.

## 📋 Cheat Sheet

| Need | Use |
|------|-----|
| Ordered list, fast read | `ArrayList` |
| Frequent add/remove | `LinkedList` |
| Unique items | `HashSet` |
| Unique + sorted | `TreeSet` |
| Key-value lookup | `HashMap` |
| Key-value sorted | `TreeMap` |
| Priority order | `PriorityQueue` |
| Thread-safe map | `ConcurrentHashMap` |

## 🙋 FAQs
**Q: Which is faster, HashMap or TreeMap?** HashMap (O(1)) vs TreeMap (O(log n)), but TreeMap keeps keys sorted.

## 📎 References
- Oracle Docs — Collections Framework
- Baeldung — Java Collections guides

[⬅ Back to Java Index](./README.md)

