# 2. Joins & Normalization

> 🟡 **Level:** Intermediate | 🔥 **Interview Frequency:** Very High

---

## Part A — Joins

### 🧠 Concept
A **JOIN** combines rows from **two or more tables** based on a related column (usually a
foreign key). This is how you read data spread across tables.

### 🗺️ Join Types Diagram
```
INNER JOIN        LEFT JOIN         RIGHT JOIN        FULL OUTER JOIN
  ( A ∩ B )       ( all A + match)  (all B + match)   ( all A + all B )

   A   B            A   B             A   B              A   B
  ( (X) )          (X( ) )           ( )X )            (X( )X)
```

| Join | Returns |
|------|---------|
| **INNER JOIN** | Only matching rows in both tables |
| **LEFT JOIN** | All from left + matches from right (NULL if none) |
| **RIGHT JOIN** | All from right + matches from left |
| **FULL OUTER JOIN** | All rows from both, matched where possible |
| **CROSS JOIN** | Every combination (Cartesian product) |
| **SELF JOIN** | Table joined with itself |

### 🧩 Examples
```sql
-- INNER JOIN: users who placed orders
SELECT u.name, o.order_id
FROM users u
INNER JOIN orders o ON u.id = o.user_id;

-- LEFT JOIN: all users, even those with no orders
SELECT u.name, o.order_id
FROM users u
LEFT JOIN orders o ON u.id = o.user_id;

-- SELF JOIN: employees and their managers
SELECT e.name AS emp, m.name AS manager
FROM employees e
JOIN employees m ON e.manager_id = m.id;
```

---

## Part B — Normalization

### 🧠 Concept
**Normalization** = organizing tables to **remove duplicate data** and avoid update problems.
We split big messy tables into smaller related ones.

### 📈 Normal Forms (simple)
| Form | Rule (simple words) |
|------|---------------------|
| **1NF** | No repeating groups; each cell holds one value |
| **2NF** | 1NF + every column depends on the **whole** primary key |
| **3NF** | 2NF + no column depends on another **non-key** column |
| **BCNF** | Stricter 3NF |

### Example
**Before (bad — repeated data):**
```
orders(order_id, customer_name, customer_city, product, price)
```
**After 3NF (split):**
```
customers(customer_id, name, city)
products(product_id, name, price)
orders(order_id, customer_id, product_id)
```

### Normalization vs Denormalization
| Normalization | Denormalization |
|---------------|-----------------|
| Less redundancy | Some redundancy |
| More tables, more joins | Fewer joins, faster reads |
| Better for writes | Better for read-heavy apps |

---

## 🌍 Real-World Use Case
A banking DB is heavily **normalized** for consistency. A reporting/analytics DB is often
**denormalized** for fast reads.

---

## ❓ Interview Questions
1. Explain INNER vs LEFT vs RIGHT JOIN.
2. What is a self join? When used?
3. What is normalization? Why do it?
4. Explain 1NF, 2NF, 3NF.
5. Normalization vs denormalization — when to use each?
6. What is a Cartesian product / cross join?
7. Difference between JOIN and UNION? (JOIN combines columns; UNION combines rows)

---

## 📋 JOIN vs UNION
| JOIN | UNION |
|------|-------|
| Combines **columns** (side by side) | Combines **rows** (stacked) |
| Based on a condition | Needs same columns/types |

---

## ✅ Best Practices
- Always specify the join **condition** (`ON`), else you get a Cartesian explosion.
- Normalize to at least **3NF** for transactional systems.
- Denormalize deliberately for read performance.

## ⚠️ Common Mistakes
- Forgetting `ON` → accidental cross join.
- Over-normalizing (too many joins hurt performance).
- Using WHERE instead of ON for outer joins (changes results).

---

## ⚡ Quick Revision Notes
- INNER = matches only; LEFT = all left + matches; RIGHT = all right + matches; FULL = both.
- SELF JOIN = table with itself (manager/employee).
- Normalization = remove redundancy (1NF → 2NF → 3NF).
- Denormalize for faster reads; JOIN = columns, UNION = rows.

## 🙋 FAQs
**Q: Default JOIN type?** `JOIN` alone = `INNER JOIN`.

## 📎 References
- Mode SQL Tutorial — Joins
- Use The Index, Luke

[⬅ Back to SQL Index](./README.md)

