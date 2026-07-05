# 📚 SQL Complete Notes

## 🎯 What is SQL?
- **SQL** = Structured Query Language
- Used to **access** and **manipulate** data in databases
- **CRUD Operations**:
  - **C**REATE → Insert data
  - **R**EAD → Select data
  - **U**PDATE → Modify data
  - **D**ELETE → Remove data

---

## 🗄️ RDBMS vs SQL

| **RDBMS** | **SQL** |
|-----------|---------|
| Software (MySQL, Oracle, MS SQL) | Query Language |
| Stores & manages databases | Performs CRUD operations |
| Uses client-server model | Used to interact with DB |

---

## 📊 SQL Data Types (Quick Reference)

### 📝 String Types

```text
CHAR(n)      → Fixed length (0-255)
VARCHAR(n)   → Variable length (0-255) ⭐ Use this!
TEXT         → 0-65535 characters
BLOB         → Binary data (0-65535)
```

### 🔢 Numeric Types (Size Order)

```text
TINYINT < SMALLINT < MEDIUMINT < INT < BIGINT
```

### 📅 Date/Time

```text
DATE       → YYYY-MM-DD
DATETIME   → YYYY-MM-DD HH:MM:SS
TIME       → HH:MM:SS
```

---

## 📋 SQL Commands Classification

### 1. DDL (Data Definition Language) – Structure

```text
CREATE    → Create tables/databases
ALTER     → Modify table structure
DROP      → Delete tables/databases
TRUNCATE  → Remove all data (keep structure)
RENAME    → Rename tables/columns
```

### 2. DML (Data Manipulation Language) – Data

```text
INSERT    → Add data
UPDATE    → Modify data
DELETE    → Remove data
```

### 3. DRL/DQL (Data Retrieval/Query Language)

```text
SELECT    → Retrieve data
```

### 4. DCL (Data Control Language) – Permissions

```text
GRANT     → Give access
REVOKE    → Remove access
```

### 5. TCL (Transaction Control Language)

```text
START TRANSACTION  → Begin transaction
COMMIT             → Save changes
ROLLBACK           → Undo changes
SAVEPOINT          → Create checkpoint
```

---

## 🗃️ Database Management (DDL)

```sql
-- Create & Use Database
CREATE DATABASE IF NOT EXISTS mydb;
USE mydb;

-- Show all databases/tables
SHOW DATABASES;
SHOW TABLES;

-- Delete Database
DROP DATABASE IF EXISTS mydb;
```

---

## 🔍 SELECT Queries (DRL)

### Basic SELECT

```sql
SELECT column1, column2 FROM table_name;
SELECT * FROM table_name; -- All columns
```

### WHERE Clause (Filtering)

```sql
SELECT * FROM customers WHERE age > 18;

-- Operators
WHERE age BETWEEN 18 AND 60        -- Inclusive
WHERE city IN ('NYC', 'LA', 'CHI') -- Multiple values
WHERE name LIKE 'J%'               -- Starts with J
WHERE name LIKE '_ohn'             -- Second letter o
WHERE email IS NULL                -- Check NULL
```

### AND / OR / NOT

```sql
WHERE age > 18 AND city = 'NYC';
WHERE age < 18 OR age > 60;
WHERE city NOT IN ('NYC', 'LA');
```

### ORDER BY (Sorting)

```sql
SELECT * FROM customers ORDER BY name ASC; -- A-Z (default)
SELECT * FROM customers ORDER BY age DESC; -- Z-A
```

### GROUP BY (Aggregation)

```sql
SELECT country, COUNT(*) AS total
FROM customers
GROUP BY country;
```

**Aggregate Functions**

```text
COUNT() → Count rows
SUM()   → Add values
AVG()   → Average
MIN()   → Minimum
MAX()   → Maximum
```

### DISTINCT (Unique Values)

```sql
SELECT DISTINCT city FROM customers;

-- Alternative
SELECT city FROM customers
GROUP BY city;
```

### HAVING (Filter Groups)

```sql
SELECT country, COUNT(*) AS total
FROM customers
GROUP BY country
HAVING total > 50;
```

### WHERE vs HAVING

| **WHERE** | **HAVING** |
|-----------|------------|
| Before GROUP BY | After GROUP BY |
| Filters rows | Filters groups |
| GROUP BY optional | GROUP BY required |

---

## 🔗 Constraints (DDL)

### Primary Key (PK)

```sql
CREATE TABLE users (
    id INT PRIMARY KEY,
    name VARCHAR(100)
);
```

### Foreign Key (FK)

```sql
CREATE TABLE orders (
    id INT PRIMARY KEY,
    user_id INT,
    FOREIGN KEY (user_id) REFERENCES users(id)
);
```

### Other Constraints

```sql
-- UNIQUE
email VARCHAR(100) UNIQUE;

-- CHECK
age INT CHECK (age >= 18);

-- DEFAULT
status VARCHAR(20) DEFAULT 'active';
```

---

## 🛠️ ALTER TABLE Operations

```sql
-- Add Column
ALTER TABLE users ADD phone VARCHAR(15);

-- Modify Column Type
ALTER TABLE users MODIFY name CHAR(100);

-- Rename Column
ALTER TABLE users CHANGE COLUMN name full_name VARCHAR(100);

-- Drop Column
ALTER TABLE users DROP COLUMN middle_name;

-- Rename Table
ALTER TABLE users RENAME TO customers;
```

---

## ✏️ DML Operations

### INSERT

```sql
-- Single row
INSERT INTO users (name, age)
VALUES ('John', 25);

-- Multiple rows
INSERT INTO users (name, age)
VALUES
    ('John', 25),
    ('Jane', 30),
    ('Bob', 22);
```

### UPDATE

```sql
-- Single row
UPDATE users
SET age = 26
WHERE id = 1;

-- Multiple rows
UPDATE users
SET age = age + 1;

-- With CASCADE
ON UPDATE CASCADE;
```

### DELETE

```sql
-- Specific row
DELETE FROM users
WHERE id = 1;

-- All rows
DELETE FROM users;

-- Cascade
ON DELETE CASCADE;

-- Set NULL
ON DELETE SET NULL;
```

### REPLACE (Insert or Update)

```sql
REPLACE INTO users (id, name)
VALUES (1, 'John');
```

---

## 🔗 JOIN Types

### INNER JOIN

```sql
SELECT u.name, o.order_date
FROM users u
INNER JOIN orders o
ON u.id = o.user_id;
```

### LEFT JOIN

```sql
SELECT u.name, o.order_date
FROM users u
LEFT JOIN orders o
ON u.id = o.user_id;
```

### RIGHT JOIN

```sql
SELECT u.name, o.order_date
FROM users u
RIGHT JOIN orders o
ON u.id = o.user_id;
```

### FULL JOIN (MySQL Emulation)

```sql
SELECT *
FROM table1
LEFT JOIN table2 ON id

UNION

SELECT *
FROM table1
RIGHT JOIN table2 ON id;
```

### CROSS JOIN

```sql
SELECT *
FROM products
CROSS JOIN categories;

-- 10 × 5 = 50 rows
```

### SELF JOIN

```sql
SELECT
    e1.name AS employee,
    e2.name AS manager
FROM employees e1
INNER JOIN employees e2
ON e1.manager_id = e2.id;
```

### Old Join Syntax

```sql
SELECT *
FROM table1, table2
WHERE table1.id = table2.id;
```

---

## 🎯 SET Operations

| **JOIN** | **SET Operations** |
|----------|--------------------|
| Column-wise | Row-wise |
| Horizontal | Vertical |
| Different types OK | Same types required |
| Duplicates allowed | DISTINCT by default |

### UNION

```sql
SELECT name
FROM employees

UNION

SELECT name
FROM contractors;

SELECT name
FROM employees

UNION ALL

SELECT name
FROM contractors;
```

### INTERSECT (Emulated)

```sql
SELECT DISTINCT id
FROM table1
INNER JOIN table2 USING(id);
```

### MINUS (Emulated)

```sql
SELECT id
FROM table1
LEFT JOIN table2 USING(id)
WHERE table2.id IS NULL;
```

---

## 📦 Subqueries

### 1. WHERE Clause

```sql
SELECT *
FROM users
WHERE id IN (
    SELECT user_id
    FROM orders
);
```

### 2. FROM Clause (Derived Table)

```sql
SELECT MAX(age)
FROM (
    SELECT *
    FROM users
    WHERE city = 'NYC'
) AS nyc_users;
```

### 3. SELECT Clause

```sql
SELECT
    name,
    (
        SELECT COUNT(*)
        FROM orders
        WHERE user_id = users.id
    ) AS order_count
FROM users;
```

### Correlated Subquery

```sql
SELECT name
FROM users u
WHERE EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.user_id = u.id
      AND o.total > 1000
);
```

---

## 👁️ Views (Virtual Tables)

```sql
-- Create View
CREATE VIEW active_users AS
SELECT id, name, email
FROM users
WHERE status = 'active';

-- Update View
ALTER VIEW active_users AS
SELECT id, name
FROM users
WHERE status = 'active';

-- Drop View
DROP VIEW IF EXISTS active_users;
```

---

## 💡 Quick Tips

1. ✅ Use `VARCHAR` instead of `CHAR` to save space.
2. ✅ Always use `WHERE` with `UPDATE` and `DELETE`.
3. ✅ Add a `PRIMARY KEY` to every table.
4. ✅ Use indexes for frequently searched columns.
5. ✅ Backup before running `DELETE` or `UPDATE` without `WHERE`.
6. ✅ Use `EXPLAIN` to analyze query performance.
7. ✅ `GROUP BY` columns should match non-aggregated `SELECT` columns.
8. ✅ Views store queries, not data.
9. ✅ `NULL` is not equal to `0` or an empty string.
10. ✅ Use `IF EXISTS` / `IF NOT EXISTS` to avoid errors.

---

## 📝 Common Mistakes to Avoid

```sql
-- ❌ Wrong
SELECT name, age
FROM users
GROUP BY name;

-- ✅ Correct
SELECT name, COUNT(*)
FROM users
GROUP BY name;

-- ❌ Wrong
DELETE FROM users;

-- ✅ Correct
DELETE FROM users
WHERE id = 1;

-- ❌ Wrong
WHERE name = NULL;

-- ✅ Correct
WHERE name IS NULL;
```

---

## 🏁 Summary Cheat Sheet

| Operation | Command |
|-----------|---------|
| Read all | `SELECT * FROM table;` |
| Filter | `WHERE condition` |
| Sort | `ORDER BY column ASC/DESC` |
| Group | `GROUP BY column` |
| Filter groups | `HAVING condition` |
| Unique values | `DISTINCT column` |
| Join tables | `INNER/LEFT/RIGHT JOIN` |
| Insert | `INSERT INTO table VALUES (...);` |
| Update | `UPDATE table SET column=value WHERE condition;` |
| Delete | `DELETE FROM table WHERE condition;` |
| Create table | `CREATE TABLE table_name (...);` |
| Add column | `ALTER TABLE table_name ADD column TYPE;` |
| Create view | `CREATE VIEW view_name AS SELECT ...;` |
