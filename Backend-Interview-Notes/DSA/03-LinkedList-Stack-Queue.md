# 3. Linked List, Stack & Queue

> 🟡 **Level:** Intermediate | 🔥 **Interview Frequency:** Very High

---

## Part A — Linked List

### 🧠 Concept
A **linked list** is a chain of **nodes**. Each node holds **data** + a **pointer** to the next node.
Unlike arrays, nodes are **not** stored together in memory.

```
[10|•]→[20|•]→[30|•]→null
 head
```

Types: **Singly** (one direction), **Doubly** (both directions), **Circular** (last points to first).

### 🧩 Java Node + Reverse
```java
class Node {
    int data;
    Node next;
    Node(int d) { data = d; }
}

// Reverse a singly linked list - O(n)
Node reverse(Node head) {
    Node prev = null, curr = head;
    while (curr != null) {
        Node next = curr.next;
        curr.next = prev;
        prev = curr;
        curr = next;
    }
    return prev;   // new head
}
```

### Array vs Linked List
| | Array | Linked List |
|-|-------|-------------|
| Memory | Contiguous | Scattered (pointers) |
| Access | O(1) | O(n) |
| Insert/delete | O(n) | O(1) at node |
| Size | Fixed | Dynamic |

---

## Part B — Stack (LIFO)

### 🧠 Concept
**Stack** = Last In, First Out. Like a stack of plates — add/remove from the **top** only.

```
push→ | 30 | ←pop (top)
      | 20 |
      | 10 |
```

### 🧩 Java
```java
Deque<Integer> stack = new ArrayDeque<>();   // preferred over Stack class
stack.push(10);
stack.push(20);
stack.peek();   // 20 (top, without removing)
stack.pop();    // 20 (remove top)
```

Operations: `push`, `pop`, `peek` — all **O(1)**.

---

## Part C — Queue (FIFO)

### 🧠 Concept
**Queue** = First In, First Out. Like a line at a ticket counter — enter at back, leave from front.

```
front →[10][20][30]← back
       poll        offer
```

### 🧩 Java
```java
Queue<Integer> q = new LinkedList<>();
q.offer(10);      // add at back
q.offer(20);
q.peek();         // 10 (front)
q.poll();         // 10 (remove front)

Deque<Integer> dq = new ArrayDeque<>();   // double-ended queue
```

---

## 🌍 Real-World Use Cases
- **Stack** → browser back button, undo/redo, function call stack, expression evaluation.
- **Queue** → printer jobs, task scheduling, message queues (Kafka/RabbitMQ idea).
- **Linked List** → music playlists (next/prev), LRU cache.

---

## ❓ Most Asked Interview Questions
1. Difference between array and linked list?
2. How to reverse a linked list?
3. How to detect a loop in a linked list? (**Floyd's slow/fast pointers**)
4. Find the middle of a linked list.
5. Implement a stack using arrays / two queues.
6. Implement a queue using two stacks.
7. What is a deque?
8. Difference between Stack class and ArrayDeque? (ArrayDeque is faster, non-legacy)

---

## 💻 Coding Example — Detect Cycle (Floyd's)
```java
boolean hasCycle(Node head) {
    Node slow = head, fast = head;
    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
        if (slow == fast) return true;   // they meet → cycle
    }
    return false;
}
```

---

## 🏆 Top LeetCode Problems
| # | Problem | Difficulty |
|---|---------|-----------|
| 206 | Reverse Linked List | Easy |
| 21 | Merge Two Sorted Lists | Easy |
| 141 | Linked List Cycle | Easy |
| 143 | Reorder List | Medium |
| 19 | Remove Nth Node From End | Medium |
| 20 | Valid Parentheses (stack) | Easy |
| 155 | Min Stack | Medium |
| 232 | Queue using Stacks | Easy |
| 622 | Design Circular Queue | Medium |
| 146 | LRU Cache | Medium |

---

## ✅ Best Practices
- Use `ArrayDeque` for stack/queue (not legacy `Stack`/`Vector`).
- Draw the pointers on paper for linked list problems.
- Use dummy/head nodes to simplify edge cases.

## ⚠️ Common Mistakes
- Losing the `next` reference while reversing (save it first!).
- NullPointerException at list ends.
- Confusing LIFO (stack) with FIFO (queue).

---

## ⚡ Quick Revision Notes
- Linked list = nodes with pointers; O(1) insert/delete, O(n) access.
- Stack = LIFO (push/pop/peek). Queue = FIFO (offer/poll/peek).
- Cycle detection = slow + fast pointers (Floyd's).
- Use `ArrayDeque` for both stack and queue.

## 🙋 FAQs
**Q: Which is better for a stack — `Stack` or `ArrayDeque`?** `ArrayDeque` (faster, not synchronized/legacy).

## 📎 References
- LeetCode Linked List / Stack / Queue tags

[⬅ Back to DSA Index](./README.md)

