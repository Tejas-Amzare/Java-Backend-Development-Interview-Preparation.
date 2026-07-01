# 4. Trees, BST, Heap & Trie

> 🟡 **Level:** Intermediate | 🔥 **Interview Frequency:** Very High

---

## Part A — Binary Tree

### 🧠 Concept
A **tree** is a hierarchy of nodes. A **binary tree** = each node has **at most 2 children**
(left & right). The top node is the **root**; bottom nodes are **leaves**.

```
        1        ← root
       / \
      2   3
     / \
    4   5        ← leaves
```

### 🌳 Tree Traversals (very common!)
```
Inorder   (Left, Root, Right) → 4 2 5 1 3   (gives sorted order in BST)
Preorder  (Root, Left, Right) → 1 2 4 5 3
Postorder (Left, Right, Root) → 4 5 2 3 1
Level order (BFS, by level)   → 1 2 3 4 5
```

```java
class Node { int val; Node left, right; Node(int v){val=v;} }

void inorder(Node root) {
    if (root == null) return;
    inorder(root.left);
    System.out.print(root.val + " ");
    inorder(root.right);
}
```

---

## Part B — Binary Search Tree (BST)

### 🧠 Concept
A **BST** is a binary tree where: **left < root < right** for every node.
This gives **fast search, insert, delete** — **O(log n)** when balanced.

```
        8
       / \
      3   10
     / \    \
    1   6    14
```
> Inorder traversal of a BST gives values in **sorted order**.

```java
Node search(Node root, int key) {
    if (root == null || root.val == key) return root;
    return key < root.val ? search(root.left, key) : search(root.right, key);
}
```

⚠️ If unbalanced (like a straight line), BST degrades to **O(n)**. Balanced versions:
**AVL tree**, **Red-Black tree** (Java's `TreeMap`/`TreeSet` use Red-Black).

---

## Part C — Heap (Priority Queue)

### 🧠 Concept
A **heap** is a special tree kept as an array.
- **Min-heap** → smallest value on top.
- **Max-heap** → largest value on top.

Used to always get the **min/max quickly** — insert & remove in **O(log n)**, peek in **O(1)**.

```java
PriorityQueue<Integer> minHeap = new PriorityQueue<>();               // min
PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());
minHeap.offer(5); minHeap.offer(1); minHeap.offer(3);
minHeap.poll();   // 1
```

Use cases: **top K elements**, **Dijkstra's shortest path**, **task scheduling**, **median**.

---

## Part D — Trie (Prefix Tree)

### 🧠 Concept
A **Trie** stores strings **character by character** in a tree. Great for **prefix search**
and **autocomplete**.

```
root
 ├─ c ─ a ─ t   ("cat")
 │       └ r   ("car")
 └─ d ─ o ─ g   ("dog")
```

- Insert / search a word = **O(word length)**.
- Used in autocomplete, spell-check, IP routing, dictionaries.

---

## 🌍 Real-World Use Cases
- **Tree** → file systems, HTML DOM, org charts.
- **BST / TreeMap** → sorted data, range queries, leaderboards.
- **Heap** → priority scheduling, top-K, Dijkstra.
- **Trie** → search autocomplete, spell checkers.

---

## ❓ Most Asked Interview Questions
1. Tree traversals — inorder, preorder, postorder, level order.
2. What is a BST? Its time complexity?
3. How to validate a BST?
4. Find height / diameter of a tree.
5. Lowest Common Ancestor (LCA).
6. Difference between min-heap and max-heap?
7. How does a PriorityQueue work internally? (Binary heap)
8. What is a balanced tree (AVL / Red-Black)?
9. When would you use a Trie?
10. BFS vs DFS on a tree?

---

## 💻 Coding Example — Level Order (BFS)
```java
void levelOrder(Node root) {
    if (root == null) return;
    Queue<Node> q = new LinkedList<>();
    q.offer(root);
    while (!q.isEmpty()) {
        Node cur = q.poll();
        System.out.print(cur.val + " ");
        if (cur.left != null)  q.offer(cur.left);
        if (cur.right != null) q.offer(cur.right);
    }
}
```

---

## 🏆 Top LeetCode Problems
| # | Problem | Difficulty |
|---|---------|-----------|
| 104 | Maximum Depth of Binary Tree | Easy |
| 226 | Invert Binary Tree | Easy |
| 100 | Same Tree | Easy |
| 102 | Level Order Traversal | Medium |
| 98 | Validate BST | Medium |
| 235 | LCA of BST | Medium |
| 236 | LCA of Binary Tree | Medium |
| 215 | Kth Largest Element (heap) | Medium |
| 347 | Top K Frequent Elements | Medium |
| 208 | Implement Trie | Medium |
| 297 | Serialize/Deserialize Tree | Hard |

---

## ✅ Best Practices
- Use recursion for tree problems — it's natural.
- For "top K" or "min/max repeatedly" → think **heap**.
- For "prefix / autocomplete" → think **Trie**.

## ⚠️ Common Mistakes
- Forgetting the `null` base case in recursion.
- Assuming a BST is always balanced.
- Mixing up traversal orders.

---

## ⚡ Quick Revision Notes
- Binary tree: ≤ 2 children. Traversals: in/pre/post/level.
- BST: left < root < right; O(log n) balanced; inorder = sorted.
- Heap: min/max on top; PriorityQueue; O(log n) insert/remove.
- Trie: char-by-char string tree; great for prefixes/autocomplete.

## 🙋 FAQs
**Q: Which traversal gives sorted BST output?** Inorder.

## 📎 References
- LeetCode Tree / Heap / Trie tags

[⬅ Back to DSA Index](./README.md)

