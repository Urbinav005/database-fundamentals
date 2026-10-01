# 🧾 SQL — Structured Query Language

SQL (Structured Query Language) is the standard language used to communicate with relational databases.

It allows us to create databases and tables, insert information, query data, modify records, and delete information.

---

## 📌 What is SQL?

SQL is used to interact with relational database management systems such as:

- PostgreSQL
- Oracle Database
- MySQL
- Microsoft SQL Server

SQL is mainly used for working with structured data stored in tables.

---

# 🏗️ SQL Categories

SQL commands can be grouped into different categories.

| Category | Meaning | Examples |
|---|---|---|
| DDL | Data Definition Language | CREATE, ALTER, DROP |
| DML | Data Manipulation Language | INSERT, UPDATE, DELETE |
| DQL | Data Query Language | SELECT |
| DCL | Data Control Language | GRANT, REVOKE |
| TCL | Transaction Control Language | COMMIT, ROLLBACK |

---

# 🏗️ DDL — Data Definition Language

DDL commands define and modify the structure of database objects.

Main commands:

- CREATE
- ALTER
- DROP
- TRUNCATE

---

## CREATE

Creates a database object such as a table.

### Create a table

~~~sql
CREATE TABLE students (
    student_id INT PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(150),
    age INT
);
~~~

---

## ALTER

Modifies the structure of an existing table.

### Add a column

~~~sql
ALTER TABLE students
ADD phone VARCHAR(20);
~~~

---

## DROP

Deletes a database object.

~~~sql
DROP TABLE students;
~~~

⚠️ `DROP` removes the table and its structure.

---

## TRUNCATE

Removes all records from a table while keeping the table structure.

~~~sql
TRUNCATE TABLE students;
~~~

---

# ✏️ DML — Data Manipulation Language

DML commands manipulate the data stored inside tables.

Main commands:

- INSERT
- UPDATE
- DELETE

---

## INSERT

Adds new records to a table.

~~~sql
INSERT INTO students (student_id, name, email, age)
VALUES (1, 'Rodolfo', 'rodolfo@email.com', 21);
~~~

Multiple records can also be inserted:

~~~sql
INSERT INTO students (student_id, name, email, age)
VALUES
(2, 'Carlos', 'carlos@email.com', 20),
(3, 'Ana', 'ana@email.com', 22);
~~~

---

## UPDATE

Modifies existing records.

~~~sql
UPDATE students
SET age = 22
WHERE student_id = 1;
~~~

⚠️ Always be careful with `UPDATE` without a `WHERE` condition.

---

## DELETE

Deletes records from a table.

~~~sql
DELETE FROM students
WHERE student_id = 3;
~~~

⚠️ A `DELETE` without `WHERE` can remove every record from the table.

---

# 🔎 DQL — Data Query Language

The main DQL command is:

~~~text
SELECT
~~~

It is used to retrieve information from tables.

---

## SELECT

Retrieve all columns:

~~~sql
SELECT *
FROM students;
~~~

Retrieve specific columns:

~~~sql
SELECT name, email
FROM students;
~~~

---

# 🎯 WHERE

`WHERE` filters records according to a condition.

~~~sql
SELECT *
FROM students
WHERE age >= 21;
~~~

Another example:

~~~sql
SELECT *
FROM students
WHERE name = 'Rodolfo';
~~~

---

# 🔢 Comparison Operators

Common comparison operators include:

| Operator | Meaning |
|---|---|
| = | Equal |
| <> | Not equal |
| > | Greater than |
| < | Less than |
| >= | Greater than or equal |
| <= | Less than or equal |

Example:

~~~sql
SELECT *
FROM students
WHERE age > 20;
~~~

---

# 🔗 Logical Operators

SQL also provides logical operators.

## AND

Both conditions must be true.

~~~sql
SELECT *
FROM students
WHERE age >= 18 AND age <= 25;
~~~

## OR

At least one condition must be true.

~~~sql
SELECT *
FROM students
WHERE age = 20 OR age = 21;
~~~

## NOT

Negates a condition.

~~~sql
SELECT *
FROM students
WHERE NOT age = 20;
~~~

---

# 🔤 LIKE

`LIKE` searches for patterns in text.

### Starts with R

~~~sql
SELECT *
FROM students
WHERE name LIKE 'R%';
~~~

### Ends with o

~~~sql
SELECT *
FROM students
WHERE name LIKE '%o';
~~~

### Contains "ol"

~~~sql
SELECT *
FROM students
WHERE name LIKE '%ol%';
~~~

`%` represents any sequence of characters.

---

# 📊 ORDER BY

Sorts query results.

### Ascending

~~~sql
SELECT *
FROM students
ORDER BY age ASC;
~~~

### Descending

~~~sql
SELECT *
FROM students
ORDER BY age DESC;
~~~

---

# 🔢 LIMIT

Limits the number of returned records.

~~~sql
SELECT *
FROM students
LIMIT 5;
~~~

---

# 📈 Aggregate Functions

Aggregate functions perform calculations over multiple records.

Common functions include:

- COUNT()
- SUM()
- AVG()
- MIN()
- MAX()

---

## COUNT

Counts records.

~~~sql
SELECT COUNT(*)
FROM students;
~~~

---

## SUM

Calculates a total.

~~~sql
SELECT SUM(age)
FROM students;
~~~

---

## AVG

Calculates an average.

~~~sql
SELECT AVG(age)
FROM students;
~~~

---

## MIN

Returns the smallest value.

~~~sql
SELECT MIN(age)
FROM students;
~~~

---

## MAX

Returns the largest value.

~~~sql
SELECT MAX(age)
FROM students;
~~~

---

# 📦 GROUP BY

Groups records according to a column.

Example:

~~~sql
SELECT career_id, COUNT(*)
FROM students
GROUP BY career_id;
~~~

This can be used to count how many students belong to each career.

---

# 🎯 HAVING

`HAVING` filters grouped results.

~~~sql
SELECT career_id, COUNT(*)
FROM students
GROUP BY career_id
HAVING COUNT(*) > 5;
~~~

Difference:

~~~text
WHERE  → filters individual rows
HAVING → filters groups
~~~

---

# 🔗 SQL JOINs

JOINs combine information from multiple tables.

The most common JOINs are:

- INNER JOIN
- LEFT JOIN
- RIGHT JOIN
- FULL OUTER JOIN

---

## INNER JOIN

Returns records that have matching values in both tables.

~~~sql
SELECT students.name, careers.name
FROM students
INNER JOIN careers
ON students.career_id = careers.career_id;
~~~

---

## LEFT JOIN

Returns all records from the left table and matching records from the right table.

~~~sql
SELECT students.name, careers.name
FROM students
LEFT JOIN careers
ON students.career_id = careers.career_id;
~~~

---

## RIGHT JOIN

Returns all records from the right table and matching records from the left table.

~~~sql
SELECT students.name, careers.name
FROM students
RIGHT JOIN careers
ON students.career_id = careers.career_id;
~~~

---

## FULL OUTER JOIN

Returns matching and non-matching records from both tables.

~~~sql
SELECT students.name, careers.name
FROM students
FULL OUTER JOIN careers
ON students.career_id = careers.career_id;
~~~

---

# 🧩 Aliases

Aliases give temporary names to tables or columns.

### Column alias

~~~sql
SELECT name AS student_name
FROM students;
~~~

### Table alias

~~~sql
SELECT s.name
FROM students AS s;
~~~

Aliases make complex queries easier to read.

---

# 🪆 Subqueries

A subquery is a query inside another query.

Example:

~~~sql
SELECT name
FROM students
WHERE age > (
    SELECT AVG(age)
    FROM students
);
~~~

This returns students whose age is above the average.

---

# 👁️ Views

A view is a virtual table based on a query.

Example:

~~~sql
CREATE VIEW adult_students AS
SELECT student_id, name, age
FROM students
WHERE age >= 18;
~~~

Then:

~~~sql
SELECT *
FROM adult_students;
~~~

Views can simplify complex queries and control which information users can access.

---

# 🔐 Transactions

A transaction is a sequence of database operations treated as a logical unit.

Important commands include:

- BEGIN
- COMMIT
- ROLLBACK

Example:

~~~sql
BEGIN;

UPDATE students
SET age = 22
WHERE student_id = 1;

COMMIT;
~~~

If something goes wrong:

~~~sql
ROLLBACK;
~~~

---

# 🔐 TCL — Transaction Control Language

## COMMIT

Permanently saves the changes made during a transaction.

~~~sql
COMMIT;
~~~

## ROLLBACK

Undoes changes that have not been committed.

~~~sql
ROLLBACK;
~~~

---

# 🔑 DCL — Data Control Language

DCL controls permissions and access to database objects.

Common commands include:

- GRANT
- REVOKE

Example:

~~~sql
GRANT SELECT ON students TO user1;
~~~

---

# 🧠 NULL

`NULL` represents an unknown, missing, or undefined value.

It is important to remember:

~~~text
NULL ≠ 0
NULL ≠ ''
~~~

To search for NULL values:

~~~sql
SELECT *
FROM students
WHERE email IS NULL;
~~~

To search for values that are not NULL:

~~~sql
SELECT *
FROM students
WHERE email IS NOT NULL;
~~~

---

# 🧹 DISTINCT

Removes duplicate values from query results.

~~~sql
SELECT DISTINCT career_id
FROM students;
~~~

---

# 🧮 Complete SQL Example

A complete example combining several concepts:

~~~sql
SELECT
    c.name AS career,
    COUNT(s.student_id) AS total_students,
    AVG(s.age) AS average_age
FROM students AS s
INNER JOIN careers AS c
    ON s.career_id = c.career_id
WHERE s.age >= 18
GROUP BY c.name
HAVING COUNT(s.student_id) > 1
ORDER BY total_students DESC;
~~~

This query:

1. Joins students with careers.
2. Filters students by age.
3. Groups students by career.
4. Counts students.
5. Calculates the average age.
6. Filters groups.
7. Sorts the results.

---

# 📚 SQL Cheat Sheet

| Task | Command |
|---|---|
| Create table | CREATE TABLE |
| Modify table | ALTER TABLE |
| Delete table | DROP TABLE |
| Add data | INSERT |
| Read data | SELECT |
| Modify data | UPDATE |
| Delete data | DELETE |
| Filter | WHERE |
| Sort | ORDER BY |
| Group | GROUP BY |
| Filter groups | HAVING |
| Combine tables | JOIN |
| Remove duplicates | DISTINCT |
| Limit results | LIMIT |
| Save transaction | COMMIT |
| Undo transaction | ROLLBACK |

---

# 📖 Summary

SQL is the primary language used to interact with relational databases.

The most important concepts include:

- DDL
- DML
- DQL
- DCL
- TCL
- SELECT
- INSERT
- UPDATE
- DELETE
- WHERE
- JOINs
- GROUP BY
- HAVING
- Aggregate functions
- Subqueries
- Views
- Transactions

SQL is fundamental for working with systems such as PostgreSQL, Oracle, MySQL, and SQL Server.

---

## 📚 Related Sections

⬅️ [Relational Databases](../02-relational-databases/)

➡️ [PostgreSQL](../04-postgresql/)

➡️ [Oracle](../05-oracle/)

➡️ [NoSQL](../06-nosql/)

➡️ [Database Design](../08-database-design/)
