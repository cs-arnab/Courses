```markdown
# SQL Guide
**Author**: Arnab Dana

---

### Resource
- [W3Schools SQL Tutorial](https://www.w3schools.com/sql/default.asp)

---

### Content
1. [Category of Queries](#1-category-of-queries)
2. [Introduction](#2-introduction)
3. [DQL (Data Query Language)](#3-dql-data-query-language)
4. Regex
5. SQL Operator
6. DDL (Data Definition Language)
7. DML (Data Manipulation Language)
8. DCL (Data Control Language)
9. TCL (Transaction Control Language)
10. Aggregate Functions
11. Joins
12. Execution Sequence of Clause
13. Creating Custom Functions in SQL
14. SQL NULL Functions
15. Stored Procedures
16. SQL Constraints
17. SQL Indexing
18. Other Topics
19. Data Types
20. Quick Reference

---

### 1. Category of Queries
In SQL, queries are categorized into different types based on the kind of operations they perform on the database. The main categories are:

| **Category** | **Full Form**               | **Purpose**                          | **Examples**               |
|--------------|-----------------------------|--------------------------------------|----------------------------|
| **DDL**      | Data Definition Language    | Defines and modifies database structure | `CREATE`, `ALTER`, `DROP`, `TRUNCATE` |
| **DML**      | Data Manipulation Language  | Manipulates data within tables       | `INSERT`, `UPDATE`, `DELETE`, `MERGE` |
| **DQL**      | Data Query Language         | Retrieves data from the database     | `SELECT`                  |
| **DCL**      | Data Control Language       | Controls access to data and permissions | `GRANT`, `REVOKE`       |
| **TCL**      | Transaction Control Language| Manages transactions to maintain database integrity | `COMMIT`, `ROLLBACK`, `SAVEPOINT` |

---

### 2. Introduction

#### What is a Database?
A database is an organized collection of data that is stored and accessed electronically. Think of it as a digital filing system where information is stored in a structured way, making it easy to retrieve, manage, and update.

1. **Structured Storage**: Data is stored in a specific format, often in tables with rows and columns, making it easy to query and analyze.
2. **Consistency**: The data stored is consistent, meaning that the same type of data is stored in the same way across the database.
3. **Integrity**: Data integrity ensures that the data is accurate and reliable.
4. **Scalability**: Databases can grow in size, handling more data without performance issues.

---

#### Question) What is a Database Management System (DBMS)?
A Database Management System (DBMS) is software that allows users to create, manage, and interact with databases. It acts as an intermediary between the user and the database, enabling users to easily retrieve, insert, update, and delete data while ensuring that the data is secure and consistent.

---

#### Question) What is a Relational Database Management System (RDBMS)?
RDBMS stands for Relational Database Management System. It is a type of database management system (DBMS) that stores data in a structured format, using rows and columns, which are organized into tables. The key feature of an RDBMS is that it uses relationships (or links) between tables to manage and query data efficiently.

Here are some key points about RDBMS:
- **Tables**: Data is stored in tables, where each table consists of rows (records) and columns (attributes).
- **Primary Key**: Each table typically has a primary key, a unique identifier for each row in the table.
- **Foreign Key**: Relationships between tables are established using foreign keys, which are fields in one table that refer to the primary key in another table.
- **SQL (Structured Query Language)**: RDBMS systems use SQL for querying, updating, and managing the data.
- **Normalization**: RDBMSs often involve the normalization process, which organizes data to minimize redundancy and dependency.
- **Examples**: MySQL, PostgreSQL, Microsoft SQL Server, Oracle Database.

---

#### Question) What is SQL?
SQL (Structured Query Language) is a standardized programming language used to manage and manipulate relational databases. It is the primary language used for querying, inserting, updating, and deleting data in relational databases, as well as for creating and modifying the database structure itself.

Here are the key components of SQL:
1. **Data Query Language (DQL)**: Used to query data from the database. The most common command is `SELECT`.
2. **Data Manipulation Language (DML)**: Used to insert, update, and delete data.
3. **Data Definition Language (DDL)**: Used to define or alter the structure of the database, such as creating, altering, or dropping tables.
4. **Data Control Language (DCL)**: Used to control access to the data, like granting and revoking permissions.
5. **Transaction Control Language (TCL)**: Used to manage transactions in the database, ensuring data integrity.
   - `COMMIT`: Saves all changes made in the current transaction.
   - `ROLLBACK`: Undoes all changes made in the current transaction.

---

### 3. DQL (Data Query Language)

#### 1. Read Data from Customers Table
```sql
SELECT * FROM Customers; -- * means all columns
SELECT CustomerName, City FROM Customers;
```

#### 2. DISTINCT
```sql
SELECT DISTINCT Country FROM Customers;
SELECT COUNT(DISTINCT column_name) AS DistinctCountries FROM table_name;
```

#### 3. WHERE Clause
```sql
SELECT * FROM Customers
WHERE Country = 'Mexico';
```

#### 4. ORDER BY
```sql
SELECT * FROM Products
ORDER BY Price;

SELECT column1, column2, ...
FROM table_name
ORDER BY column1, column2, ... ASC|DESC;

SELECT * FROM Customers
ORDER BY Country ASC, CustomerName DESC;
```

#### 5. TOP
Retrieves a specified number of rows from a result set.
```sql
SELECT TOP number | percentage columns
FROM table_name
WHERE condition;

-- Example: Get the top 5 highest-paid employees
SELECT TOP 5 * FROM Employees ORDER BY Salary DESC;

-- Example: Get the top 10% of employees
SELECT TOP 10 PERCENT * FROM Employees ORDER BY Salary DESC;
```

#### 6. LIMIT
Retrieves a specific number of rows.
```sql
SELECT columns FROM table_name
WHERE condition
LIMIT number;

-- Example: Get the top 5 employees
SELECT * FROM Employees ORDER BY Salary DESC LIMIT 5;

-- Example: Get rows 5 to 10 (Pagination)
SELECT * FROM Employees ORDER BY EmployeeID LIMIT 5 OFFSET 5;
```

#### 7. FETCH FIRST
Works similarly to `LIMIT`.
```sql
SELECT columns FROM table_name
ORDER BY column_name
FETCH FIRST number ROWS ONLY;

SELECT * FROM Employees FETCH FIRST 5 ROWS ONLY;
```

#### 8. ROWNUM
Filters rows **before** sorting (needs a subquery for correct results).
```sql
SELECT * FROM table_name WHERE ROWNUM <= number;

SELECT * FROM 
(SELECT * FROM Employees ORDER BY Salary DESC) 
WHERE ROWNUM <= 5;
```

#### 9. Alias
Rename a column.
```sql
SELECT COUNT(*) AS [Number of records]
FROM Products;
```

#### 10. GROUP BY
```sql
SELECT column_name(s)
FROM table_name
WHERE condition
GROUP BY column_name(s)
ORDER BY column_name(s);

SELECT COUNT(CustomerID), Country
FROM Customers
GROUP BY Country;
```

#### 11. HAVING
```sql
SELECT column_name(s)
FROM table_name
WHERE condition
GROUP BY column_name(s)
HAVING condition
ORDER BY column_name(s);

SELECT COUNT(CustomerID), Country
FROM Customers
GROUP BY Country
HAVING COUNT(CustomerID) > 5
ORDER BY COUNT(CustomerID) DESC;
```

#### 12. EXISTS
The `EXISTS` operator is used to test for the existence of any record in a subquery.
```sql
SELECT column_name(s)
FROM table_name
WHERE EXISTS
(SELECT column_name FROM table_name WHERE condition);
```

#### 13. SELECT INTO
The `SELECT INTO` statement copies data from one table into a new table.
```sql
SELECT *
INTO newtable [IN externaldb]
FROM oldtable
WHERE condition;

-- The following SQL statement creates a backup copy of Customers:
SELECT * INTO CustomersBackup2017
FROM Customers;

-- The following SQL statement uses the IN clause to copy the table into a new table in another database:
SELECT * INTO CustomersBackup2017 IN 'Backup.mdb'
FROM Customers;
```

#### 14. CASE Expression
```sql
CASE
    WHEN condition1 THEN result1
    WHEN condition2 THEN result2
    WHEN conditionN THEN resultN
    ELSE result
END;

-- Example 2
SELECT OrderID, Quantity,
CASE
    WHEN Quantity > 30 THEN 'The quantity is greater than 30'
    WHEN Quantity = 30 THEN 'The quantity is 30'
    ELSE 'The quantity is under 30'
END AS QuantityText
FROM OrderDetails;

-- Example Output:
-- OrderID  Quantity  QuantityText
-- 10248    12        The quantity is under 30
-- 10248    10        The quantity is under 30
-- 10248    5         The quantity is under 30

-- Example 3
SELECT CustomerName, City, Country
FROM Customers
ORDER BY
(CASE
    WHEN City IS NULL THEN Country
    ELSE City
END);
```
Here’s the content converted into a properly formatted `README.md` file using Markdown syntax:

```markdown
# SQL Regex and Operators Guide

## 4. Regex

SQL supports **regular expressions (regex)** in some database systems, like MySQL, PostgreSQL, and Oracle, for pattern matching beyond `LIKE`. Below are commonly used regex patterns in SQL:

### Basic Wildcards (`LIKE` Operator)

| Symbol | Description                        | Example                              |
|--------|------------------------------------|--------------------------------------|
| `%`    | Matches zero or more characters    | `WHERE name LIKE 'A%'` (Names starting with 'A') |
| `_`    | Matches a single character         | `WHERE name LIKE 'J_n'` (Matches 'Jon', 'Jan', etc.) |
| `-`    | Represents any single character within the specified range | `WHERE CustomerName LIKE '[a-f]%';` (Returns all customers starting with "a", "b", "c", "d", "e", or "f") |

### Regex Patterns (`REGEXP` or `SIMILAR TO`) *(Depends on SQL Database)*

| Regex Pattern | Description                           | Example                                      |
|---------------|---------------------------------------|----------------------------------------------|
| `^`           | Start of string                       | `WHERE name REGEXP '^A'` (Names starting with 'A') |
| `$`           | End of string                         | `WHERE email REGEXP 'gmail.com$'` (Emails ending with 'gmail.com') |
| `.`           | Matches any single character          | `WHERE name REGEXP 'J.n'` (Matches 'Jon', 'Jan', etc.) |
| `[abc]`       | Matches any character in brackets     | `WHERE name REGEXP '[JKT]ohn'` (Matches 'John', 'Kohn', or 'Tohn') |
| `[^abc]`      | Matches any character *not* in brackets | `WHERE name REGEXP '[^JK]ohn'` (Excludes 'John' & 'Kohn') |
| `[a-z]`       | Matches any character in a range      | `WHERE name REGEXP '[a-d]an'` (Matches 'Aman', 'Bman', etc.) |
| `*`           | Matches 0 or more occurrences         | `WHERE name REGEXP 'A*'` (Matches '', 'A', 'AA', etc.) |
| `+`           | Matches 1 or more occurrences         | `WHERE name REGEXP 'A+'` (Matches 'A', 'AA', but not '') |
| `?`           | Matches 0 or 1 occurrence             | `WHERE name REGEXP 'colou?r'` (Matches 'color' & 'colour') |
| `{n,m}`       | Matches between `n` and `m` occurrences | `WHERE name REGEXP 'A{2,4}'` (Matches 'AA', 'AAA', or 'AAAA') |

### Special SQL-Specific Regex Usage

| Database   | Regex Support             | Example                                           |
|------------|---------------------------|--------------------------------------------------|
| MySQL      | `REGEXP` operator         | `SELECT * FROM users WHERE name REGEXP '^[A-Z].*son$';` |
| PostgreSQL | `~` (case-sensitive), `~*` (case-insensitive) | `SELECT * FROM users WHERE name ~ '^John';` |
| Oracle     | `REGEXP_LIKE()` function  | `SELECT * FROM employees WHERE REGEXP_LIKE(name, '^A');` |

### Coding Example

#### Basic Wildcards with `LIKE`

| Use Case                     | Query                                  | Description                          |
|------------------------------|----------------------------------------|--------------------------------------|
| Find names starting with 'A' | `SELECT * FROM users WHERE name LIKE 'A%';` | Matches names like 'Alice', 'Adam' |
| Find names with 'o' as second letter | `SELECT * FROM users WHERE name LIKE '_o%';` | Matches 'John', 'Tony' |
| Find names ending with 'son' | `SELECT * FROM users WHERE name LIKE '%son';` | Matches 'Jackson', 'Emerson' |

#### Using `REGEXP` for Advanced Matching

| Use Case                       | Query                                       | Description                          |
|--------------------------------|---------------------------------------------|--------------------------------------|
| Names starting with 'A'        | `SELECT * FROM users WHERE name REGEXP '^A';` | Matches 'Alice', 'Andrew'          |
| Names ending with 'n'          | `SELECT * FROM users WHERE name REGEXP 'n$';` | Matches 'John', 'Ethan'            |
| Names containing 'o'           | `SELECT * FROM users WHERE name REGEXP 'o';` | Matches 'John', 'Tony'             |
| Names with exactly 5 letters   | `SELECT * FROM users WHERE name REGEXP '^.{5}$';` | Matches 'James', 'David'       |
| Names containing 'a', 'b', or 'c' | `SELECT * FROM users WHERE name REGEXP '[abc]';` | Matches 'Alice', 'Bob', 'Charlie' |
| Names not containing 'x' or 'z' | `SELECT * FROM users WHERE name REGEXP '^[^xz]+$';` | Excludes 'Xavier', 'Zane'     |
| Names with double 'o'          | `SELECT * FROM users WHERE name REGEXP 'o{2}';` | Matches 'Cooper', 'Brooklyn'     |
| Emails from Gmail              | `SELECT * FROM users WHERE email REGEXP 'gmail\\.com$';` | Matches emails ending in 'gmail.com' |

#### Case-Insensitive Matching in MySQL (`BINARY` and `LOWER()` for workaround)

| Use Case                     | Query                                       | Description                          |
|------------------------------|---------------------------------------------|--------------------------------------|
| Case-insensitive match for 'john' | `SELECT * FROM users WHERE LOWER(name) REGEXP 'john';` | Matches 'John', 'john'        |
| Case-sensitive match for 'John' | `SELECT * FROM users WHERE name REGEXP BINARY 'John';` | Matches 'John', but not 'john' |

## 5. SQL Operators

| **Operator Type** | **Operator** | **Example**                              | **Description**                          |
|-------------------|--------------|------------------------------------------|------------------------------------------|
| **Arithmetic**    | `+`          | `SELECT 10 + 5;`                        | Returns `15`                            |
|                   | `-`          | `SELECT 10 - 5;`                        | Returns `5`                             |
|                   | `*`          | `SELECT 10 * 5;`                        | Returns `50`                            |
|                   | `/`          | `SELECT 10 / 5;`                        | Returns `2`                             |
|                   | `%`          | `SELECT 10 % 3;`                        | Returns `1` (remainder)                 |
| **Comparison**    | `=`          | `SELECT * FROM employees WHERE salary = 50000;` | Selects employees with a salary of 50,000 |
|                   | `!=` or `<>` | `SELECT * FROM employees WHERE age <> 30;` | Selects employees not 30 years old    |
|                   | `>`          | `SELECT * FROM products WHERE price > 100;` | Selects products priced above 100     |
|                   | `<`          | `SELECT * FROM orders WHERE quantity < 50;` | Selects orders with quantity below 50 |
|                   | `>=`         | `SELECT * FROM students WHERE marks >= 80;` | Selects students scoring 80 or above  |
|                   | `<=`         | `SELECT * FROM books WHERE pages <= 300;` | Selects books with 300 pages or less  |
| **Logical**       | `AND`        | `SELECT * FROM customers WHERE city = 'New York' AND age > 25;` | Selects customers from New York older than 25 |
|                   | `OR`         | `SELECT * FROM employees WHERE department = 'IT' OR department = 'HR';` | Selects employees in IT or HR department |
|                   | `NOT`        | `SELECT * FROM orders WHERE NOT status = 'Cancelled';` | Selects orders that are not cancelled |
| **Bitwise**       | `&`          | `SELECT 5 & 3;`                         | Returns `1` (Bitwise AND)              |
|                   | `|`          | `SELECT 5 | 3;`                         | Returns `7` (Bitwise OR)               |
|                   | `^`          | `SELECT 5 ^ 3;`                         | Returns `6` (Bitwise XOR)              |
| **Assignment**    | `:=` or `=`  | `SET @x := 10;`                        | Assigns `10` to `@x` (MySQL)           |
| **Set**           | `IN`         | `SELECT * FROM employees WHERE department IN ('HR', 'Finance');` | Selects employees in HR or Finance |
|                   | `NOT IN`     | `SELECT * FROM students WHERE class NOT IN ('10A', '10B');` | Selects students not in class 10A or 10B |
| **Pattern Matching** | `LIKE`    | `SELECT * FROM customers WHERE name LIKE 'A%';` | Selects names starting with 'A'      |
|                   | `NOT LIKE`   | `SELECT * FROM customers WHERE name NOT LIKE '%son';` | Selects names that do not end with 'son' |
| **Null Handling** | `IS NULL`    | `SELECT * FROM employees WHERE manager_id IS NULL;` | Selects employees without a manager  |
|                   | `IS NOT NULL`| `SELECT * FROM employees WHERE salary IS NOT NULL;` | Selects employees with a salary value |
| **Existence**     | `EXISTS`     | `SELECT * FROM customers WHERE EXISTS (SELECT 1 FROM orders WHERE customers.id = orders.customer_id);` | Selects customers who have placed orders |
|                   | `NOT EXISTS` | `SELECT * FROM customers WHERE NOT EXISTS (SELECT 1 FROM orders WHERE customers.id = orders.customer_id);` | Selects customers without orders |
| **Range**         | `BETWEEN`    | `SELECT * FROM products WHERE price BETWEEN 50 AND 100;` | Selects products priced between 50 and 100 |
|                   | `NOT BETWEEN`| `SELECT * FROM students WHERE marks NOT BETWEEN 40 AND 80;` | Selects students scoring outside 40-80 |
| **String Concatenation** | `CONCAT()` | `SELECT CONCAT('Hello', ' ', 'World');` (MySQL) | Returns `Hello World`              |
| **Other Special Operators** | `UNION` | `SELECT name FROM customers UNION SELECT name FROM suppliers;` | Combines unique customer and supplier names |
|                   | `UNION ALL`  | `SELECT name FROM customers UNION ALL SELECT name FROM suppliers;` | Combines customer and supplier names, including duplicates |

| Operator Type | Operator | Example                                      | Description                                  |
|---------------|----------|----------------------------------------------|----------------------------------------------|
| Logical       | `ALL`    | `SELECT * FROM Employees WHERE Salary > ALL (SELECT Salary FROM Interns);` | TRUE if all subquery values meet the condition |
| Logical       | `AND`    | `SELECT * FROM Employees WHERE Age > 30 AND Department = 'IT';` | TRUE if all conditions separated by AND are TRUE |
| Logical       | `ANY`    | `SELECT * FROM Employees WHERE Salary > ANY (SELECT Salary FROM Interns);` | TRUE if any subquery values meet the condition |
| Comparison    | `BETWEEN`| `SELECT * FROM Employees WHERE Salary BETWEEN 30000 AND 70000;` | TRUE if operand is within the range         |
| Logical       | `EXISTS` | `SELECT * FROM Employees WHERE EXISTS (SELECT 1 FROM Departments WHERE Employees.DeptID = Departments.ID);` | TRUE if subquery returns one or more records |
| Comparison    | `IN`     | `SELECT * FROM Employees WHERE Department IN ('HR', 'IT', 'Finance');` | TRUE if operand equals one in list         |
| Pattern Matching | `LIKE` | `SELECT * FROM Employees WHERE Name LIKE 'A%';` | TRUE if operand matches a pattern          |
| Logical       | `NOT`    | `SELECT * FROM Employees WHERE NOT (Department = 'HR');` | Displays record if condition(s) is NOT TRUE |
| Logical       | `OR`     | `SELECT * FROM Employees WHERE Age < 25 OR Experience > 5;` | TRUE if any conditions separated by OR are TRUE |
| Logical       | `SOME`   | `SELECT * FROM Employees WHERE Salary > SOME (SELECT Salary FROM Interns);` | TRUE if any subquery values meet the condition |

## 6. DDL (Data Definition Language)

`CREATE`, `ALTER`, `DROP`, `TRUNCATE`

### Data Definition Language (DDL) in SQL

DDL commands are used to define and modify the structure of database objects such as tables, indexes, and schemas.

### 1. CREATE – Creates a new database object (e.g., table, database, index)

#### Example: Create a Table
```sql
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    Name VARCHAR(100),
    Age INT,
    Department VARCHAR(50)
);
```

#### Example: Create a Database
```sql
CREATE DATABASE CompanyDB;
```

#### Example: Create an Index
```sql
CREATE INDEX idx_employee_name ON Employees(Name);
```

### 2. ALTER – Modifies the structure of an existing table or other database objects

#### Example: Add a Column
```sql
ALTER TABLE Employees ADD Salary DECIMAL(10,2);
```

#### Example: Modify Column Data Type
```sql
ALTER TABLE Employees MODIFY Age SMALLINT;
```

#### Example: Rename a Column
```sql
ALTER TABLE Employees RENAME COLUMN Name TO FullName;
```

#### Example: Drop a Column
```sql
ALTER TABLE Employees DROP COLUMN Department;
```

### 3. DROP – Deletes database objects permanently

#### Example: Drop a Table
```sql
DROP TABLE Employees;
```

#### Example: Drop a Database
```sql
DROP DATABASE CompanyDB;
```

#### Example: Drop an Index
```sql
DROP INDEX idx_employee_name ON Employees;
```

### 4. TRUNCATE – Removes all rows from a table without logging individual row deletions

#### Example: Truncate a Table
```sql
TRUNCATE TABLE Employees;
```

> **Note:** Unlike `DROP`, `TRUNCATE` keeps the table structure intact but deletes all records efficiently.

### 5. RENAME – Renames an existing database object

#### Example: Rename a Table
```sql
RENAME TABLE Employees TO Staff;
```

These are the core **DDL (Data Definition Language) commands** used to define and manage database structures.
```
