# SQL Notes – Definitions, Syntax & Examples

# 1. What is SQL?

## Definition

**SQL (Structured Query Language)** is a language used to communicate with and work with relational databases.

SQL can be used to:

- Retrieve data
- Insert new data
- Update existing data
- Delete data
- Create tables and databases
- Modify database structures
- Combine data from multiple tables

---

# 2. Database

## Definition

A **database** is an organized collection of data that can be stored, managed, and retrieved efficiently.

A relational database stores data in **tables**.

### Example

A `students` table might contain:

| id | name | age | course |
|---|---|---:|---|
| 1 | Rahul | 21 | Python |
| 2 | Priya | 22 | SQL |
| 3 | Aman | 20 | Python |

---

# 3. DBMS

## Definition

A **DBMS (Database Management System)** is software used to create, store, manage, and access databases.

Examples:

- MySQL
- PostgreSQL
- Microsoft SQL Server
- Oracle Database
- SQLite

The SQL language is used to interact with many relational database systems.

---

# 4. Table, Row and Column

## Table

A **table** stores related data in rows and columns.

## Row

A **row** represents one record.

## Column

A **column** represents one attribute or property of the data.

For example:

```text
students
--------------------------------
id | name  | age | course
--------------------------------
1  | Rahul | 21  | Python
2  | Priya | 22  | SQL
```

Here:

- `students` → table
- `1, Rahul, 21, Python` → row
- `name`, `age`, `course` → columns

---

# 5. SQL Comments

Comments are used to explain SQL code. They are ignored when the query is executed.

## Single-line comment

```sql
-- This is a comment
SELECT * FROM students;
```

## Multi-line comment

```sql
/*
This is a
multi-line comment
*/
SELECT * FROM students;
```

---

# 6. SELECT

## Definition

`SELECT` is used to retrieve data from a table.

## Syntax

```sql
SELECT column1, column2
FROM table_name;
```

## Example

```sql
SELECT name, age
FROM students;
```

To select all columns:

```sql
SELECT *
FROM students;
```

---

# 7. DISTINCT

## Definition

`DISTINCT` removes duplicate values from the result.

## Syntax

```sql
SELECT DISTINCT column_name
FROM table_name;
```

## Example

```sql
SELECT DISTINCT course
FROM students;
```

If several students have the same course, each course appears only once.

---

# 8. WHERE

## Definition

`WHERE` filters rows based on a condition.

## Syntax

```sql
SELECT columns
FROM table_name
WHERE condition;
```

## Example

```sql
SELECT *
FROM students
WHERE age > 20;
```

This returns students whose age is greater than 20.

---

# 9. Comparison Operators

Comparison operators are used to compare values.

| Operator | Meaning |
|---|---|
| `=` | Equal to |
| `<>` | Not equal to |
| `!=` | Not equal to |
| `>` | Greater than |
| `<` | Less than |
| `>=` | Greater than or equal to |
| `<=` | Less than or equal to |

## Example

```sql
SELECT *
FROM students
WHERE age >= 21;
```

---

# 10. Logical Operators

Logical operators combine or modify conditions.

## AND

Both conditions must be true.

```sql
SELECT *
FROM students
WHERE age > 20 AND course = 'Python';
```

## OR

At least one condition must be true.

```sql
SELECT *
FROM students
WHERE course = 'Python' OR course = 'SQL';
```

## NOT

Reverses a condition.

```sql
SELECT *
FROM students
WHERE NOT course = 'Python';
```

---

# 11. IN

## Definition

`IN` checks whether a value exists in a list of values.

## Syntax

```sql
WHERE column_name IN (value1, value2, value3);
```

## Example

```sql
SELECT *
FROM students
WHERE course IN ('Python', 'SQL');
```

This is often cleaner than:

```sql
WHERE course = 'Python' OR course = 'SQL';
```

---

# 12. BETWEEN

## Definition

`BETWEEN` checks whether a value falls within a specified range.

## Syntax

```sql
WHERE column_name BETWEEN value1 AND value2;
```

## Example

```sql
SELECT *
FROM students
WHERE age BETWEEN 20 AND 22;
```

`BETWEEN` is inclusive of the boundary values in common SQL implementations.

---

# 13. LIKE

## Definition

`LIKE` is used for pattern matching.

Two common wildcards are:

- `%` → zero or more characters
- `_` → exactly one character

## Examples

Names starting with `A`:

```sql
SELECT *
FROM students
WHERE name LIKE 'A%';
```

Names ending with `a`:

```sql
SELECT *
FROM students
WHERE name LIKE '%a';
```

Names containing `an`:

```sql
SELECT *
FROM students
WHERE name LIKE '%an%';
```

---

# 14. ORDER BY

## Definition

`ORDER BY` sorts the result.

## Syntax

```sql
SELECT columns
FROM table_name
ORDER BY column_name;
```

Ascending order:

```sql
SELECT *
FROM students
ORDER BY age ASC;
```

Descending order:

```sql
SELECT *
FROM students
ORDER BY age DESC;
```

`ASC` is the default in many SQL systems.

---

# 15. LIMIT

## Definition

`LIMIT` restricts the number of rows returned in SQL systems that support this syntax, such as MySQL and PostgreSQL.

## Example

```sql
SELECT *
FROM students
LIMIT 5;
```

This returns up to 5 rows.

> Note: SQL syntax for limiting rows varies between database systems. For example, SQL Server commonly uses `TOP` or `OFFSET ... FETCH`.

---

# 16. NULL

## Definition

`NULL` represents a missing, unknown, or unavailable value.

`NULL` is not the same as:

- `0`
- An empty string
- `FALSE`

## Checking for NULL

Use `IS NULL`:

```sql
SELECT *
FROM students
WHERE age IS NULL;
```

Use `IS NOT NULL`:

```sql
SELECT *
FROM students
WHERE age IS NOT NULL;
```

Do not normally use:

```sql
WHERE age = NULL;
```

---

# 17. Aggregate Functions

Aggregate functions perform calculations on multiple rows and return a result.

Common aggregate functions:

- `COUNT()`
- `SUM()`
- `AVG()`
- `MIN()`
- `MAX()`

## COUNT

Counts rows or non-NULL values depending on the expression.

```sql
SELECT COUNT(*)
FROM students;
```

## SUM

Adds numeric values.

```sql
SELECT SUM(salary)
FROM employees;
```

## AVG

Calculates the average.

```sql
SELECT AVG(salary)
FROM employees;
```

## MIN

Finds the minimum value.

```sql
SELECT MIN(salary)
FROM employees;
```

## MAX

Finds the maximum value.

```sql
SELECT MAX(salary)
FROM employees;
```

---

# 18. GROUP BY

## Definition

`GROUP BY` groups rows that have the same values so aggregate functions can be applied to each group.

## Syntax

```sql
SELECT column_name, aggregate_function(column_name)
FROM table_name
GROUP BY column_name;
```

## Example

```sql
SELECT course, COUNT(*)
FROM students
GROUP BY course;
```

This counts how many students belong to each course.

---

# 19. HAVING

## Definition

`HAVING` filters groups after `GROUP BY`.

## Example

```sql
SELECT course, COUNT(*) AS total_students
FROM students
GROUP BY course
HAVING COUNT(*) > 2;
```

This returns courses having more than 2 students.

### WHERE vs HAVING

- `WHERE` filters individual rows before grouping.
- `HAVING` filters groups after grouping.

---

# 20. AS (Alias)

## Definition

An alias gives a temporary name to a column or table in a query.

## Column alias

```sql
SELECT name AS student_name
FROM students;
```

## Table alias

```sql
SELECT s.name
FROM students AS s;
```

`AS` can often be omitted:

```sql
SELECT s.name
FROM students s;
```

---

# 21. CASE

## Definition

`CASE` allows conditional logic inside a SQL query.

## Syntax

```sql
CASE
    WHEN condition THEN result
    WHEN condition THEN result
    ELSE result
END
```

## Example

```sql
SELECT
    name,
    age,
    CASE
        WHEN age >= 18 THEN 'Adult'
        ELSE 'Minor'
    END AS age_group
FROM students;
```

---

# 22. String Functions

String functions work with text.

Common functions include:

- `UPPER()`
- `LOWER()`
- `LENGTH()`
- `CONCAT()`
- `TRIM()`

## UPPER

```sql
SELECT UPPER(name)
FROM students;
```

## LOWER

```sql
SELECT LOWER(name)
FROM students;
```

## LENGTH

```sql
SELECT LENGTH(name)
FROM students;
```

## CONCAT

```sql
SELECT CONCAT(first_name, ' ', last_name) AS full_name
FROM employees;
```

> String-function names and exact behavior can vary between database systems.

---

# 23. COALESCE

## Definition

`COALESCE()` returns the first non-NULL value from the supplied expressions.

## Example

```sql
SELECT COALESCE(phone, 'Not Available') AS phone_number
FROM students;
```

If `phone` is `NULL`, the query returns `'Not Available'`.

---

# 24. Date Functions

SQL databases provide functions for working with dates and times.

Common examples include functions such as:

```sql
CURRENT_DATE
```

and, depending on the database:

```sql
CURRENT_TIMESTAMP
```

Example:

```sql
SELECT CURRENT_DATE;
```

Date functions differ between database systems, so check the documentation for the specific database you are using.

---

# 25. Primary Key

## Definition

A **primary key** uniquely identifies each row in a table.

Important properties:

- Values must be unique.
- A primary key cannot contain `NULL`.
- A table normally has one primary key constraint, which can contain one or multiple columns.

## Example

```sql
CREATE TABLE students (
    student_id INT PRIMARY KEY,
    name VARCHAR(100),
    age INT
);
```

Here, `student_id` uniquely identifies each student.

---

# 26. Foreign Key

## Definition

A **foreign key** creates a relationship between tables by referring to a key in another table.

## Example

```sql
CREATE TABLE departments (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(100)
);

CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100),
    department_id INT,
    FOREIGN KEY (department_id)
        REFERENCES departments(department_id)
);
```

Here, `department_id` in `employees` refers to `department_id` in `departments`.

---

# 27. Constraints

## Definition

Constraints are rules applied to table columns to control the data that can be stored.

Common constraints:

- `PRIMARY KEY`
- `FOREIGN KEY`
- `NOT NULL`
- `UNIQUE`
- `CHECK`
- `DEFAULT`

## Example

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(150) UNIQUE,
    age INT CHECK (age >= 18),
    country VARCHAR(50) DEFAULT 'India'
);
```

---

# 28. INNER JOIN

## Definition

`INNER JOIN` returns rows where there is a matching value in both tables.

## Syntax

```sql
SELECT columns
FROM table1
INNER JOIN table2
    ON table1.column = table2.column;
```

## Example

```sql
SELECT e.name, d.department_name
FROM employees e
INNER JOIN departments d
    ON e.department_id = d.department_id;
```

Only employees with a matching department are returned.

---

# 29. LEFT JOIN

## Definition

`LEFT JOIN` returns all rows from the left table and matching rows from the right table.

If there is no match, columns from the right table contain `NULL`.

## Example

```sql
SELECT e.name, d.department_name
FROM employees e
LEFT JOIN departments d
    ON e.department_id = d.department_id;
```

---

# 30. RIGHT JOIN

## Definition

`RIGHT JOIN` returns all rows from the right table and matching rows from the left table.

```sql
SELECT e.name, d.department_name
FROM employees e
RIGHT JOIN departments d
    ON e.department_id = d.department_id;
```

Support and usage can vary by database system.

---

# 31. FULL OUTER JOIN

## Definition

`FULL OUTER JOIN` returns matching rows plus unmatched rows from both tables.

Conceptually:

```sql
SELECT *
FROM table1
FULL OUTER JOIN table2
    ON table1.id = table2.id;
```

Not every database system supports `FULL OUTER JOIN` directly.

---

# 32. CROSS JOIN

## Definition

`CROSS JOIN` returns every possible combination of rows from two tables.

If table A has 3 rows and table B has 4 rows, the result contains 12 combinations.

## Example

```sql
SELECT *
FROM colors
CROSS JOIN sizes;
```

---

# 33. SELF JOIN

## Definition

A self join joins a table with itself.

It is useful when rows in the same table are related to each other.

## Example

Suppose an employee table contains a `manager_id`:

```sql
SELECT
    e.name AS employee,
    m.name AS manager
FROM employees e
LEFT JOIN employees m
    ON e.manager_id = m.employee_id;
```

Here the `employees` table is used twice with different aliases.

---

# 34. UNION

## Definition

`UNION` combines the results of two compatible `SELECT` queries and removes duplicate rows.

## Example

```sql
SELECT name FROM students
UNION
SELECT name FROM teachers;
```

The queries generally need the same number of columns with compatible data types.

---

# 35. UNION ALL

## Definition

`UNION ALL` combines results and keeps duplicates.

```sql
SELECT name FROM students
UNION ALL
SELECT name FROM teachers;
```

### UNION vs UNION ALL

- `UNION` → removes duplicates.
- `UNION ALL` → keeps duplicates and can be faster because duplicate removal is not required.

---

# 36. Subquery

## Definition

A **subquery** is a query written inside another SQL query.

## Example

Find employees whose salary is greater than the average salary:

```sql
SELECT name, salary
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

The inner query calculates the average salary. The outer query uses that result.

---

# 37. Common Table Expression (CTE)

## Definition

A **CTE (Common Table Expression)** creates a temporary named result set that can be referenced by the main query.

It begins with `WITH`.

## Syntax

```sql
WITH cte_name AS (
    SELECT ...
)
SELECT *
FROM cte_name;
```

## Example

```sql
WITH high_salary AS (
    SELECT *
    FROM employees
    WHERE salary > 50000
)
SELECT name, salary
FROM high_salary;
```

CTEs can make complex queries easier to read.

---

# 38. Window Functions

## Definition

Window functions perform calculations across related rows without combining those rows into one result row like `GROUP BY` does.

Common window functions:

- `ROW_NUMBER()`
- `RANK()`
- `DENSE_RANK()`
- `LAG()`
- `LEAD()`
- `SUM() OVER()`
- `AVG() OVER()`

## ROW_NUMBER

```sql
SELECT
    name,
    salary,
    ROW_NUMBER() OVER (ORDER BY salary DESC) AS row_num
FROM employees;
```

## RANK

```sql
SELECT
    name,
    salary,
    RANK() OVER (ORDER BY salary DESC) AS salary_rank
FROM employees;
```

### Important difference

`GROUP BY` reduces multiple rows into groups.

A window function normally keeps the original rows and adds a calculated value.

---

# 39. INSERT

## Definition

`INSERT` adds new rows to a table.

## Syntax

```sql
INSERT INTO table_name (column1, column2)
VALUES (value1, value2);
```

## Example

```sql
INSERT INTO students (id, name, age)
VALUES (1, 'Rahul', 21);
```

---

# 40. UPDATE

## Definition

`UPDATE` modifies existing rows.

## Syntax

```sql
UPDATE table_name
SET column_name = value
WHERE condition;
```

## Example

```sql
UPDATE students
SET age = 22
WHERE id = 1;
```

### Important

Be careful with `UPDATE` without a `WHERE` clause:

```sql
UPDATE students
SET age = 22;
```

This can update every row.

---

# 41. DELETE

## Definition

`DELETE` removes rows from a table.

## Syntax

```sql
DELETE FROM table_name
WHERE condition;
```

## Example

```sql
DELETE FROM students
WHERE id = 1;
```

Without a `WHERE` clause:

```sql
DELETE FROM students;
```

all rows are deleted, although the table itself remains.

---

# 42. CREATE TABLE

## Definition

`CREATE TABLE` creates a new table.

## Syntax

```sql
CREATE TABLE table_name (
    column1 data_type,
    column2 data_type
);
```

## Example

```sql
CREATE TABLE students (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    age INT
);
```

---

# 43. ALTER TABLE

## Definition

`ALTER TABLE` changes the structure of an existing table.

For example, adding a column:

```sql
ALTER TABLE students
ADD email VARCHAR(150);
```

Exact `ALTER TABLE` syntax varies by database system.

---

# 44. DROP TABLE

## Definition

`DROP TABLE` permanently removes a table and its data.

```sql
DROP TABLE students;
```

Use it carefully.

---

# 45. DELETE vs DROP vs TRUNCATE

| Command | Purpose |
|---|---|
| `DELETE` | Removes rows |
| `TRUNCATE` | Removes all rows while keeping the table structure |
| `DROP` | Removes the table itself |

Example:

```sql
DELETE FROM students
WHERE id = 1;
```

```sql
TRUNCATE TABLE students;
```

```sql
DROP TABLE students;
```

Exact behavior of `TRUNCATE`, including transaction and identity behavior, can vary between database systems.

---

# 46. SQL Query Execution Order

A useful conceptual order for understanding many `SELECT` queries is:

```text
FROM
JOIN
WHERE
GROUP BY
HAVING
SELECT
DISTINCT
ORDER BY
LIMIT
```

For example:

```sql
SELECT department_id, AVG(salary) AS avg_salary
FROM employees
WHERE salary > 30000
GROUP BY department_id
HAVING AVG(salary) > 50000
ORDER BY avg_salary DESC
LIMIT 5;
```

Understanding this order helps when writing complex queries.

---

# 47. WHERE vs HAVING

### WHERE

Filters rows before grouping.

```sql
SELECT *
FROM employees
WHERE salary > 30000;
```

### HAVING

Filters groups after aggregation.

```sql
SELECT department_id, AVG(salary)
FROM employees
GROUP BY department_id
HAVING AVG(salary) > 50000;
```

---

# 48. WHERE vs ON

The `ON` clause defines how rows are matched during a join.

Example:

```sql
SELECT e.name, d.department_name
FROM employees e
JOIN departments d
    ON e.department_id = d.department_id;
```

`WHERE` then filters the resulting rows:

```sql
SELECT e.name, d.department_name
FROM employees e
JOIN departments d
    ON e.department_id = d.department_id
WHERE e.salary > 50000;
```

---

# 49. Primary Key vs Foreign Key

| Primary Key | Foreign Key |
|---|---|
| Uniquely identifies rows | Creates a relationship with another table |
| Cannot be `NULL` | Can be `NULL` unless restricted |
| Unique within its key constraint | Can contain repeated values |
| Defines the main identifier | References a key in another table |

---

# 50. Common SQL Practice Problems

## Find the highest salary

```sql
SELECT MAX(salary)
FROM employees;
```

## Find the lowest salary

```sql
SELECT MIN(salary)
FROM employees;
```

## Find the average salary

```sql
SELECT AVG(salary)
FROM employees;
```

## Count employees

```sql
SELECT COUNT(*)
FROM employees;
```

## Find employees with salary above 50000

```sql
SELECT *
FROM employees
WHERE salary > 50000;
```

## Find the second-highest salary

One common approach:

```sql
SELECT MAX(salary) AS second_highest
FROM employees
WHERE salary < (
    SELECT MAX(salary)
    FROM employees
);
```

This approach finds the second distinct salary.

## Find duplicate values

```sql
SELECT email, COUNT(*) AS count
FROM employees
GROUP BY email
HAVING COUNT(*) > 1;
```

## Find departments with more than 5 employees

```sql
SELECT department_id, COUNT(*) AS employee_count
FROM employees
GROUP BY department_id
HAVING COUNT(*) > 5;
```

---

# 51. Quick SQL Syntax Reference

## Select

```sql
SELECT column1, column2
FROM table_name;
```

## Filter

```sql
SELECT *
FROM table_name
WHERE condition;
```

## Sort

```sql
SELECT *
FROM table_name
ORDER BY column_name DESC;
```

## Group

```sql
SELECT column_name, COUNT(*)
FROM table_name
GROUP BY column_name;
```

## Filter groups

```sql
SELECT column_name, COUNT(*)
FROM table_name
GROUP BY column_name
HAVING COUNT(*) > 1;
```

## Join

```sql
SELECT *
FROM table1
JOIN table2
    ON table1.id = table2.id;
```

## Insert

```sql
INSERT INTO table_name (column1, column2)
VALUES (value1, value2);
```

## Update

```sql
UPDATE table_name
SET column1 = value1
WHERE condition;
```

## Delete

```sql
DELETE FROM table_name
WHERE condition;
```

## Create table

```sql
CREATE TABLE table_name (
    id INT PRIMARY KEY,
    name VARCHAR(100)
);
```

## CTE

```sql
WITH cte_name AS (
    SELECT ...
)
SELECT *
FROM cte_name;
```

## Window function

```sql
SELECT
    column_name,
    ROW_NUMBER() OVER (ORDER BY column_name) AS row_num
FROM table_name;
```

---

# 52. Important SQL Concepts to Remember

- SQL is used to work with relational databases.
- `SELECT` retrieves data.
- `WHERE` filters rows.
- `GROUP BY` creates groups for aggregation.
- `HAVING` filters groups.
- `ORDER BY` sorts results.
- `JOIN` combines related data from tables.
- A primary key identifies a row uniquely.
- A foreign key creates a relationship between tables.
- `NULL` represents missing or unknown data.
- Aggregate functions calculate values across multiple rows.
- Subqueries place one query inside another.
- CTEs make complex queries easier to organize.
- Window functions calculate across related rows while retaining individual rows.
- SQL syntax can differ between database systems, so database-specific documentation matters.

