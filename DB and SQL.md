### **Author : Arnab Dana**

### Resource

https://www.w3schools.com/sql/default.asp

### Content

1. Category of Queries
2. Introduction
3. DQL (Data Query Language)
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

### 1. Category of Queries

In SQL, queries are categorized into different types based on the kind of operations they perform on the database. The main categories are:

| **Category** | **Full Form** | **Purpose** | **Examples** |
| --- | --- | --- | --- |
| **DDL** | Data Definition Language | Defines and modifies database structure | `CREATE`, `ALTER`, `DROP`, `TRUNCATE` |
| **DML** | Data Manipulation Language | Manipulates data within tables | `INSERT`, `UPDATE`, `DELETE`, `MERGE` |
| **DQL** | Data Query Language | Retrieves data from the database | `SELECT` |
| **DCL** | Data Control Language | Controls access to data and permissions | `GRANT`, `REVOKE` |
| **TCL** | Transaction Control Language | Manages transactions to maintain database integrity | `COMMIT`, `ROLLBACK`, `SAVEPOINT` |

### 2. Introduction

#### What is a Database?

A database is an organized collection of data that is stored and accessed electronically. It functions as a digital filing system where information is stored in a structured way, making it easy to retrieve, manage, and update.

- **Structured Storage:** Data is stored in tables with rows and columns.
- **Consistency:** Ensures uniform data storage.
- **Integrity:** Maintains data accuracy and reliability.
- **Scalability:** Can handle increasing amounts of data efficiently.

#### What is a Database Management System (DBMS)?

A Database Management System (DBMS) is software that allows users to create, manage, and interact with databases. It acts as an intermediary between the user and the database, ensuring secure and consistent data management.

#### What is a Relational Database Management System (RDBMS)?

RDBMS stores data in a structured format using tables, ensuring efficient data management through relationships (links) between tables.

Key features:

- **Tables:** Data is stored in rows and columns.
- **Primary Key:** Unique identifier for each record.
- **Foreign Key:** Establishes relationships between tables.
- **Normalization:** Reduces redundancy and improves efficiency.

Examples: MySQL, PostgreSQL, Microsoft SQL Server, Oracle Database.

#### What is SQL?

SQL (Structured Query Language) is a programming language used to manage relational databases.

Key components:

- **DQL:** Querying data (`SELECT`).
- **DML:** Data manipulation (`INSERT`, `UPDATE`, `DELETE`).
- **DDL:** Database structure management (`CREATE`, `ALTER`, `DROP`).
- **DCL:** Access control (`GRANT`, `REVOKE`).
- **TCL:** Transaction management (`COMMIT`, `ROLLBACK`).

---

### 3. **DQL (Data Query Language)**

#### **Basic Queries**

```sql
SELECT * FROM Customers; -- Select all columns
SELECT CustomerName, City FROM Customers; -- Select specific columns
```

#### **DISTINCT**

```sql
SELECT DISTINCT Country FROM Customers;
SELECT COUNT(DISTINCT column_name) AS DistinctCountries FROM table_name;
```

#### **WHERE Clause**

```sql
SELECT * FROM Customers WHERE Country='Mexico';
```

#### **ORDER BY**

```sql
SELECT * FROM Products ORDER BY Price;
SELECT * FROM Customers ORDER BY Country ASC, CustomerName DESC;
```

#### **TOP / LIMIT / FETCH FIRST**

```sql
-- Get top 5 highest-paid employees
SELECT TOP 5 * FROM Employees ORDER BY Salary DESC;
-- Get top 10% of employees
SELECT TOP 10 PERCENT * FROM Employees ORDER BY Salary DESC;
-- Get rows 5 to 10 (Pagination)
SELECT * FROM Employees ORDER BY EmployeeID LIMIT 5 OFFSET 5;
```

#### **Alias**

```sql
SELECT COUNT(*) AS [Number of records] FROM Products;
```

#### **GROUP BY & HAVING**

```sql
SELECT COUNT(CustomerID), Country FROM Customers GROUP BY Country HAVING COUNT(CustomerID) > 5 ORDER BY COUNT(CustomerID) DESC;
```

#### **EXISTS**

```sql
SELECT column_name(s) FROM table_name WHERE EXISTS (SELECT column_name FROM table_name WHERE condition);
```

#### **SELECT INTO**

```sql
-- Copy data into a new table
SELECT * INTO CustomersBackup2017 FROM Customers;
```

#### **CASE Expression**

```sql
SELECT OrderID, Quantity,
CASE
    WHEN Quantity > 30 THEN 'High'
    WHEN Quantity = 30 THEN 'Medium'
    ELSE 'Low'
END AS QuantityCategory
FROM OrderDetails;
```

---

### 4. Regex in SQL

SQL supports **regular expressions (regex)** in MySQL, PostgreSQL, and Oracle for advanced pattern matching.

#### **Basic Wildcards (`LIKE` Operator)**

| Symbol | Description | Example |
| --- | --- | --- |
| `%` | Matches zero or more characters | `WHERE name LIKE 'A%'` (Names starting with 'A') |
| `_` | Matches a single character | `WHERE name LIKE 'J_n'` (Matches 'Jon', 'Jan', etc.) |

#### **Regex Patterns (`REGEXP`)**

| Pattern | Description | Example |
| --- | --- | --- |
| `^` | Start of string | `WHERE name REGEXP '^A'` (Starts with 'A') |
| `$` | End of string | `WHERE email REGEXP 'gmail.com$'` (Ends with 'gmail.com') |
| `[abc]` | Matches any character in brackets | `WHERE name REGEXP '[JKT]ohn'` |

#### **SQL-Specific Regex Usage**

| Database | Regex Support | Example |
| --- | --- | --- |
| MySQL | `REGEXP` operator | `SELECT * FROM users WHERE name REGEXP '^[A-Z].*son$';` |
| PostgreSQL | `~` (case-sensitive), `~*` (case-insensitive) | `SELECT * FROM users WHERE name ~ '^John';` |
| Oracle | `REGEXP_LIKE()` function | `SELECT * FROM employees WHERE REGEXP_LIKE(name, '^A');` |

---
