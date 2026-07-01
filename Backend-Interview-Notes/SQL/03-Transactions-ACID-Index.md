# 3. Transactions, ACID & Indexes

> 🟡 **Level:** Intermediate | 🔥 **Interview Frequency:** Very High

---

## Part A — Transactions

### 🧠 Concept
A **transaction** is a group of SQL operations treated as **one single unit** — either
**all succeed** or **none do**.

```sql
BEGIN;
UPDATE accounts SET balance = balance - 100 WHERE id = 1;  -- withdraw
UPDATE accounts SET balance = balance + 100 WHERE id = 2;  -- deposit
COMMIT;    -- save both
-- ROLLBACK;  -- undo everything if something failed
```

If the second update fails, `ROLLBACK` undoes the first too — money is never lost.

---

## Part B — ACID Properties (must know!)

| Letter | Property | Simple meaning |
|--------|----------|----------------|
| **A** | Atomicity | All or nothing |
| **C** | Consistency | DB stays valid (rules kept) |
| **I** | Isolation | Transactions don't disturb each other |
| **D** | Durability | Once committed, stays saved (even after crash) |

### Isolation Levels & Problems
| Level | Dirty Read | Non-repeatable Read | Phantom Read |
|-------|-----------|---------------------|--------------|
| Read Uncommitted | ✅ possible | ✅ | ✅ |
| Read Committed | ❌ | ✅ | ✅ |
| Repeatable Read | ❌ | ❌ | ✅ |
| Serializable | ❌ | ❌ | ❌ |

- **Dirty read** = read uncommitted data.
- **Non-repeatable read** = same query gives different results in one transaction.
- **Phantom read** = new rows appear between reads.

---

## Part C — Indexes

### 🧠 Concept
An **index** is like a **book's index** — it helps the database **find rows fast** without
scanning the whole table. Speeds up `SELECT`/`WHERE`, but slows down `INSERT`/`UPDATE`.

```sql
CREATE INDEX idx_email ON users(email);          -- speeds up email lookups
CREATE UNIQUE INDEX idx_uid ON users(id);
```

```
Without index: scan all 1,000,000 rows  (slow, O(n))
With index:    B-tree jump to the row   (fast, O(log n))
```

### Types
| Index | Use |
|-------|-----|
| Primary index | On primary key (auto) |
| Unique index | Enforces uniqueness |
| Composite index | Multiple columns together |
| Clustered | Rows physically sorted by key (1 per table) |
| Non-clustered | Separate structure pointing to rows |

---

## 🌍 Real-World Use Case
- **Transactions** → bank transfers, placing an order (deduct stock + create order together).
- **Indexes** → fast search on email/username in a users table with millions of rows.

---

## ❓ Interview Questions
1. What is a transaction?
2. Explain ACID properties.
3. What is the difference between COMMIT and ROLLBACK?
4. What are isolation levels? What problems do they solve?
5. What is an index and how does it help?
6. Downside of too many indexes? (Slower writes, more storage)
7. Clustered vs non-clustered index?
8. What is a deadlock in a database?
9. What data structure do indexes usually use? (**B-tree / B+ tree**)

---

## ✅ Best Practices
- Wrap related writes in a transaction.
- Index columns used in `WHERE`, `JOIN`, `ORDER BY`.
- Don't over-index — it slows down writes.
- Choose the right isolation level for your needs.

## ⚠️ Common Mistakes
- Forgetting COMMIT (changes not saved) or ROLLBACK on error.
- Indexing every column "just in case".
- Ignoring isolation issues in concurrent systems.

---

## ⚡ Quick Revision Notes
- Transaction = all-or-nothing unit (COMMIT / ROLLBACK).
- ACID = Atomicity, Consistency, Isolation, Durability.
- Isolation levels prevent dirty/non-repeatable/phantom reads.
- Index = fast lookup (B-tree), speeds reads, slows writes.

## 🙋 FAQs
**Q: Do indexes slow anything down?** Yes — writes (INSERT/UPDATE/DELETE) become slower.

## 📎 References
- Use The Index, Luke (indexing)
- PostgreSQL / MySQL docs — Transactions

[⬅ Back to SQL Index](./README.md)

