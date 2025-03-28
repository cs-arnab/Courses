Here’s the content converted into a properly formatted `README.md` file:

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
```

This `README.md` file is now properly formatted with Markdown syntax, including headings, tables, code blocks, and anchor links for easy navigation. You can copy this content into a file named `README.md` and use it in a GitHub repository or similar platform. Let me know if you need further adjustments!
