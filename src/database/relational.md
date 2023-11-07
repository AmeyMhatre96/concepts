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
