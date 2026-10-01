# 🗃️ Relational Databases

Relational databases organize data into structured tables and establish relationships between them using keys.

---

## 📋 What is a Relational Database?

A relational database stores information in **tables** made up of rows and columns.

Each table normally represents an entity, while relationships between tables allow related information to be connected.

### Example

A university database could contain:

- STUDENTS
- COURSES
- TEACHERS
- CAREERS
- ENROLLMENTS

---

## 📊 Tables

A table is one of the main structures of a relational database.

It is composed of:

| Element | Description |
|---|---|
| Row | A single record |
| Column | An attribute of the data |
| Primary Key | Unique identifier of a record |
| Foreign Key | Reference to another table |

### Example

~~~text
STUDENTS

student_id | name    | email
-----------|---------|--------------------
1          | Rodolfo | rodolfo@email.com
2          | Carlos  | carlos@email.com
3          | Ana     | ana@email.com
~~~

---

## 🔑 Primary Key

A **Primary Key (PK)** uniquely identifies each record in a table.

### Characteristics

- Must be unique
- Cannot normally contain NULL values
- Identifies a specific record
- Provides a unique identity for each row

### Example

~~~sql
CREATE TABLE students (
    student_id INT PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(150)
);
~~~

Here, `student_id` uniquely identifies each student.

---

## 🔗 Foreign Key

A **Foreign Key (FK)** creates a relationship between two tables.

It references a primary key from another table.

### Example

~~~sql
CREATE TABLE careers (
    career_id INT PRIMARY KEY,
    name VARCHAR(100)
);

CREATE TABLE students (
    student_id INT PRIMARY KEY,
    name VARCHAR(100),
    career_id INT,
    FOREIGN KEY (career_id)
        REFERENCES careers(career_id)
);
~~~

The column `students.career_id` references `careers.career_id`.

---

# 🔄 Relationships

Relationships define how records from different tables are connected.

The main types are:

- One-to-One
- One-to-Many
- Many-to-Many

---

## 1️⃣ One-to-One (1:1)

One record in table A is associated with one record in table B.

~~~text
PERSON -------- PASSPORT
   1                1
~~~

Example:

One person has one passport.

---

## 2️⃣ One-to-Many (1:N)

One record can be associated with multiple records.

~~~text
CAREER
   |
   |--- STUDENT
   |--- STUDENT
   |--- STUDENT
~~~

Example:

One career can have many students.

---

## 3️⃣ Many-to-Many (N:M)

Multiple records from one table can be related to multiple records from another table.

~~~text
STUDENTS ---- ENROLLMENTS ---- COURSES
~~~

A student can enroll in many courses.

A course can contain many students.

A third table, such as `enrollments`, is normally used to represent this relationship.

---

# 🛡️ Constraints

Constraints are rules applied to database columns to maintain data integrity.

### PRIMARY KEY

Uniquely identifies a record.

~~~sql
student_id INT PRIMARY KEY
~~~

### FOREIGN KEY

Maintains relationships between tables.

~~~sql
FOREIGN KEY (career_id)
REFERENCES careers(career_id)
~~~

### NOT NULL

Prevents a column from containing NULL values.

~~~sql
name VARCHAR(100) NOT NULL
~~~

### UNIQUE

Prevents duplicate values.

~~~sql
email VARCHAR(150) UNIQUE
~~~

### CHECK

Restricts values according to a condition.

~~~sql
age INT CHECK (age >= 18)
~~~

### DEFAULT

Provides a default value.

~~~sql
status VARCHAR(20) DEFAULT 'active'
~~~

---

# 🧹 Database Normalization

Normalization is the process of organizing data to reduce redundancy and improve data integrity.

The main normal forms are:

~~~text
1NF
 ↓
2NF
 ↓
3NF
~~~

---

## 1NF — First Normal Form

A table should contain atomic values.

Each field should contain a single value instead of a list of values.

### Bad example

~~~text
student_id | courses
-----------|---------------------------
1          | Math, Physics, Database
~~~

### Better example

~~~text
student_id | course
-----------|----------
1          | Math
1          | Physics
1          | Database
~~~

---

## 2NF — Second Normal Form

A table must:

- Be in 1NF
- Have no partial dependency on a composite primary key

The objective is to make sure that non-key attributes depend on the entire primary key.

---

## 3NF — Third Normal Form

A table must:

- Be in 2NF
- Have no unnecessary transitive dependencies

The objective is to prevent non-key attributes from depending on other non-key attributes.

---

# 🧠 Data Integrity

Data integrity means maintaining accurate, consistent, and reliable information.

Relational databases use several mechanisms to maintain integrity:

- Primary keys
- Foreign keys
- Constraints
- Data types
- Transactions
- Referential integrity

### Referential Integrity

Foreign keys help ensure that relationships between tables remain valid.

---

# 🔄 CRUD Operations

CRUD represents the four basic operations performed on data.

| Operation | SQL Command | Purpose |
|---|---|---|
| Create | INSERT | Add data |
| Read | SELECT | Retrieve data |
| Update | UPDATE | Modify data |
| Delete | DELETE | Remove data |

### Example

~~~sql
INSERT INTO students (student_id, name)
VALUES (1, 'Rodolfo');

SELECT *
FROM students;

UPDATE students
SET name = 'Rodolfo Urbina'
WHERE student_id = 1;

DELETE FROM students
WHERE student_id = 1;
~~~

---

# 🧩 Entity Relationships

In database design, tables normally represent entities.

For example:

~~~text
STUDENT
COURSE
TEACHER
CAREER
ENROLLMENT
~~~

Relationships connect these entities.

---

# 🧱 Schema

A **database schema** describes the logical structure of a database.

It can define:

- Tables
- Columns
- Data types
- Relationships
- Constraints
- Views
- Other database objects

### Example

~~~text
University Database
|
|-- students
|-- teachers
|-- careers
|-- courses
`-- enrollments
~~~

---

# 🧠 Relational Database Advantages

Relational databases provide several important advantages:

- Structured data
- Strong data integrity
- Relationships between entities
- Powerful SQL queries
- Transactions
- Data consistency
- Well-defined schemas
- Referential integrity
- Data normalization

---

# ⚠️ Considerations

Relational databases also have some limitations depending on the application.

- Schema changes may require planning
- Complex relationships can increase query complexity
- Horizontal scaling can require additional architecture
- Large amounts of unstructured data may be better suited to other database models

The appropriate database model depends on the requirements of the system.

---

# 🗄️ Examples of Relational DBMS

| DBMS | Description |
|---|---|
| PostgreSQL | Open-source relational database |
| Oracle Database | Enterprise relational database |
| MySQL | Popular open-source relational database |
| Microsoft SQL Server | Microsoft's relational database system |

---

# 🆚 Relational vs Non-Relational

| Relational | Non-Relational |
|---|---|
| Tables | Documents, key-value, graphs, etc. |
| Structured schema | Flexible schema |
| SQL | Different query models |
| Strong relationships | Relationships handled differently |
| PostgreSQL | MongoDB |
| Oracle | Redis / Neo4j |

Neither model is universally better.

The appropriate choice depends on the type of data, application requirements, scalability needs, and consistency requirements.

---

# 📚 Key Concepts

The most important concepts in relational databases include:

~~~text
Tables
   ↓
Rows & Columns
   ↓
Primary Keys
   ↓
Foreign Keys
   ↓
Relationships
   ↓
Constraints
   ↓
Normalization
   ↓
Data Integrity
   ↓
SQL
~~~

---

# 📖 Summary

A relational database organizes information into structured tables.

Primary keys uniquely identify records, while foreign keys establish relationships between tables.

Relationships can be:

- One-to-One
- One-to-Many
- Many-to-Many

Constraints help maintain data integrity, while normalization reduces redundancy and improves database organization.

SQL is used to create, retrieve, modify, and delete information stored in relational databases.

---

## 📚 Related Sections

⬅️ [Database Fundamentals](../01-fundamentals/)

➡️ [SQL](../03-sql/)

➡️ [PostgreSQL](../04-postgresql/)

➡️ [Oracle](../05-oracle/)

➡️ [NoSQL](../06-nosql/)

➡️ [Database Design](../08-database-design/)
