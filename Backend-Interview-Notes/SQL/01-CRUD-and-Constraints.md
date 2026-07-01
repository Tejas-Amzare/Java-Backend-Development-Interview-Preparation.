# 1. CRUD & Constraints (Primary Key, Foreign Key)

> 🟢 **Level:** Beginner | 🔥 **Interview Frequency:** Very High

---

## 🧠 Concept

- **SQL** (Structured Query Language) = language to talk to relational databases.
- **CRUD** = the 4 basic operations: **C**reate, **R**ead, **U**pdate, **D**elete.
- **Constraints** = rules that keep data **correct and valid**.

---

## 🧩 CRUD Commands

```sql
-- CREATE (Insert)
INSERT INTO users (id, name, email) VALUES (1, 'Aman', 'aman@mail.com');

-- READ (Select)
SELECT * FROM users;
SELECT name FROM users WHERE id = 1;

-- UPDATE
UPDATE users SET name = 'Aman Kumar' WHERE id = 1;

-- DELETE
DELETE FROM users WHERE id = 1;
```

### Table Creation
```sql
CREATE TABLE users (
    id    INT PRIMARY KEY,
    name  VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE,
    age   INT CHECK (age >= 18),
    city  VARCHAR(50) DEFAULT 'Unknown'
);
```

---

## 🔒 Constraints (Data Rules)

| Constraint | Meaning |
|------------|---------|
| `PRIMARY KEY` | Unique + not null; identifies each row |
| `FOREIGN KEY` | Links to another table's primary key |
| `UNIQUE` | No duplicate values |
| `NOT NULL` | Value is required |
| `CHECK` | Value must meet a condition |
| `DEFAULT` | Auto value if none given |

---

## 🔑 Primary Key vs Foreign Key (very common!)

- **Primary Key** → uniquely identifies each row. One per table. Not null, unique.
- **Foreign Key** → a column that **points to** the primary key of another table. Creates a
  **relationship** and keeps data consistent (referential integrity).

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    user_id  INT,
    FOREIGN KEY (user_id) REFERENCES users(id)   -- links orders to users
);
```

```
users                 orders
+----+------+         +--------+---------+
| id | name |◄────────| user_id| order_id|
+----+------+  FK     +--------+---------+
```

| Primary Key | Foreign Key |
|-------------|-------------|
| Unique identifier | Reference to another table |
| One per table | Many allowed |
| Cannot be null | Can be null |
| No duplicates | Duplicates allowed |

---

## 🌍 Real-World Use Case
An e-commerce DB: `users`, `orders`, `products`. `orders.user_id` is a foreign key to `users.id`
so every order belongs to a real user.

---

## ❓ Interview Questions
1. What is CRUD?
2. Difference between primary key and foreign key?
3. Can a primary key be null? (**No**)
4. Difference between `UNIQUE` and `PRIMARY KEY`? (Table can have many unique, one PK; unique allows one null)
5. What is a composite key? (Primary key made of 2+ columns)
6. Difference between `DELETE`, `TRUNCATE`, and `DROP`?
7. What is referential integrity?

---

## 📋 DELETE vs TRUNCATE vs DROP

| | DELETE | TRUNCATE | DROP |
|-|--------|----------|------|
| Removes | Selected rows | All rows | Entire table |
| WHERE | Yes | No | No |
| Rollback | Yes | Usually no | No |
| Speed | Slow | Fast | Fast |
| Structure kept | Yes | Yes | No |

---

## ✅ Best Practices
- Always define a primary key.
- Use foreign keys to enforce relationships.
- Add `NOT NULL` and `CHECK` to prevent bad data.

## ⚠️ Common Mistakes
- Forgetting `WHERE` in UPDATE/DELETE → changes **all** rows!
- Confusing TRUNCATE (all rows) with DELETE (some rows).

---

## ⚡ Quick Revision Notes
- CRUD = INSERT, SELECT, UPDATE, DELETE.
- PK = unique + not null, one per table. FK = link to another table's PK.
- DELETE = rows (rollback), TRUNCATE = all rows (fast), DROP = whole table.
- Constraints keep data valid: NOT NULL, UNIQUE, CHECK, DEFAULT.

## 🙋 FAQs
**Q: Always include WHERE in UPDATE/DELETE?** Yes, unless you truly want to affect every row.

## 📎 References
- W3Schools SQL, Mode SQL Tutorial

[⬅ Back to SQL Index](./README.md)

