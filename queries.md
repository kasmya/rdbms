# 📚 SQL Query Examples (Easy Cheat Sheet)

Assume we have this table:

## 👤 `students`

| id | name | age | city | marks |
|----|------|-----|------|-------|
| 1 | Alice | 20 | Delhi | 90 |
| 2 | Bob | 22 | Mumbai | 75 |
| 3 | Charlie | 19 | Delhi | 85 |
| 4 | David | 21 | Pune | 60 |
| 5 | Eva | 22 | Mumbai | 95 |

---

# 1. SELECT

### Select all columns

```sql
SELECT * FROM students;
```

### Select specific columns

```sql
SELECT name, age
FROM students;
```

---

# 2. WHERE

### Equal

```sql
SELECT *
FROM students
WHERE city = 'Delhi';
```

### Greater than

```sql
SELECT *
FROM students
WHERE marks > 80;
```

### Less than

```sql
SELECT *
FROM students
WHERE age < 21;
```

### Greater than or equal

```sql
SELECT *
FROM students
WHERE marks >= 90;
```

### Not equal

```sql
SELECT *
FROM students
WHERE city != 'Mumbai';
```

---

# 3. AND

```sql
SELECT *
FROM students
WHERE city = 'Delhi'
AND marks > 80;
```

---

# 4. OR

```sql
SELECT *
FROM students
WHERE city = 'Delhi'
OR city = 'Mumbai';
```

---

# 5. NOT

```sql
SELECT *
FROM students
WHERE NOT city = 'Delhi';
```

---

# 6. BETWEEN

```sql
SELECT *
FROM students
WHERE age BETWEEN 20 AND 22;
```

---

# 7. IN

```sql
SELECT *
FROM students
WHERE city IN ('Delhi', 'Mumbai');
```

---

# 8. NOT IN

```sql
SELECT *
FROM students
WHERE city NOT IN ('Delhi', 'Mumbai');
```

---

# 9. LIKE

### Starts with A

```sql
SELECT *
FROM students
WHERE name LIKE 'A%';
```

### Ends with e

```sql
SELECT *
FROM students
WHERE name LIKE '%e';
```

### Contains a

```sql
SELECT *
FROM students
WHERE name LIKE '%a%';
```

### Second letter = o

```sql
SELECT *
FROM students
WHERE name LIKE '_o%';
```

---

# 10. IS NULL

```sql
SELECT *
FROM students
WHERE marks IS NULL;
```

---

# 11. IS NOT NULL

```sql
SELECT *
FROM students
WHERE marks IS NOT NULL;
```

---

# 12. ORDER BY

### Ascending

```sql
SELECT *
FROM students
ORDER BY marks ASC;
```

### Descending

```sql
SELECT *
FROM students
ORDER BY marks DESC;
```

---

# 13. LIMIT

```sql
SELECT *
FROM students
LIMIT 3;
```

---

# 14. DISTINCT

```sql
SELECT DISTINCT city
FROM students;
```

---

# 15. COUNT()

```sql
SELECT COUNT(*)
FROM students;
```

---

# 16. SUM()

```sql
SELECT SUM(marks)
FROM students;
```

---

# 17. AVG()

```sql
SELECT AVG(marks)
FROM students;
```

---

# 18. MIN()

```sql
SELECT MIN(marks)
FROM students;
```

---

# 19. MAX()

```sql
SELECT MAX(marks)
FROM students;
```

---

# 20. GROUP BY

```sql
SELECT city, COUNT(*)
FROM students
GROUP BY city;
```

---

# 21. HAVING

```sql
SELECT city, AVG(marks)
FROM students
GROUP BY city
HAVING AVG(marks) > 80;
```

---

# 22. INSERT

```sql
INSERT INTO students(name, age, city, marks)
VALUES ('John', 20, 'Delhi', 88);
```

---

# 23. INSERT Multiple Rows

```sql
INSERT INTO students(name, age, city, marks)
VALUES
('Tom',20,'Delhi',80),
('Sam',21,'Pune',90),
('Amy',19,'Mumbai',95);
```

---

# 24. UPDATE

```sql
UPDATE students
SET marks = 100
WHERE id = 1;
```

---

# 25. UPDATE Multiple Columns

```sql
UPDATE students
SET city = 'Noida',
    marks = 95
WHERE id = 2;
```

---

# 26. DELETE

```sql
DELETE FROM students
WHERE id = 3;
```

---

# 27. DELETE All Rows

```sql
DELETE FROM students;
```

---

# 28. CREATE DATABASE

```sql
CREATE DATABASE school;
```

---

# 29. USE DATABASE

```sql
USE school;
```

---

# 30. CREATE TABLE

```sql
CREATE TABLE students (
    id INT PRIMARY KEY,
    name VARCHAR(50),
    age INT,
    city VARCHAR(50),
    marks INT
);
```

---

# 31. ALTER TABLE (Add Column)

```sql
ALTER TABLE students
ADD email VARCHAR(100);
```

---

# 32. ALTER TABLE (Modify Column)

```sql
ALTER TABLE students
MODIFY name VARCHAR(100);
```

---

# 33. ALTER TABLE (Drop Column)

```sql
ALTER TABLE students
DROP COLUMN email;
```

---

# 34. DROP TABLE

```sql
DROP TABLE students;
```

---

# 35. TRUNCATE TABLE

```sql
TRUNCATE TABLE students;
```

---

# 36. INNER JOIN

Tables:

### students

| id | name |
|----|------|
|1|Alice|
|2|Bob|

### marks

| student_id | score |
|------------|-------|
|1|90|
|2|80|

```sql
SELECT students.name, marks.score
FROM students
INNER JOIN marks
ON students.id = marks.student_id;
```

---

# 37. LEFT JOIN

```sql
SELECT students.name, marks.score
FROM students
LEFT JOIN marks
ON students.id = marks.student_id;
```

---

# 38. RIGHT JOIN

```sql
SELECT students.name, marks.score
FROM students
RIGHT JOIN marks
ON students.id = marks.student_id;
```

---

# 39. CROSS JOIN

```sql
SELECT *
FROM students
CROSS JOIN marks;
```

---

# 40. UNION

```sql
SELECT city
FROM students

UNION

SELECT city
FROM teachers;
```

---

# 41. UNION ALL

```sql
SELECT city
FROM students

UNION ALL

SELECT city
FROM teachers;
```

---

# 42. Subquery

```sql
SELECT *
FROM students
WHERE marks > (
    SELECT AVG(marks)
    FROM students
);
```

---

# 43. EXISTS

```sql
SELECT *
FROM students s
WHERE EXISTS (
    SELECT *
    FROM marks m
    WHERE s.id = m.student_id
);
```

---

# 44. CREATE VIEW

```sql
CREATE VIEW toppers AS
SELECT *
FROM students
WHERE marks > 90;
```

---

# 45. DROP VIEW

```sql
DROP VIEW toppers;
```

---

# 46. CASE

```sql
SELECT
name,
marks,
CASE
    WHEN marks >= 90 THEN 'Excellent'
    WHEN marks >= 75 THEN 'Good'
    ELSE 'Average'
END AS Grade
FROM students;
```

---

# 47. Aliases (AS)

```sql
SELECT
name AS Student_Name,
marks AS Score
FROM students;
```

---

# 48. SQL Execution Order (Very Important)

```text
FROM
↓
WHERE
↓
GROUP BY
↓
HAVING
↓
SELECT
↓
DISTINCT
↓
ORDER BY
↓
LIMIT
```

---

# 🎯 Most Frequently Asked SQL Queries in Interviews

```sql
SELECT * FROM students;

SELECT DISTINCT city FROM students;

SELECT * FROM students WHERE marks > 80;

SELECT * FROM students ORDER BY marks DESC;

SELECT city, COUNT(*)
FROM students
GROUP BY city;

SELECT city, AVG(marks)
FROM students
GROUP BY city
HAVING AVG(marks) > 80;

SELECT * FROM students
WHERE marks > (
    SELECT AVG(marks)
    FROM students
);

SELECT students.name, marks.score
FROM students
INNER JOIN marks
ON students.id = marks.student_id;

UPDATE students
SET marks = 95
WHERE id = 1;

DELETE FROM students
WHERE id = 1;
```
