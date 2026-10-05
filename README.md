# University-Database-Management-System
DBMS  project containing SQL programs for table creation, data manipulation, nested queries, joins, materialized views, SQL functions, transactions, and student/employee database operations using Oracle SQL.
# DBMS PROJECT — SQL Programs & Database Operations

Welcome to the **DBMS PROJECT ** repository. This project contains SQL programs, database operations, sample tables, queries, and practical implementations completed as part of the Database Management Systems laboratory.

The project is designed to provide hands-on experience with **Oracle SQL** and important relational database concepts such as table creation, data manipulation, nested queries, joins, views, SQL functions, and transaction management.

---

## 📌 Project Overview

A Database Management System (DBMS) is used to store, organize, retrieve, and manage data efficiently.

In this project, different real-world entities such as:

* Employees
* Departments
* Students
* Courses
* Enrollments
* Instructors

are represented using relational database tables.

SQL queries are then used to perform operations such as inserting data, retrieving records, updating information, combining tables, performing calculations, and managing transactions.

---

## 🎯 Objectives

The main objectives of this project are:

1. To understand relational database concepts.
2. To create and manage database tables.
3. To insert and retrieve records using SQL.
4. To perform data manipulation operations.
5. To understand and implement nested queries.
6. To perform different types of joins.
7. To create and query materialized views.
8. To use numeric and date/time SQL functions.
9. To understand transaction control commands.
10. To gain practical experience with Oracle SQL.

---

# 🗂️ Database Tables

The project uses multiple tables to represent different entities.

## 1. Department Table

The `Department` table stores information about different departments.

### Important Columns

| Column      | Description            |
| ----------- | ---------------------- |
| `Dept_ID`   | Unique department ID   |
| `Dept_Name` | Name of the department |

Example departments:

* Finance
* IT
* HR
* Marketing

---

## 2. Employee Table

The `Employee` table stores employee information.

### Important Columns

| Column     | Description                         |
| ---------- | ----------------------------------- |
| `Emp_ID`   | Unique employee ID                  |
| `Emp_Name` | Employee name                       |
| `Dept_ID`  | Department assigned to the employee |
| `City`     | Employee's city                     |
| `Salary`   | Employee salary                     |

The `Dept_ID` column connects the Employee table with the Department table.

---

# 🔍 SQL Concepts Covered

## 1. Table Creation

Tables are created using the `CREATE TABLE` command.

Example:

```sql
CREATE TABLE Department (
    Dept_ID NUMBER PRIMARY KEY,
    Dept_Name VARCHAR2(30)
);
```

The `PRIMARY KEY` constraint ensures that every department has a unique ID.

---

## 2. Data Insertion

The `INSERT INTO` command is used to add records to a table.

Example:

```sql
INSERT INTO Department
VALUES (10, 'Finance');
```

Multiple records can be inserted to populate the database for testing and query execution.

---

## 3. SELECT Queries

The `SELECT` statement is used to retrieve data from tables.

Example:

```sql
SELECT *
FROM Employee;
```

Specific columns can also be selected:

```sql
SELECT Emp_ID, Emp_Name, Salary
FROM Employee;
```

---

# 🧠 Nested Queries / Subqueries

A nested query is a query written inside another query.

For example, to find employees working in the **Finance and IT departments**, the inner query first finds the department IDs.

```sql
SELECT Dept_ID
FROM Department
WHERE Dept_Name IN ('Finance', 'IT');
```

The outer query then uses those IDs:

```sql
SELECT *
FROM Employee
WHERE Dept_ID IN
(
    SELECT Dept_ID
    FROM Department
    WHERE Dept_Name IN ('Finance', 'IT')
);
```

### Why Nested Queries Are Used

Nested queries are useful when the result of one query is required as a condition for another query.

---

# 👁️ Materialized Views

A materialized view stores the result of a query physically in the database.

Example:

```sql
CREATE MATERIALIZED VIEW Emp_Dept_MV
AS
SELECT E.Emp_ID,
       E.Emp_Name,
       D.Dept_ID,
       D.Dept_Name
FROM Employee E
JOIN Department D
ON E.Dept_ID = D.Dept_ID;
```

The materialized view can then be queried like a table:

```sql
SELECT *
FROM Emp_Dept_MV;
```

It can also be refreshed when required:

```sql
BEGIN
    DBMS_MVIEW.REFRESH('EMP_DEPT_MV');
END;
/
```

### Advantage

Materialized views can improve performance when the same complex query needs to be accessed repeatedly.

---

# 👨‍🏫 Instructor and Course Queries

The project also demonstrates retrieving instructors who teach a particular course.

Example:

```sql
SELECT Instructor_ID, Instructor_Name
FROM Instructor
WHERE Instructor_ID IN
(
    SELECT Instructor_ID
    FROM Teaches
    WHERE Course_ID = 'C101'
);
```

The inner query identifies the instructors associated with the course, while the outer query retrieves their details.

---

# 🎓 Student Enrollment and Grades

Student enrollment information can be retrieved by joining the `Student` and `Enrollment` tables.

```sql
SELECT S.Student_ID,
       S.Student_Name,
       E.Course_ID,
       E.Grade
FROM Student S
INNER JOIN Enrollment E
ON S.Student_ID = E.Student_ID;
```

This displays:

* Student ID
* Student name
* Course ID
* Grade

---

# 🔗 SQL Joins

Joins are used to combine data from multiple tables based on a related column.

The project demonstrates four major joins.

## INNER JOIN

Returns only matching records.

```sql
SELECT E.Emp_ID,
       E.Emp_Name,
       D.Dept_Name
FROM Employee E
INNER JOIN Department D
ON E.Dept_ID = D.Dept_ID;
```

---

## LEFT OUTER JOIN

Returns all records from the left table and matching records from the right table.

```sql
SELECT E.Emp_ID,
       E.Emp_Name,
       D.Dept_Name
FROM Employee E
LEFT JOIN Department D
ON E.Dept_ID = D.Dept_ID;
```

---

## RIGHT OUTER JOIN

Returns all records from the right table and matching records from the left table.

```sql
SELECT E.Emp_ID,
       E.Emp_Name,
       D.Dept_Name
FROM Employee E
RIGHT JOIN Department D
ON E.Dept_ID = D.Dept_ID;
```

---

## FULL OUTER JOIN

Returns matching and non-matching records from both tables.

```sql
SELECT E.Emp_ID,
       E.Emp_Name,
       D.Dept_Name
FROM Employee E
FULL OUTER JOIN Department D
ON E.Dept_ID = D.Dept_ID;
```

---

# ✏️ UPDATE Operation

The `UPDATE` command is used to modify existing records.

Example:

```sql
UPDATE Employee
SET City = 'Hyderabad'
WHERE Emp_ID = 101;
```

The employee's city is changed only for the employee whose ID is `101`.

The changes can then be saved using:

```sql
COMMIT;
```

---

# 🔢 Numeric SQL Functions

The project demonstrates commonly used numeric functions.

### ABS()

Returns the absolute value.

```sql
SELECT ABS(-25)
FROM DUAL;
```

### ROUND()

Rounds a number to a specified number of decimal places.

```sql
SELECT ROUND(45.678, 2)
FROM DUAL;
```

### CEIL()

Returns the smallest integer greater than or equal to a number.

```sql
SELECT CEIL(45.2)
FROM DUAL;
```

### FLOOR()

Returns the largest integer less than or equal to a number.

```sql
SELECT FLOOR(45.8)
FROM DUAL;
```

### MOD()

Returns the remainder after division.

```sql
SELECT MOD(10, 3)
FROM DUAL;
```

---

# 📅 Date and Time Functions

Oracle provides several functions for working with dates and time.

### SYSDATE

Returns the current system date.

```sql
SELECT SYSDATE
FROM DUAL;
```

### CURRENT_TIMESTAMP

Returns the current date and time with time-zone information.

```sql
SELECT CURRENT_TIMESTAMP
FROM DUAL;
```

### ADD_MONTHS()

Adds a specified number of months to a date.

```sql
SELECT ADD_MONTHS(SYSDATE, 2)
FROM DUAL;
```

### LAST_DAY()

Returns the last day of the month.

```sql
SELECT LAST_DAY(SYSDATE)
FROM DUAL;
```

### EXTRACT()

Extracts a specific part of a date.

```sql
SELECT EXTRACT(YEAR FROM SYSDATE)
FROM DUAL;
```

---

# 💾 Transaction Control

The project demonstrates three important transaction control commands.

## COMMIT

`COMMIT` permanently saves the changes made during a transaction.

```sql
COMMIT;
```

---

## SAVEPOINT

`SAVEPOINT` creates a temporary point within a transaction.

```sql
SAVEPOINT S1;
```

---

## ROLLBACK

`ROLLBACK` cancels changes made after a specified savepoint.

```sql
ROLLBACK TO S1;
```

### Example

```sql
UPDATE Employee
SET Salary = Salary + 1000
WHERE Emp_ID = 101;

SAVEPOINT S1;

UPDATE Employee
SET Salary = Salary + 2000
WHERE Emp_ID = 102;

ROLLBACK TO S1;

COMMIT;
```

In this example, the first update is retained, while the second update is cancelled.

---

# 🛠️ Technologies Used

| Technology           | Purpose                            |
| -------------------- | ---------------------------------- |
| SQL                  | Database querying and manipulation |
| Oracle Database      | Database management system         |
| Oracle SQL Developer | SQL development and execution      |

---

# 📁 Repository Contents

The repository contains:

* SQL table creation scripts
* Sample data
* SQL queries
* Nested query examples
* Join operations
* Materialized view queries
* Numeric and date/time functions
* Transaction control examples
* Student and employee database operations
* Expected outputs for practical exercises

---

# 🎓 Learning Outcomes

After completing this project, the learner will be able to:

* Create relational database tables.
* Define primary and foreign keys.
* Insert and manipulate database records.
* Write simple and nested SQL queries.
* Use different types of joins.
* Create and query materialized views.
* Apply SQL built-in functions.
* Work with dates and numerical values.
* Manage transactions using `COMMIT`, `SAVEPOINT`, and `ROLLBACK`.
* Solve practical database problems using SQL.

---
