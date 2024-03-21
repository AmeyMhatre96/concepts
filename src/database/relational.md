[Top Q/A](https://www.datacamp.com/blog/top-sql-interview-questions-and-answers-for-beginners-and-intermediate-practitioners)

## SQL Subqueries

Subqueries, also known as subselects or nested queries, are queries that are embedded within another SQL query. They are used to retrieve data that will be used in the main query's condition or to provide additional information. There are several types of subqueries in SQL, including:

1. **Scalar Subquery:**
   - A scalar subquery returns a single value and can be used in a comparison or expression.
   - Example: Find all employees whose salary is greater than the average salary.
     ```sql
     SELECT employee_name
     FROM employees
     WHERE salary > (SELECT AVG(salary) FROM employees);
     ```

2. **Single-Row Subquery:**
   - A single-row subquery returns a single row of data. It can be used in a comparison to filter rows based on the result.
   - Example: Find the department with the highest average salary.
     ```sql
     SELECT department_name
     FROM departments
     WHERE department_id = (SELECT department_id FROM employees GROUP BY department_id HAVING AVG(salary) = MAX(AVG(salary)));
     ```

3. **Multi-Row Subquery:**
   - A multi-row subquery returns multiple rows, and it can be used in operations involving sets of data.
   - Example: Find all employees who belong to departments with more than 10 employees.
     ```sql
     SELECT employee_name
     FROM employees
     WHERE department_id IN (SELECT department_id FROM employees GROUP BY department_id HAVING COUNT(*) > 10);
     ```

4. **Correlated Subquery:**
   - A correlated subquery refers to a column in the outer query, and its result depends on the row being evaluated in the main query.
   - Example: Find all employees whose salary is greater than the average salary in their department.
     ```sql
     SELECT employee_name
     FROM employees e
     WHERE salary > (SELECT AVG(salary) FROM employees WHERE department_id = e.department_id);
     ```

5. **Table Subquery (Inline View):**
   - A table subquery returns a result set that can be treated as a table within the main query.
   - Example: Find the department names and the employees in each department with their salaries.
     ```sql
     SELECT d.department_name, e.employee_name, e.salary
     FROM departments d
     JOIN (SELECT * FROM employees) e ON d.department_id = e.department_id;
     ```

6. **Existence Subquery:**
   - An existence subquery is used to check for the existence of rows that meet certain criteria.
   - Example: Find all departments that have at least one employee.
     ```sql
     SELECT department_name
     FROM departments d
     WHERE EXISTS (SELECT 1 FROM employees e WHERE d.department_id = e.department_id);
     ```

7. **Correlated Existence Subquery:**
   - A correlated existence subquery checks for the existence of rows based on the values in the outer query.
   - Example: Find all employees whose salary is not the highest in their department.
     ```sql
     SELECT employee_name
     FROM employees e
     WHERE NOT EXISTS (SELECT 1 FROM employees WHERE department_id = e.department_id AND salary > e.salary);
     ```

## SQL Constraints

In SQL, constraints are used to enforce rules and restrictions on data in database tables. Constraints ensure data integrity and help maintain the consistency and accuracy of the data. You can add constraints to tables during the table creation (using the `CREATE TABLE` statement) or alter an existing table (using the `ALTER TABLE` statement).

Here are some common constraints and how to add them:

1. **Primary Key Constraint:**
   - A primary key constraint ensures that a column or a set of columns uniquely identifies each row in a table.
   - Example:
     ```sql
     CREATE TABLE Employees (
         EmployeeID INT PRIMARY KEY,
         FirstName VARCHAR(50),
         LastName VARCHAR(50)
     );
     ```

2. **Foreign Key Constraint:**
   - A foreign key constraint establishes a relationship between two tables, ensuring that values in one table's column match values in another table's primary key.
   - Example:
     ```sql
     CREATE TABLE Orders (
         OrderID INT PRIMARY KEY,
         CustomerID INT,
         OrderDate DATE,
         FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
     );
     ```

3. **Unique Constraint:**
   - A unique constraint ensures that all values in a column or a set of columns are unique, but it doesn't have to be the primary key.
   - Example:
     ```sql
     CREATE TABLE Products (
         ProductID INT PRIMARY KEY,
         ProductName VARCHAR(50) UNIQUE,
         Price DECIMAL(10, 2)
     );
     ```

4. **Check Constraint:**
   - A check constraint enforces a condition on the values that can be inserted into a column.
   - Example:
     ```sql
     CREATE TABLE Students (
         StudentID INT PRIMARY KEY,
         Age INT,
         CONSTRAINT CheckAge CHECK (Age >= 18)
     );
     ```

5. **Not Null Constraint:**
   - A not null constraint ensures that a column cannot have NULL values.
   - Example:
     ```sql
     CREATE TABLE Customers (
         CustomerID INT PRIMARY KEY,
         FirstName VARCHAR(50) NOT NULL,
         LastName VARCHAR(50) NOT NULL
     );
     ```

6. **Default Constraint:**
   - A default constraint specifies a default value for a column when no value is provided during an insert operation.
   - Example:
     ```sql
     CREATE TABLE Orders (
         OrderID INT PRIMARY KEY,
         OrderDate DATE DEFAULT GETDATE(),
         CustomerID INT
     );
     ```

To add constraints to an existing table, you can use the `ALTER TABLE` statement. For example, to add a unique constraint to an existing column, you can do the following:

```sql
ALTER TABLE YourTable
ADD CONSTRAINT UniqueConstraintName UNIQUE (ColumnName);
```

Make sure to replace `YourTable`, `UniqueConstraintName`, and `ColumnName` with the appropriate table name, constraint name, and column name.


## SQL Joins

In SQL, joins are used to retrieve data from multiple tables based on a related column between them. Joins allow you to combine data from different tables into a single result set. There are several types of joins, including inner join, left join (or left outer join), right join (or right outer join), and full outer join. Here are examples of each type of join:

Suppose we have two tables: `Customers` and `Orders`.

**Customers Table:**

| CustomerID | CustomerName | ContactName | Country  |
|------------|--------------|-------------|----------|
| 1          | Customer A   | John        | USA      |
| 2          | Customer B   | Jane        | UK       |
| 3          | Customer C   | Bob         | France   |

**Orders Table:**

| OrderID | CustomerID | OrderDate  |
|---------|------------|------------|
| 101     | 1          | 2023-01-15 |
| 102     | 2          | 2023-01-16 |
| 103     | 1          | 2023-01-17 |

Now, let's perform various types of joins on these tables:

1. **Inner Join:**
   - An inner join returns only the rows that have matching values in both tables.
   - Example: Retrieve all orders and their associated customer details.
     ```sql
     SELECT Orders.OrderID, Customers.CustomerName, Orders.OrderDate
     FROM Orders
     INNER JOIN Customers ON Orders.CustomerID = Customers.CustomerID;
     ```

2. **Left Join (Left Outer Join):**
   - A left join returns all rows from the left table and the matched rows from the right table. If there are no matches in the right table, NULL values are returned.
   - Example: Retrieve all customers and their associated orders (including customers with no orders).
     ```sql
     SELECT Customers.CustomerName, Orders.OrderID, Orders.OrderDate
     FROM Customers
     LEFT JOIN Orders ON Customers.CustomerID = Orders.CustomerID;
     ```

3. **Right Join (Right Outer Join):**
   - A right join returns all rows from the right table and the matched rows from the left table. If there are no matches in the left table, NULL values are returned.
   - Example: Retrieve all orders and their associated customer details (including orders with no matching customers).
     ```sql
     SELECT Orders.OrderID, Customers.CustomerName, Orders.OrderDate
     FROM Orders
     RIGHT JOIN Customers ON Orders.CustomerID = Customers.CustomerID;
     ```

4. **Full Outer Join:**
   - A full outer join returns all rows when there is a match in either the left or right table. If there is no match, NULL values are returned.
   - Example: Retrieve all customers and their associated orders, including unmatched customers and orders.
     ```sql
     SELECT Customers.CustomerName, Orders.OrderID, Orders.OrderDate
     FROM Customers
     FULL OUTER JOIN Orders ON Customers.CustomerID = Orders.CustomerID;
     ```

## SQL Languages

SQL (Structured Query Language) is a domain-specific language used for managing and manipulating relational databases. It allows you to perform a wide range of operations on structured data, such as querying, inserting, updating, and deleting data. SQL is not a single language; it includes several sub-languages and commands. Here are some key SQL sub-languages and commands:

1. **Data Query Language (DQL):**
   - DQL is used to query and retrieve data from a database.
   - Primary command: `SELECT`
   - Example: Retrieve all records from a table named `Customers`.
     ```sql
     SELECT * FROM Customers;
     ```

2. **Data Definition Language (DDL):**
   - DDL is used to define and manage the structure of a database, including tables, indexes, and constraints.
   - Primary commands: `CREATE`, `ALTER`, `DROP`
   - Example: Create a new table named `Products`.
     ```sql
     CREATE TABLE Products (
         ProductID INT PRIMARY KEY,
         ProductName VARCHAR(255),
         Price DECIMAL(10, 2)
     );
     ```

3. **Data Manipulation Language (DML):**
   - DML is used to manipulate data within a database, including inserting, updating, and deleting records.
   - Primary commands: `INSERT`, `UPDATE`, `DELETE`
   - Example: Insert a new record into the `Customers` table.
     ```sql
     INSERT INTO Customers (CustomerName, ContactName, Country)
     VALUES ('New Customer', 'John Doe', 'USA');
     ```

4. **Data Control Language (DCL):**
   - DCL is used to control access to the data and database security.
   - Primary commands: `GRANT`, `REVOKE`
   - Example: Grant SELECT privileges on a table to a user.
     ```sql
     GRANT SELECT ON Customers TO User123;
     ```

5. **Transaction Control Language (TCL):**
   - TCL is used to control transactions and ensure data consistency.
   - Primary commands: `COMMIT`, `ROLLBACK`, `SAVEPOINT`
   - Example: Commit a transaction to save changes to the database.
     ```sql
     COMMIT;
     ```

6. **Data Query Language Extensions:**
   - Some SQL databases provide extensions or specialized commands to enhance querying capabilities. For example, Microsoft SQL Server uses `TOP`, Oracle uses `ROWNUM`, and PostgreSQL uses `LIMIT` for limiting query results.

7. **Vendor-Specific SQL:**
   - Different database management systems (DBMS) may introduce their own extensions or variations to SQL. For example, Microsoft SQL Server uses `T-SQL`, Oracle has `PL/SQL`, and MySQL has its own extensions.


## Views 

A view is a virtual table based on the result set of a SQL statement. It is stored in the database and can be used like a regular table. Views are useful for simplifying complex queries and hiding the underlying table structure. They can also be used to restrict access to sensitive data. Views can be created using the `CREATE VIEW` statement. For example, to create a view named `CustomersView` that contains the `CustomerID` and `CustomerName` columns from the `Customers` table, you can do the following:

```sql

CREATE VIEW CustomersView AS

SELECT CustomerID, CustomerName
FROM Customers;
```

You can then query the view like a regular table:

```sql
SELECT * FROM CustomersView;
```   
### Types of Views

- Materialized Views
  Materialized views are views that are stored in the database and updated periodically. They are useful for improving query performance by pre-computing expensive queries and storing the results in a table.

- Non-Materialized
  Non materialized views are views that are not stored in the database and are created on the fly when they are queried. They are useful for simplifying complex queries and hiding the underlying table structure. 


## SQL Indexes

An index is a data structure that improves the performance of data retrieval operations on a database table. It is used to quickly locate rows in a table based on the values in one or more columns. Indexes are created using the `CREATE INDEX` statement. For example, to create an index named `CustomerNameIndex` on the `CustomerName` column of the `Customers` table, you can do the following:

```sql
CREATE INDEX CustomerNameIndex ON Customers (CustomerName);
```
### Types of Indexes

- Clustered Index
  A clustered index is an index that determines the physical order of the rows in a table. It is created on the primary key column by default, but you can also create it on other columns. A table can only have one clustered index.

- Non-Clustered Index
   A non-clustered index is an index that does not determine the physical order of the rows in a table. It is created on a column or a set of columns that are not the primary key. A table can have multiple non-clustered indexes.

- Multi-Column Index
  A multi-column index is an index that is created on multiple columns. It is useful for queries that involve multiple columns.

Choosing the right type of database index is crucial for optimizing database performance. The choice of index depends on the specific use case, the types of queries you run, and the characteristics of your data. Here are some guidelines for when to use different types of database indexes:

1. **Primary Key Index:**
   - Use a primary key index for columns that uniquely identify each row in a table. Typically, this index is automatically created for primary key columns.
   - Use it when you need to enforce data integrity through unique constraints.

2. **Unique Index:**
   - Use a unique index for columns that must contain unique values, but are not the primary key.
   - Use it to enforce uniqueness constraints on non-primary key columns.

3. **Non-Unique Index:**
   - Use a non-unique index for columns that you frequently search, join, or filter in queries.
   - Use it for columns that have a relatively high cardinality, meaning they have many distinct values.

4. **Composite Index (Multi-Column Index):**
   - Use a composite index for queries that involve multiple columns. This is especially useful for filtering or searching on multiple columns in a single query.
   - Order the columns in the index based on query patterns; the order matters.

5. **Full-Text Index:**
   - Use a full-text index for columns containing textual data (e.g., descriptions, articles, or product names) when you need to perform full-text search operations.
   - Use it to improve the efficiency of text-based searching.

6. **Spatial Index:**
   - Use a spatial index for geographic or location-based data when you need to perform spatial queries, such as finding nearby points or regions.
   - Use it to optimize queries involving geographical data.

7. **Bitmap Index:**
   - Use a bitmap index for columns with low cardinality, like boolean columns or gender columns.
   - Use it when you have very specific queries that involve multiple boolean or categorical filters.

8. **Hash Index:**
   - Use a hash index for specific use cases, such as when you need to hash and index large amounts of data, and exact matches are important.
   - Use it when dealing with scenarios like hash-based partitioning.

9. **Clustered Index:**
   - Use a clustered index for the primary key of a table. This determines the physical order of data rows in the table.
   - Use it for tables that you frequently search, join, or retrieve data from.

10. **Covering Index (Index with Included Columns):**
    - Use a covering index to include non-key columns in the index, which can eliminate the need to access the base table for specific queries.
    - Use it to improve query performance and reduce I/O operations.

11. **Functional Index:**
    - Use a functional index when you need to index the result of a function applied to a column, such as indexing the lowercase version of a string column for case-insensitive searches.
    - Use it to optimize queries involving calculated or transformed values.

12. **Partial Index:**
    - Use a partial index to index only a subset of rows in a table based on a condition.
    - Use it when you have a large table, but only need to index a portion of the data for specific queries.


## Normalization

Normalization is the process of organizing data in a database to reduce data redundancy and improve data integrity. It involves breaking up a table into multiple tables and defining relationships between them. Normalization is important because it helps reduce data redundancy and improve data integrity. It also makes it easier to maintain and update the database.

There are several normal forms, each with its own set of rules. The most common normal forms are:

1. **First Normal Form (1NF):**
   - A table is in 1NF if it has no repeating groups (arrays or lists) and all its attributes contain atomic (indivisible) values.
   - Ensure that each column contains a single value, and there are no arrays or lists.
  
   | CustomerID | CustomerName | Phone       | Salary      |
   |------------|--------------|-------------| ----------- |
   | 1          | Customer A   | 123-456-788, 123-456-789 | 1000 |
   | 2          | Customer B   | 987-654-321 | 2000 |

   - To convert the above table to 1NF, we need to split the `Phone` column into two separate rows.

   | CustomerID | CustomerName | Phone       | Salary      |
   |------------|--------------|-------------| ----------- |
   | 1          | Customer A   | 123-456-788 | 1000 |
   | 1          | Customer A   | 123-456-789 | 1000 |
   | 2          | Customer B   | 987-654-321 | 2000 |


2. **Second Normal Form (2NF):**

   - A table is in 2NF if it is in 1NF and all non-key columns are fully dependent on the primary key.
   - Example: The following table is not in 2NF because the `Price` column is not fully dependent on the primary key.
  
     | ProductID | ProductName | CategoryID | CategoryName | Price |
     |-----------|-------------|------------|--------------|-------|
     | 1         | Product A   | 1          | Category A   | 10    |
     | 2         | Product B   | 2          | Category B   | 20    |