# 5. Graphs & Hashing

> 🔴 **Level:** Advanced | ⭐ **Interview Frequency:** High

---

## Part A — Graphs

### 🧠 Concept
A **graph** is a set of **nodes (vertices)** connected by **edges**. Unlike trees, graphs can have
**cycles** and **any** connections.

```
   A --- B
   |   / |
   | /   |
   C --- D
```

Types: **Directed** (one-way) / **Undirected** (two-way), **Weighted** (edges have cost) / Unweighted.

### 📦 Representation
```java
// Adjacency list (most common) - node -> list of neighbors
Map<Integer, List<Integer>> graph = new HashMap<>();
graph.put(0, List.of(1, 2));
graph.put(1, List.of(2));
```

### 🚶 Traversals

**BFS (Breadth-First)** — level by level, uses a **Queue**. Finds shortest path in unweighted graphs.
```java
void bfs(int start, Map<Integer, List<Integer>> g) {
    Queue<Integer> q = new LinkedList<>();
    Set<Integer> seen = new HashSet<>();
    q.offer(start); seen.add(start);
    while (!q.isEmpty()) {
        int node = q.poll();
        System.out.print(node + " ");
        for (int nb : g.getOrDefault(node, List.of())) {
            if (seen.add(nb)) q.offer(nb);
        }
    }
}
```

**DFS (Depth-First)** — go deep first, uses **recursion/stack**.
```java
void dfs(int node, Map<Integer, List<Integer>> g, Set<Integer> seen) {
    if (!seen.add(node)) return;
    System.out.print(node + " ");
    for (int nb : g.getOrDefault(node, List.of())) dfs(nb, g, seen);
}
```

### 🧭 Important Graph Algorithms
| Algorithm | Use |
|-----------|-----|
| BFS | Shortest path (unweighted) |
| DFS | Explore, cycle detection, connected components |
| Dijkstra | Shortest path (weighted, no negatives) |
| Bellman-Ford | Shortest path with negative edges |
| Topological Sort | Order tasks with dependencies (DAG) |
| Union-Find | Detect cycles, connected components |
| Prim / Kruskal | Minimum Spanning Tree |

---

## Part B — Hashing

### 🧠 Concept
**Hashing** converts a key into an **index** using a **hash function**, giving **O(1)** average
lookup. This is how `HashMap` and `HashSet` are so fast.

```
key "Aman" --hash()--> 4382 --% size--> bucket 5
```

- **Collision** = two keys land in the same bucket. Handled by **chaining** (linked list/tree)
  or **open addressing**.
- **Load factor** = filled/size. HashMap resizes at **0.75**.

### 🧩 Common Hashing Uses
```java
// Count frequency - O(n)
Map<Character, Integer> freq = new HashMap<>();
for (char c : s.toCharArray())
    freq.merge(c, 1, Integer::sum);

// Fast lookup / duplicates
Set<Integer> seen = new HashSet<>();
```

---

## 🌍 Real-World Use Cases
- **Graphs** → Google Maps (routes), social networks (friends), dependency resolution.
- **Hashing** → caches, database indexes, deduplication, symbol tables.

---

## ❓ Most Asked Interview Questions
1. BFS vs DFS — when to use each?
2. How to detect a cycle in a graph?
3. What is topological sort?
4. Explain Dijkstra's algorithm.
5. How does a hash table handle collisions?
6. What is a good hash function?
7. Time complexity of HashMap operations? (O(1) average, O(n) worst)
8. Difference between HashMap and HashSet?
9. How to find connected components?
10. What is Union-Find (Disjoint Set)?

---

## 🏆 Top LeetCode Problems
| # | Problem | Difficulty |
|---|---------|-----------|
| 200 | Number of Islands | Medium |
| 133 | Clone Graph | Medium |
| 207 | Course Schedule (topo sort) | Medium |
| 994 | Rotting Oranges (BFS) | Medium |
| 417 | Pacific Atlantic Water Flow | Medium |
| 743 | Network Delay Time (Dijkstra) | Medium |
| 684 | Redundant Connection (Union-Find) | Medium |
| 1 | Two Sum (hashing) | Easy |
| 128 | Longest Consecutive Sequence | Medium |
| 49 | Group Anagrams | Medium |

---

## ✅ Best Practices
- Track visited nodes with a `Set` to avoid infinite loops.
- Choose adjacency **list** for sparse graphs (memory efficient).
- Use hashing for O(1) lookups instead of scanning lists.

## ⚠️ Common Mistakes
- Forgetting to mark nodes visited → infinite loop.
- Using bad hash keys (mutable objects) in HashMap.
- Confusing BFS (queue) with DFS (stack/recursion).

---

## ⚡ Quick Revision Notes
- Graph = nodes + edges; can have cycles. Store as adjacency list.
- BFS = queue, shortest path (unweighted). DFS = recursion/stack.
- Dijkstra = weighted shortest path; Topo sort = task ordering.
- Hashing = O(1) average via hash function; collisions via chaining; load factor 0.75.

## 🙋 FAQs
**Q: BFS or DFS for shortest path in an unweighted graph?** BFS.

## 📎 References
- LeetCode Graph / Hash Table tags

[⬅ Back to DSA Index](./README.md)

