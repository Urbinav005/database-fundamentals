# 🐘 PostgreSQL

PostgreSQL is an open-source object-relational database management system (ORDBMS).

It is widely used for applications that require reliability, data integrity, advanced SQL features, and complex queries.

---

## 📌 What is PostgreSQL?

PostgreSQL is a relational database management system based on SQL.

It allows developers to:

- Create databases
- Create tables
- Define relationships
- Insert data
- Query information
- Update records
- Delete records
- Create views
- Use transactions
- Define constraints
- Manage users and permissions

---

## 🏗️ PostgreSQL Architecture

A simplified PostgreSQL structure is:

~~~text
PostgreSQL Server
│
├── Database
│   ├── Schema
│   │   ├── Tables
│   │   ├── Views
│   │   ├── Functions
│   │   └── Sequences
│   │
│   └── Other database objects
│
└── Users / Roles
~~~

---

## 🗄️ Creating a Database

A PostgreSQL database can be created with:

~~~sql
CREATE DATABASE university;
~~~

---

## 📋 Creating Tables

Tables store structured information.

Example:

~~~sql
CREATE TABLE students (
    student_id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(150) UNIQUE NOT NULL,
    age INT,
    career_id INT
);
~~~

The table contains:

| Column | Type | Purpose |
|---|---|---|
| student_id | SERIAL | Automatically generated identifier |
| name | VARCHAR(100) | Student name |
| email | VARCHAR(150) | Student email |
| age | INT | Student age |
| career_id | INT | Related career |

---

## 🔑 Primary Keys

A primary key uniquely identifies each record.

Example:

~~~sql
CREATE TABLE careers (
    career_id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL
);
~~~

Here:

~~~text
career_id → Primary Key
~~~

---

## 🔗 Foreign Keys

Foreign keys establish relationships between tables.

Example:

~~~sql
CREATE TABLE students (
    student_id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    career_id INT,
    FOREIGN KEY (career_id)
        REFERENCES careers(career_id)
);
~~~

The relationship is:

~~~text
CAREERS
   │
   │ career_id
   ▼
STUDENTS
~~~

---

# 🧱 PostgreSQL Data Types

PostgreSQL supports many data types.

### Numeric

| Type | Example |
|---|---|
| SMALLINT | 10 |
| INTEGER | 100 |
| BIGINT | 100000 |
| NUMERIC | 99.99 |
| DECIMAL | 150.50 |
| REAL | 10.5 |

### Character

| Type | Example |
|---|---|
| VARCHAR(n) | `'Rodolfo'` |
| CHAR(n) | `'A'` |
| TEXT | `'Software Development'` |

### Boolean

~~~sql
active BOOLEAN
~~~

Values:

~~~text
TRUE
FALSE
~~~

### Date and Time

PostgreSQL supports:

- DATE
- TIME
- TIMESTAMP
- TIMESTAMPTZ
- INTERVAL

Example:

~~~sql
birth_date DATE
~~~

---

# ⚙️ SERIAL

`SERIAL` can be used to automatically generate integer values for identifiers.

Example:

~~~sql
CREATE TABLE students (
    student_id SERIAL PRIMARY KEY,
    name VARCHAR(100)
);
~~~

When records are inserted, PostgreSQL generates the identifier automatically.

Example:

~~~sql
INSERT INTO students (name)
VALUES ('Rodolfo');

INSERT INTO students (name)
VALUES ('Carlos');
~~~

The generated IDs can be:

~~~text
1
2
~~~

---

# ➕ INSERT

Insert data into a table:

~~~sql
INSERT INTO careers (name)
VALUES ('Software Development');
~~~

Multiple records:

~~~sql
INSERT INTO careers (name)
VALUES
('Software Development'),
('Computer Engineering'),
('Information Systems');
~~~

---

# 🔎 SELECT

Retrieve data:

~~~sql
SELECT *
FROM students;
~~~

Select specific columns:

~~~sql
SELECT name, email
FROM students;
~~~

---

# 🎯 WHERE

Filter records:

~~~sql
SELECT *
FROM students
WHERE age >= 18;
~~~

---

# 🔄 UPDATE

Modify existing data:

~~~sql
UPDATE students
SET age = 22
WHERE student_id = 1;
~~~

Always use a `WHERE` condition when you only want to modify specific records.

---

# 🗑️ DELETE

Delete records:

~~~sql
DELETE FROM students
WHERE student_id = 1;
~~~

⚠️ Without `WHERE`, all records can be deleted.

---

# 🔗 JOINs in PostgreSQL

PostgreSQL supports different types of JOINs.

## INNER JOIN

~~~sql
SELECT
    students.name,
    careers.name AS career
FROM students
INNER JOIN careers
    ON students.career_id = careers.career_id;
~~~

## LEFT JOIN

~~~sql
SELECT
    students.name,
    careers.name AS career
FROM students
LEFT JOIN careers
    ON students.career_id = careers.career_id;
~~~

## RIGHT JOIN

~~~sql
SELECT
    students.name,
    careers.name AS career
FROM students
RIGHT JOIN careers
    ON students.career_id = careers.career_id;
~~~

## FULL OUTER JOIN

~~~sql
SELECT
    students.name,
    careers.name AS career
FROM students
FULL OUTER JOIN careers
    ON students.career_id = careers.career_id;
~~~

---

# 📊 GROUP BY

Example:

~~~sql
SELECT
    career_id,
    COUNT(*) AS total_students
FROM students
GROUP BY career_id;
~~~

---

# 📈 Aggregate Functions

PostgreSQL supports aggregate functions such as:

- COUNT()
- SUM()
- AVG()
- MIN()
- MAX()

Example:

~~~sql
SELECT
    AVG(age) AS average_age
FROM students;
~~~

---

# 🪆 Subqueries

PostgreSQL supports nested queries.

Example:

~~~sql
SELECT name, age
FROM students
WHERE age > (
    SELECT AVG(age)
    FROM students
);
~~~

---

# 👁️ Views

A view is a virtual table based on a query.

Example:

~~~sql
CREATE VIEW student_careers AS
SELECT
    students.student_id,
    students.name,
    careers.name AS career
FROM students
INNER JOIN careers
    ON students.career_id = careers.career_id;
~~~

Use the view:

~~~sql
SELECT *
FROM student_careers;
~~~

---

# 🔐 Constraints

PostgreSQL supports several important constraints.

### PRIMARY KEY

~~~sql
student_id SERIAL PRIMARY KEY
~~~

### FOREIGN KEY

~~~sql
FOREIGN KEY (career_id)
REFERENCES careers(career_id)
~~~

### NOT NULL

~~~sql
name VARCHAR(100) NOT NULL
~~~

### UNIQUE

~~~sql
email VARCHAR(150) UNIQUE
~~~

### CHECK

~~~sql
age INT CHECK (age >= 18)
~~~

---

# 🔄 Transactions

PostgreSQL supports transactions.

A transaction can be started with:

~~~sql
BEGIN;
~~~

Example:

~~~sql
BEGIN;

UPDATE students
SET age = 22
WHERE student_id = 1;

COMMIT;
~~~

If the changes should be cancelled:

~~~sql
ROLLBACK;
~~~

---

# 🧩 Schemas

A schema organizes database objects.

The default PostgreSQL schema is commonly:

~~~text
public
~~~

Example:

~~~sql
CREATE SCHEMA university;
~~~

A table can then be created inside that schema:

~~~sql
CREATE TABLE university.students (
    student_id SERIAL PRIMARY KEY,
    name VARCHAR(100)
);
~~~

---

# 👤 Users and Roles

PostgreSQL uses roles to manage authentication and permissions.

Example:

~~~sql
CREATE ROLE student_user
LOGIN
PASSWORD 'example_password';
~~~

Permissions can be granted with:

~~~sql
GRANT SELECT
ON students
TO student_user;
~~~

⚠️ Never commit real passwords or credentials to a public GitHub repository.

---

# 🛡️ PostgreSQL Data Integrity

PostgreSQL provides mechanisms to maintain reliable data.

These include:

- Primary keys
- Foreign keys
- NOT NULL
- UNIQUE
- CHECK
- Transactions
- Referential integrity

These features help prevent invalid or inconsistent data.

---

# 🧠 PostgreSQL-Specific Features

PostgreSQL supports standard SQL but also provides advanced features such as:

- JSON and JSONB
- Arrays
- Extensions
- Advanced indexing
- Common Table Expressions
- Window functions
- Custom data types
- Full-text search

---

# 📦 JSON and JSONB

PostgreSQL can store JSON data.

Example:

~~~sql
CREATE TABLE products (
    product_id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    data JSONB
);
~~~

Insert JSON:

~~~sql
INSERT INTO products (name, data)
VALUES (
    'Laptop',
    '{"brand": "HP", "ram": 16, "gpu": "RTX 4050"}'
);
~~~

This allows PostgreSQL to work with some semi-structured data while remaining a relational database.

---

# 🪟 Window Functions

Window functions perform calculations across related rows without grouping them into a single result.

Example:

~~~sql
SELECT
    name,
    age,
    AVG(age) OVER () AS average_age
FROM students;
~~~

Each student remains as an individual row while the average is calculated across the result.

---

# 🔍 Indexes

Indexes can improve query performance.

Example:

~~~sql
CREATE INDEX idx_students_email
ON students(email);
~~~

Indexes should be designed carefully because they require storage and can add overhead to data modification operations.

---

# 🧰 PostgreSQL Tools

PostgreSQL can be managed using several tools.

### pgAdmin

Graphical administration tool for PostgreSQL.

### DBeaver

Database management tool that can connect to PostgreSQL and many other database systems.

### psql

PostgreSQL's command-line client.

Example:

~~~text
psql -U postgres
~~~

---

# 🖥️ Basic psql Commands

List databases:

~~~text
\l
~~~

Connect to a database:

~~~text
\c university
~~~

List tables:

~~~text
\dt
~~~

Show table structure:

~~~text
\d students
~~~

Exit psql:

~~~text
\q
~~~

---

# 🧪 Example University Database

A simple university database can contain:

~~~text
UNIVERSITY DATABASE
│
├── careers
├── students
├── teachers
├── courses
└── enrollments
~~~

Possible relationships:

~~~text
CAREERS
   │
   │ 1
   │
   │ N
   ▼
STUDENTS
   │
   │ N
   │
   ▼
ENROLLMENTS
   ▲
   │ N
   │
   │ 1
COURSES
~~~

---

# 🧮 Complete PostgreSQL Example

~~~sql
CREATE TABLE careers (
    career_id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL UNIQUE
);

CREATE TABLE students (
    student_id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(150) UNIQUE NOT NULL,
    age INT CHECK (age >= 18),
    career_id INT,
    FOREIGN KEY (career_id)
        REFERENCES careers(career_id)
);

INSERT INTO careers (name)
VALUES
('Software Development'),
('Computer Engineering');

INSERT INTO students (name, email, age, career_id)
VALUES
('Rodolfo', 'rodolfo@email.com', 21, 1),
('Carlos', 'carlos@email.com', 20, 1),
('Ana', 'ana@email.com', 22, 2);

SELECT
    s.name AS student,
    s.email,
    c.name AS career
FROM students AS s
INNER JOIN careers AS c
    ON s.career_id = c.career_id;
~~~

---

# 📚 PostgreSQL Cheat Sheet

| Task | PostgreSQL |
|---|---|
| Create database | CREATE DATABASE |
| Create table | CREATE TABLE |
| Insert data | INSERT |
| Read data | SELECT |
| Update data | UPDATE |
| Delete data | DELETE |
| Add column | ALTER TABLE |
| Delete table | DROP TABLE |
| Create schema | CREATE SCHEMA |
| Create view | CREATE VIEW |
| Create index | CREATE INDEX |
| Start transaction | BEGIN |
| Save transaction | COMMIT |
| Cancel transaction | ROLLBACK |
| Create role | CREATE ROLE |
| Grant permission | GRANT |

---

# 📖 Summary

PostgreSQL is a powerful relational database management system that supports standard SQL along with many advanced features.

Important PostgreSQL concepts include:

- Databases
- Schemas
- Tables
- Primary keys
- Foreign keys
- Constraints
- Data types
- SQL queries
- JOINs
- Views
- Transactions
- Roles and permissions
- Indexes
- JSONB
- Window functions

PostgreSQL is useful for both educational projects and production applications.

---

## 📚 Related Sections

⬅️ [Fundamentals](../01-fundamentals/)

⬅️ [Relational Databases](../02-relational-databases/)

⬅️ [SQL](../03-sql/)

➡️ [Oracle](../05-oracle/)

➡️ [NoSQL](../06-nosql/)

➡️ [Tools](../07-tools/)

➡️ [Database Design](../08-database-design/)
