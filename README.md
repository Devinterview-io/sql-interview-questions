# 100 Must-Know SQL Interview Questions

<div>
<p align="center">
<a href="https://devinterview.io/questions/web-and-mobile-development/">
<img src="https://firebasestorage.googleapis.com/v0/b/dev-stack-app.appspot.com/o/github-blog-img%2Fweb-and-mobile-development-github-img.jpg?alt=media&token=1b5eeecc-c9fb-49f5-9e03-50cf2e309555" alt="web-and-mobile-development" width="100%">
</a>
</p>

#### You can also find all 100 answers here 👉 [Devinterview.io - SQL](https://devinterview.io/questions/web-and-mobile-development/sql-interview-questions)

<br>

## 1. What is _SQL_ and what is it used for?

**SQL** (**Structured Query Language**) is a domain-specific, declarative programming language designed for managing relational databases. It is the primary language for tasks like data retrieval, data manipulation, and database administration.

### Core Components

- **DDL** (Data Definition Language): Used for defining and modifying the structure of the database.
- **DML** (Data Manipulation Language): Deals with adding, modifying, and removing data in the database.
- **DCL** (Data Control Language): Manages the permissions and access rights of the database.
- **TCL** (Transaction Control Language): Governs the transactional management of the database, such as commits or rollbacks.

### Common Database Management Tasks

**Data Retrieval and Reporting**: Retrieve and analyze data, generate reports, and build dashboards.

**Data Manipulation**: Insert, update, or delete records from tables. Powerful features like Joins and Subqueries enable complex operations.

**Data Integrity**: Ensure data conform to predefined rules. Techniques like foreign keys, constraints, and triggers help maintain the integrity of the data.

**Data Security**: Manage user access permissions and roles.

**Data Consistency**: Enforce ACID properties (Atomicity, Consistency, Isolation, Durability) in database transactions.

**Data Backups and Recovery**: Perform database backups and ensure data is restorable in case of loss.

**Data Normalization**: Design databases for efficient storage and reduce data redundancy.

**Indices and Performance Tuning**: Optimize queries for faster data retrieval.

**Replication and Sharding**: Advanced techniques for distributed systems.

### Basic SQL Commands

- **CREATE DATABASE**: Used to create a new database.
- **CREATE TABLE**: Defines a new table.
- **INSERT INTO**: Adds a new record into a table.
- **SELECT**: Retrieves data from one or more tables.
- **UPDATE**: Modifies existing records.
- **DELETE**: Removes records from a table.
- **ALTER TABLE**: Modifies an existing table (e.g., adds a new column, renames an existing column, etc.).
- **DROP TABLE**: Deletes a table (along with its data) from the database.
- **INDEX**: Adds an index to a table for better performance.
- **VIEW**: Creates a virtual table that can be used for data retrieval.
- **TRIGGER**: Triggers a specified action when a database event occurs.
- **PROCEDURE** and **FUNCTION**: Store database logic for reuse and to simplify complex operations.

### Code Example: Basic SQL Queries

Here is the SQL code:

```sql
-- Create a database
CREATE DATABASE Company;

-- Use Company database
USE Company;

-- Create tables
CREATE TABLE Department (
    DeptID INT PRIMARY KEY AUTO_INCREMENT,
    DeptName VARCHAR(50) NOT NULL
);

CREATE TABLE Employee (
    EmpID INT PRIMARY KEY AUTO_INCREMENT,
    EmpName VARCHAR(100) NOT NULL,
    EmpDeptID INT,
    FOREIGN KEY (EmpDeptID) REFERENCES Department(DeptID)
);

-- Insert data
INSERT INTO Department (DeptName) VALUES ('Engineering');
INSERT INTO Department (DeptName) VALUES ('Sales');

INSERT INTO Employee (EmpName, EmpDeptID) VALUES ('John Doe', 1);
INSERT INTO Employee (EmpName, EmpDeptID) VALUES ('Jane Smith', 2);

-- Select data from database
SELECT * FROM Department;
SELECT * FROM Employee;

-- Perform an inner join to combine data from two tables
SELECT Employee.EmpID, Employee.EmpName, Department.DeptName
FROM Employee
JOIN Department ON Employee.EmpDeptID = Department.DeptID;
```
<br>

## 2. Describe the difference between _SQL_ and _NoSQL_ databases.

**SQL** and **NoSQL** databases offer different paradigms, each designed to suit various types of data and data handling.

### Top-Level Differences

- **SQL**: Primarily designed for structured (structured, semi-structured) data — data conforming to a predefined schema.
- **NoSQL**: Suited for unstructured or semi-structured data that evolves gradually, thereby supporting flexible schemas.

- **SQL**: Employs SQL (Structured Query Language) for data modification and retrieval.
- **NoSQL**: Offers various APIs (like the document and key-value store interfaces) for data operations; the use of structured query languages can vary across different NoSQL implementations.

- **SQL**: Often provides ACID (Atomicity, Consistency, Isolation, Durability) compliance to ensure data integrity.
- **NoSQL**: Databases are oftentimes optimized for high performance and horizontal scalability, with potential trade-offs in consistency.

### Common NoSQL Database Types

#### Document Stores

- **Example**: MongoDB, Couchbase
- **Key Features**: Each record is a self-contained document, typically formatted as JSON. Relationship between documents is established through embedded documents or references.
Example: Users and their blog posts could be encapsulated within a single document or linked via document references.

#### Key-Value Stores

- **Example**: Redis, Amazon DynamoDB
- **Key Features**: Data is stored as a collection of unique keys and their corresponding values. No inherent structure or schema is enforced, providing flexibility in data content.
Example: Shopping cart items keyed by a user's ID.

#### Wide-Column Stores (Column Families)

- **Example**: Apache Cassandra, HBase
- **Key Features**: Data is grouped into column families, akin to tables in traditional databases. Each column family can possess a distinct set of columns, granting a high degree of schema flexibility.
Example: User profiles, where certain users might have additional or unique attributes.

#### Graph Databases

- **Example**: Neo4j, JanusGraph
- **Key Features**: Tailored for data with complex relationships. Data entities are represented as nodes, and relationships between them are visualized as edges.
Example: A social media platform could ensure efficient friend connections management.

### Data Modeling Differences

- **SQL**: Normalization is employed to minimize data redundancies and update anomalies.
- **NoSQL**: Data is often denormalized, packaging entities together to minimize the need for multiple queries.

### Auto-Incrementing IDs

- **SQL**: Often, each entry is assigned a unique auto-incrementing ID.
- **NoSQL**: The generation of unique IDs can be driven by external systems or even specific to individual documents within a collection.

### Handling Data Relationships

- **SQL**: Relationships between different tables are established using keys (e.g., primary, foreign).
- **NoSQL**: Relationships are handled either through embedded documents, referencing techniques, or as graph-like structures in dedicated graph databases.

### Transaction Support

- **SQL**: Transactions (a series of operations that execute as a single unit) are standard.
- **NoSQL**: The concept and features of transactions can be more varied based on the specific NoSQL implementation.

### Data Consistency Levels

- **SQL**: Traditionally ensures strong consistency across the database to maintain data integrity.
- **NoSQL**: Offers various consistency models, ranging from strong consistency to eventual consistency. This flexibility enables performance optimizations in distributed environments.

### Scalability

- **SQL**: Typically scales vertically, i.e., by upgrading hardware.
- **NoSQL**: Is often designed to scale horizontally, using commodity hardware across distributed systems.

### Data Flexibility

- **SQL**: Enforces a predefined, rigid schema, making it challenging to accommodate evolving data structures.
- **NoSQL**: Supports dynamic, ad-hoc schema updates for maximum flexibility.

### Data Integrity & Validation

- **SQL**: Often relies on constraints and strict data types to ensure data integrity and validity.
- **NoSQL**: Places greater emphasis on the application layer to manage data integrity and validation.
<br>

## 3. What are the different types of _SQL commands_?

**SQL** commands fall into four primary categories: **Data Query Language** (DQL), **Data Definition Language** (DDL), **Data Manipulation Language** (DML), and **Data Control Language** (DCL).

### Data Query Language (DQL)

These commands focus on querying data within tables.

#### Keywords and Examples:

- **SELECT**: Retrieve data.
- **FROM**: Identify the source table.
- **WHERE**: Apply filtering conditions.
- **GROUP BY**: Group results based on specified fields.
- **HAVING**: Establish qualifying conditions for grouped data.
- **ORDER BY**: Arrange data based on one or more fields.
- **LIMIT**: Specify result count (sometimes replaces `SELECT TOP` for certain databases).
- **JOIN**: Bring together related data from multiple tables.

### Data Definition Language (DDL)

DDL commands are for managing the structure of the database, including tables and constraints.

#### Keywords and Examples:

- **CREATE TABLE**: Generate new tables.
- **ALTER TABLE**: Modify existing tables.
  - **ADD**, **DROP**: Incorporate or remove elements like columns, constraints, or properties.
- **CREATE INDEX**: Establish indexes to improve query performance.
- **DROP INDEX**: Remove existing indexes.
- **TRUNCATE TABLE**: Delete all rows from a table, but the table structure remains intact.
- **DROP TABLE**: Delete tables from the database.

### Data Manipulation Language (DML)

These commands are useful for handling data within tables.

#### Keywords and Examples:

- **INSERT INTO**: Add new rows of data.
  - **SELECT**: Copy data from another table or tables.
- **UPDATE**: Modify existing data in a table.
- **DELETE**: Remove rows of data from a table.

### Data Control Language (DCL)

DCL is all about managing the access and permissions to database objects.

#### Keywords and Examples:

- **GRANT**: Assign permission to specified users or roles for specific database objects.
- **REVOKE**: Withdraw or remove these permissions previously granted.
<br>

## 4. Explain the purpose of the _SELECT_ statement.

The **SELECT** statement in SQL is fundamental to data retrieval and manipulation within relational databases. Its primary role is to precisely choose, transform, and organize data per specific business requirements.

### Key Components of the SELECT Statement

The **SELECT** statement typically comprises the following elements:

- **SELECT**: Identifies the columns or expressions to be included in the result set.
- **FROM**: Specifies the table(s) from which the data should be retrieved.
- **WHERE**: Introduces conditional statements to filter rows based on specific criteria.
- **GROUP BY**: Aggregates data for summary or statistical reporting.
- **HAVING**: Functions like **WHERE**, but operates on aggregated data.
- **ORDER BY**: Defines the sort order for result sets.
- **LIMIT** or **TOP**: Limits the number of rows returned.

### Practical Applications of SELECT

The robust design of the **SELECT** statement empowers data professionals across diverse functions, enabling:

- **Data Exploration**: Gaining insights through filtered views or aggregated summaries.
- **Data Transformation**: Creating new fields via operations such as concatenation or mathematical calculations.
- **Data Validation**: Verifying data against defined criteria.
- **Data Reporting**: Generating formatted outputs for business reporting needs.
- **Data Consolidation**: Bringing together information from multiple tables or databases.
- **Data Export**: Facilitating the transfer of query results to other systems or for data backup.

Beyond these functions, proper utilization of the other components ensures efficiency and consistency working with relational databases.

### SELECT Query Example

Here is the SQL code:

```sql
SELECT 
    Orders.OrderID, 
    Customers.CustomerName, 
    Orders.OrderDate, 
    OrderDetails.UnitPrice, 
    OrderDetails.Quantity, 
    Products.ProductName, 
    Employees.LastName
FROM 
    ((Orders
    INNER JOIN Customers ON Orders.CustomerID = Customers.CustomerID)
    INNER JOIN Employees ON Orders.EmployeeID = Employees.EmployeeID)
    INNER JOIN OrderDetails ON Orders.OrderID = OrderDetails.OrderID
```
<br>

## 5. What is the difference between _WHERE_ and _HAVING_ clauses?

**WHERE** and **HAVING** clauses are both used in SQL queries to filter data, but they operate in distinct ways.

### WHERE Clause

The `WHERE` clause is primarily used to filter records before they are grouped or aggregated. It's typically employed with non-aggregated fields or raw data.

### HAVING Clause

Conversely, the `HAVING` clause filters data **after** the grouping step, often in conjunction with aggregate functions like `SUM` or `COUNT`. This makes it useful for setting group-level conditions.
<br>

## 6. Define what a _JOIN_ is in SQL and list its types.

**Join** operations in SQL are responsible for combining rows from multiple tables, primarily based on related columns that are established using a foreign key relationship.

The **three common types of joins** in SQL are:

- **Inner Join**
- **Outer Join**
  - Left Outer Join
  - Right Outer Join
  - Full Outer Join
- **Cross Join**
- **Self Join**


### Inner Join

Inner Join only returns rows where there is a match in both tables for the specified column(s).

**Visual Representation**:

```
Table1:        Table2:            Result (Inner Join):

A   B         B    C               A    B    C
-   -         -    -               -    -    -
1  aa         aa   20              1   aa   20
2  bb         bb   30              2   bb   30
3  cc         cc   40    
```

**SQL Query**:

```sql
SELECT Table1.A, Table1.B, Table2.C
FROM Table1
INNER JOIN Table2 ON Table1.B = Table2.B;
```


### Outer Join

Outer Joins—whether left, right or full—include all records from one table (the "left" or the "right" table") and matched existing records from the other table. Unmatched records are filled with NULL values for missing columns from the other table.

#### Left Outer Join

Left Outer Join (or simply Left Join) returns all records from the "left" table and the matched records from the "right" table.

**Visual Representation**:

```
Table1:        Table2:            Result (Left Outer Join):

A   B         B    C               A    B    C
-   -         -    -               -    -    -
1  aa         aa   20              1   aa   20
2  bb         bb   30              2   bb   30
3  cc         NULL  NULL            3   cc  NULL
```

**SQL Query**:

```sql
SELECT Table1.A, Table1.B, Table2.C
FROM Table1
LEFT JOIN Table2 ON Table1.B = Table2.B;
```

#### Right Outer Join

Right Outer Join (or Right Join) returns all records from the "right" table and the matched records from the "left" table.

**Visual Representation**:

```
Table1:        Table2:            Result (Right Outer Join):

A   B         B    C               A    B    C
-   -         -    -               -    -    -
1  aa         aa   20              1   aa   20
2  bb         bb   30              2   bb   30
NULL NULL      cc   40             NULL NULL  40
```

**SQL Query**:

```sql
SELECT Table1.A, Table1.B, Table2.C
FROM Table1
RIGHT JOIN Table2 ON Table1.B = Table2.B;
```


#### Full Outer Join

Full Outer Join (or Full Join) returns all records when there is a match in either the left or the right table.

**Visual Representation**:

```
Table1:        Table2:            Result (Full Outer Join):

A   B         B    C               A    B    C
-   -         -    -               -    -    -
1  aa         aa   20              1   aa   20
2  bb         bb   30              2   bb   30
3  cc         NULL  NULL            3   cc  NULL                           
NULL NULL      cc   40            NULL NULL  40
```

**SQL Query**:

```sql
SELECT COALESCE(Table1.A, Table2.A) AS A, Table1.B, Table2.C
FROM Table1
FULL JOIN Table2 ON Table1.B = Table2.B;
```


### Cross Join

A Cross Join, also known as a Cartesian Join, produces a result set that is the cartesian product of the two input sets. It will generate every possible combination of rows from both tables.

**Visual Representation**:

```
Table1:        Table2:            Result (Cross Join):

A   B         C    D               A    B    C    D
-   -         -    -               -    -    -    -
1  aa        20    X               1   aa   20   X
2  bb        30    Y               1   aa   30   Y
3  cc        40    Z               1   aa   40   Z
                                    2   bb   20   X
                                    2   bb   30   Y
                                    2   bb   40   Z
                                    3   cc   20   X
                                    3   cc   30   Y
                                    3   cc   40   Z
```

**SQL Query**:

```sql
SELECT Table1.*, Table2.*
FROM Table1
CROSS JOIN Table2;
```


### Self Join

A Self Join is when a table is joined with itself. This is used when a table has a relationship with itself, typically when it has a parent-child relationship.

**Visual Representation**:

```
Employee:                              Result (Self Join):

EmpID   Name       ManagerID       EmpID  Name     ManagerID
-       -           -               -       -          -
1      John         3               1     John        3
2      Amy          3               2     Amy         3
3      Chris       NULL              3    Chris      NULL
4      Lisa        2                4     Lisa        2
5      Mike        2                5     Mike        2
```

**SQL Query**:

```sql
SELECT E1.EmpID, E1.Name, E1.ManagerID
FROM Employee AS E1
LEFT JOIN Employee AS E2 ON E1.ManagerID = E2.EmpID;
```
<br>

## 7. What is a _primary key_ in a database?

A **primary key** in a database is a unique identifier for each record in a table.

### Key Characteristics

- **Uniqueness**: Each value in the primary key column is unique, distinguishing every record.

- **Non-Nullity**: The primary key cannot be null, ensuring data integrity.

- **Stability**: It generally does not change throughout the record's lifetime, promoting consistency.

### Data Integrity Benefits

- **Entity Distinctness**: Enforces that each record in the table represents a unique entity.

- **Association Control**: Helps manage relationships across tables and ensures referential integrity in foreign keys.

### Performance Advantages

- **Efficient Indexing**: Primary keys are often auto-indexed, making data retrieval faster.

- **Optimized Joins**: When the primary key links to a foreign key, query performance improves for related tables.

### Industry Best Practice

- **Pick a Natural Key**: Whenever possible, choose existing data values that are unique and stable.

- **Keep It Simple**: Single-column primary keys are easier to manage.

- **Avoid Data in Column Attributes**: Using data can lead to bloat, adds complexity, and can be restrictive.

- **Avoid Data Sensitivity**: Decrease potential risks associated with sensitive data by separating it from keys.

- **Evaluate Multi-Column Keys Carefully**: Identify and justify the need for such complexity.

### Code Example: Declaring a Primary Key

Here is the SQL code:

```sql
CREATE TABLE Students (
    student_id INT PRIMARY KEY,
    grade_level INT,
    first_name VARCHAR(50),
    last_name VARCHAR(50)
);
```
<br>

## 8. Explain what a _foreign key_ is and how it is used.

A **foreign key** (FK) is a column or a set of columns in a table that uniquely identifies a row or a set of rows in another table. It establishes a relationship between two tables, often referred to as the **parent table** and the **child table**.

### Key Functions of a Foreign Key

- **Data Integrity**: Assures that each entry in the referencing table has a corresponding record in the referenced table, ensuring the data's accuracy and reliability.
  
- **Relationship Mapping**: Defines logical connections between tables that can be used to retrieve related data.

- **Action Propagation**: Specify what action should be taken in the child table when a matching record in the parent table is created, updated, or deleted.

- **Cascade Control**: Allows operations like deletion or updates to propagate to related tables, maintaining data consistency.

### Foreign Key Constraints

The database ensures the following with foreign key constraints:

- **Uniqueness**: The referencing column or combination of columns in the child table is unique.
  
- **Consistency**: Each foreign key in the child table either matches a corresponding primary key or unique key in the parent table or contains a null value.

### Use Cases and Best Practices

- **Data Integrity and Consistency**: FKs ensure that references between tables are valid and up-to-date. For instance, a sales entry references a valid product ID and a customer ID.

- **Relationship Representation**: FKs depict relationships between tables, such as 'One-to-Many' (e.g., one department in a company can have multiple employees) or 'Many-to-Many' (like in associative entities).

- **Querying Simplification**: They aid in performing joined operations to retrieve related data, abstracting away complex data relationships.

### Code Example: Creating a Foreign Key Relationship

Here is the SQL code:

```sql
-- Create the parent (referenced) table first
CREATE TABLE departments (
    id INT PRIMARY KEY,
    name VARCHAR(100)
);

-- Add a foreign key reference to the child table
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    department_id INT,
    FOREIGN KEY (department_id) REFERENCES departments(id)
);
```
<br>

## 9. How can you prevent _SQL injections_?

**SQL injection** occurs when untrusted data is mixed with SQL commands. To prevent these attacks, use **parameterized queries** and input validation.

Here are specific methods to guard against SQL injection:

### Parameterized Queries

- **Description**: Also known as a prepared statement, it separates SQL code from user input, rendering direct command injection impossible.
  
- **Code Example**: 
  - Java (JDBC):

  ```java
  String query = "SELECT * FROM users WHERE username = ? AND password = ?";
  PreparedStatement ps = con.prepareStatement(query);
  ps.setString(1, username);
  ps.setString(2, password);
  ResultSet rs = ps.executeQuery();
  ```

  - Python (MySQL):

  ```python
  cursor.execute("SELECT * FROM users WHERE username = %s AND password = %s", (username, password))
  ```

- **Benefits**:
  - Improved security.
  - Reliability across different databases.
  - No need for manual escaping.

### Stored Procedures

- **Description**: Allows the database to pre-compile and store your SQL code, providing a layer of abstraction between user input and database operations.

- **Code Example**:
  - With MySQL:
    - Procedure definition:

  ```sql
  CREATE PROCEDURE login(IN p_username VARCHAR(50), IN p_password VARCHAR(50))
  BEGIN
    SELECT * FROM users WHERE username = p_username AND password = p_password;
  END
  ```

    - Calling the procedure:

  ```python
  cursor.callproc('login', (username, password))
  ```

- **Advantages**:
  - Reduction of code redundancy.
  - Allows for granular permissions.
  - Can improve performance through query plan caching.

### Input Validation

- **Description**: Examine user-supplied data to ensure it meets specific criteria before allowing it in a query.

- **Code Example**:
  Using regex:

  ```python
  if not re.match("^[A-Za-z0-9_-]*$", username):
      print("Invalid username format")
  ```

- **Drawbacks**:
  - Not a standalone method for preventing SQL injection.
  - Might introduce false positives, limiting the user's input freedom.

### Code Filtering

- **Description**: Sanitize incoming data based on its type, like strings or numbers. This approach works best in conjunction with other methods.

- **Code Example**:
  In Python:

  ```python
  username = re.sub("[^a-zA-Z0-9_-]", "", username)
  ```

- **Considerations**:
  - Still necessitates additional measures for robust security.
  - Can restrict legitimate user input.
<br>

## 10. What is _normalization_? Explain with examples.

**Normalization** is a database design method, refining table structures to reduce data redundancy and improve data integrity. It is a multi-step process, divided into five normal forms (1NF, 2NF, 3NF, BCNF, 4NF), each with specific rules.

### Normalization in Action

Let's consider a simplistic "Customer Invoices" scenario, starting from an unnormalized state:

#### Unnormalized Table (0NF)

| ID  | Name          | Invoice No.    | Invoice Date | Item No. | Description      | Quantity | Unit Price |
|----|--------------|----------------|--------------|---------|------------------|----------|-------------|
|    |              |                |              |         |                  |          |             |

In this initial state, all data is stored in a single table without structural cohesion. Each record is a mix of customer and invoice information. This can lead to data redundancy and anomalies.

#### First Normal Form (1NF)

To reach 1NF, ensure **all cells are atomic**, meaning they hold single values. Make separate tables for related groups of data. In our example, let's separate customer details from invoices and address multiple items on a single invoice.

##### Customer Details Table

| ID  | Name         |
|----|-------------|
|    |             |

##### Invoices Table

| Invoice No. | Customer_ID | Invoice Date |
|-------------|-------------|--------------|
|             |             |              |

##### Items Table

| Invoice No. | Item No. | Description | Quantity | Unit Price |
|-------------|----------|-------------|----------|------------|

Now, each table focuses on specific data, unique to 1NF.

1NF is crucial for efficient database operations, especially for tasks like reporting and maintenance.

#### Second Normal Form (2NF)

To achieve 2NF, consider the context of a complete data entry. **Each non-key column should be dependent on the whole primary key**.

In our example, the Items table already satisfies 2NF, as all non-key columns, like `Description` and `Unit Price`, depend on the entire primary key, formed by `Invoice No.` and `Item No.` together.

#### Third Normal Form (3NF)

For 3NF compliance, **there should be no transitive dependencies**. Non-key columns should rely only on the primary key.

The Invoices table requires further refinement:

##### Updated Invoices Table

| Invoice No. | Customer_ID | Invoice Date |
|-------------|-------------|--------------|
|             |             |              |

Here, `Customer_ID` is the sole attribute associated with the customer.

### Practical Implications

- Higher normal forms provide **stronger** data integrity but might be harder to maintain during regular data operations.
- Consider your specific application needs when determining the target normal form.

### Real-World Usage

- Many databases aim for 3NF.
- In scenarios requiring exhaustive data integrity, 4NF, and sometimes beyond, are appropriate.

### Code Example: Implementing 3NF

Here is the SQL code:

```sql
-- Create Customer and Invoices Table
CREATE TABLE Customers (
    ID INT PRIMARY KEY,
    Name VARCHAR(50)
);

CREATE TABLE Invoices (
    InvoiceNo INT PRIMARY KEY,
    Customer_ID INT,
    InvoiceDate DATE,
    FOREIGN KEY (Customer_ID) REFERENCES Customers(ID)
);

-- Create Items Table
CREATE TABLE Items (
    InvoiceNo INT,
    ItemNo INT,
    Description VARCHAR(100),
    Quantity INT,
    UnitPrice DECIMAL(10,2),
    PRIMARY KEY (InvoiceNo, ItemNo),
    FOREIGN KEY (InvoiceNo) REFERENCES Invoices(InvoiceNo)
);
```

This code demonstrates the specified 3NF structure with distinct tables for Customer, Invoices, and Items, ensuring data integrity during operations.
<br>

## 11. Describe the concept of _denormalization_ and when you would use it.

**Denormalization** involves optimizing database performance by reducing redundancy at the cost of some data integrity.

### Common Techniques for Denormalization

1. **Flattening Relationships**:
   - Combining related tables to minimize joins.
   - Example: `Order` and `Product` tables are merged, eliminating the many-to-many relationship.

2. **Aggregating Data**:
    -  Precomputing derived values to minimize costly calculations.
    - Example: a `Sales_Total` column in an `Order` table.

3. **Adding Additional Redundant Data**:
   -  Replicating data from one table in another to reduce the need for joins.
   - Example: The `Customer` and `Sales` tables can both have a `Country` column, even though the country is indirectly linked through the `Customer` table.

### Common Use Cases

- **Reporting and Analytics**:
   - Companies often need to run complex reports that span numerous tables.
   - Denormalization can flatten these tables, making the reporting process more efficient.

- **High-Volume Transaction Systems**:
   - In systems where data consistency can be relaxed momentarily, denormalization can speed up operations.
   - It's commonly seen in e-commerce sites where a brief delay in updating the sales figures might be acceptable for faster checkouts and improved user experience.

- **Read-Mostly Applications**:
   - Systems that are heavy on data reads and relatively light on writes can benefit from denormalization.

- **Search- and Query-Intensive Applications**:
   - For example, search engines often store data in a denormalized format to enhance retrieval speed.

- **Partitioning Data**:
   - In distributed systems like Hadoop or NoSQL databases, data is often stored redundantly across multiple nodes for enhanced performance.
   
### Considerations and Trade-offs

- **Performance vs. Consistency**:
   - Denormalization can boost performance but at the expense of data consistency.

- **Maintenance Challenges**:
   - Redundant data must be managed consistently, which can pose challenges.

- **Operational Simplicity**:
   - Sometimes, having a simple, denormalized structure can outweigh the benefits of granularity and normalization.

- **Query Flexibility**:
   - A normalized structure can be more flexible for ad-hoc queries and schema changes. Denormalized structures might require more effort to adapt to such changes.
<br>

## 12. What are _indexes_ and how can they improve query performance?

**Indexes** are essential in SQL to accelerate queries by providing quick data lookups.

### How Do Indexes Improve Performance?

- **Faster Data Retrieval**: Think of an index like a book's table of contents, which leads you right to the desired section.

- **Sorted Data Access**: With data logically ordered, lookups are more efficient.

- **Reduces Disk I/O**: Queries may read fewer data pages when using an index.

- **Enhances Joins**: Indexes help optimize join conditions, particularly in larger tables.

- **Aggregates and Uniques**: They can swiftly resolve aggregate functions and enforce data uniqueness.

### Index Types

- **B-Tree**: Standard for most databases, arranges data in a balanced tree structure.
- **Hash**: Direct lookup based on a hash of the indexed column.
- **Bitmap**: Best used for columns with a low cardinality.
- **R-Tree**: Optimized for spatial data, such as maps.

Different databases may offer additional specialized index types.

### When to Use Carefully

Excessive or unnecessary indexing can:
- **Consume Resources**: Indexes require disk space and upkeep during data modifications.
- **Slow Down Writes**: Each write operation might trigger updates to associated indexes.

### Best Practices

1. **Appropriate Index Count**: Identify crucial columns and refrain from over-indexing.
2. **Monitor and Refactor**: Regularly assess index performance and refine or remove redundant ones.
3. **Consistency**: Ensure all queries access data in a consistent manner to take full advantage of indexes.
4. **Data Type Consideration**: Certain data types are better suited for indexing than others.

### Types of Keys

- **Primary Key**: Uniquely identifies each record in a table.
- **Foreign Key**: Establishes a link between tables, enforcing referential integrity.
- **Compound Key**: Combines two or more columns to form a unique identifier.
<br>

## 13. Explain the purpose of the _GROUP BY_ clause.

The **GROUP BY** clause in SQL serves to consolidate data and perform operations across groups of records.

### Key Functions

- **Data Aggregation**: Collapses rows into summary data.
- **Filtering**: Provides filtering criteria for groups.
- **Calculated Fields**: Allows computation on group-level data.

### Usage Examples

Consider a `Sales` table with the following columns: `Product`, `Region`, and `Amount`.

#### Data Aggregation

For data aggregation, we use aggregate functions such as `SUM`, `AVG`, `COUNT`, `MIN`, or `MAX`.

The query below calculates total sales by region:

```sql
SELECT Region, SUM(Amount) AS TotalSales
FROM Sales
GROUP BY Region;
```

#### Filtering

The **GROUP BY** clause can include conditional statements. For example, to count only those sales that exceed $100 in amount:

```sql
SELECT Region, COUNT(Amount) AS SalesAbove100
FROM Sales
WHERE Amount > 100
GROUP BY Region;
```

#### Calculated Fields

You can compute derived values for groups. For instance, to find what proportion each product contributes to the overall sales in a region, use this query:

```sql
SELECT Region, Product, SUM(Amount) / (SELECT SUM(Amount) FROM Sales WHERE Region = s.Region) AS RelativeContribution
FROM Sales s
GROUP BY Region, Product;
```

### Performance Considerations

Efficient database design aims to balance query performance with storage requirements. Aggregating data during retrieval can optimize performance, especially when dealing with huge datasets.

It's essential to verify these calculations for accuracy, as improper data handling can lead to skewed results.
<br>

## 14. What is a _subquery_, and when would you use one?

**Subqueries** are embedded SQL select statements that provide inputs for an outer query. They can perform various tasks, such as filtering and aggregate computations. **Subqueries** can also be useful for complex join conditions, self-joins, and more.

### Common Subquery Types

#### Scalar Subquery

A **Scalar Subquery** returns a single value. They're frequently used for comparisons—like `>`, `=`, or `IN`.

Examples:

- Getting the **maximum** value:
  - `SELECT col1 FROM table1 WHERE col1 = (SELECT MAX(col1) FROM table1);`

- Checking existence:
  - `SELECT col1, col2 FROM table1 WHERE col1 = (SELECT col1 FROM table2 WHERE condition);`

- Using **aggregates**:
  - `SELECT col1 FROM table1 WHERE col1 = (SELECT SUM(col2) FROM table2);`

#### Table Subquery  

A **Table Subquery** is like a temporary table. It returns rows and columns and can be treated as a regular table for further processing.

Examples:

- Filtering data:
  - `SELECT * FROM table1 WHERE col1 IN (SELECT col1 FROM table2 WHERE condition);`

- Data deduplication:
  - `SELECT DISTINCT col1 FROM table1 WHERE condition1 AND col1 IN (SELECT col1 FROM table2 WHERE condition2);`


### Advantages of Using Subqueries

- **Simplicity**: They offer cleaner syntax, especially for complex queries.

- **Structured Data**: Subqueries can ensure that intermediate data is properly processed, making them ideal for multi-step tasks.

- **Reduced Code Duplication**: By encapsulating certain logic within a subquery, you can avoid repetitive code.

- **Dynamic Filtering**: The data returned by a subquery can dynamically influence the scope of the outer query.

- **Milestone Calculations**: For long and complex queries, subqueries can provide clarity and help break down the logic into manageable parts.

### Limitations and Optimization

- **Performance**: Subqueries can sometimes be less efficient. Advanced databases like Oracle, SQL Server, and PostgreSQL offer optimizations, but it's essential to monitor query performance.

- **Versatility**: While subqueries are powerful, they can be less flexible in some scenarios compared to other advanced features like Common Table Expressions (CTEs) and Window Functions.

- **Understanding and Debugging**: Nested logic might make a stored procedure or more advanced techniques like CTEs easier to follow and troubleshoot.

### Code Example: Using Subqueries

Here is the SQL code:

```sql
-- Assuming you have table1 and table2

-- Scalar Subquery Example
SELECT col1 
FROM table1 
WHERE col1 = (SELECT MAX(col1) FROM table1);

-- Table Subquery Example
SELECT col1, col2 
FROM table1 
WHERE col1 = (SELECT col1 FROM table2 WHERE condition);
```
<br>

## 15. Describe the functions of the _ORDER BY_ clause.

The **ORDER BY** clause in SQL serves to sort the result set based on specified columns, in either ascending (**ASC**, default) or descending (**DESC**) order. It's often used in conjunction with various SQL statements like **SELECT** or **UNION** to enhance result presentation.

### Key Features

- **Column-Specific Sorting**: You can designate one or more columns as the basis for sorting. For multiple columns, the order of precedence is from left to right.
- **ASC and DESC Directives**: These allow for both ascending and descending sorting. If neither is specified, it defaults to ascending.

### Use Cases

- **Top-N Queries**: Selecting a specific number of top or bottom records can be accomplished using **ORDER BY** along with **LIMIT** or **OFFSET**.
  
- **Trends Identification**: With **ORDER BY**, you can identify trends or patterns in your data, such as ranking by sales volume or time-based sequences.

- **Improved Data Presentation**: By sorting records in a logical order, you can enhance the visual appeal and comprehension of your data representations.

### Code Example: Order by Multiple Columns and Limit Results

Let's say you have a "sales" table with columns `product_name`, `sale_date`, and `units_sold`. You want to fetch the top 3 products that sold the most units on a specific date, sorted by units sold (in descending order) and product name (in ascending order).

Here is the SQL query:

```sql
SELECT product_name, sale_date, units_sold
FROM sales
WHERE sale_date = '2022-01-15'
ORDER BY units_sold DESC, product_name ASC
LIMIT 3;
```

The expected result will show the top 3 products with the highest units sold on the given date. If two products have the same number of units sold, they will be sorted in alphabetical order by their names.

### SQL Server Specific: Order by Column Position

In **SQL Server**, you can also use the column position in the ORDER BY clause. For example, instead of using column names, you can use 1 for the first column, 2 for the second, and so on. This syntax:

```sql
SELECT product_name, sale_date, units_sold
FROM sales
WHERE sale_date = '2022-01-15'
ORDER BY 3 DESC, 1 ASC
LIMIT 3;
```

performs the same operation as the previous example.

### MySQL Specific: Random Order

In **MySQL**, you can reorder the results in a random sequence. This can be useful, for instance, in a quiz app to randomize the order of questions. The **ORDER BY** clause with the **RAND()** function looks like this:

```sql
SELECT product_name
FROM products
ORDER BY RAND()
LIMIT 1;
```
<br>



#### Explore all 100 answers here 👉 [Devinterview.io - SQL](https://devinterview.io/questions/web-and-mobile-development/sql-interview-questions)

<br>

<a href="https://devinterview.io/questions/web-and-mobile-development/">
<img src="https://firebasestorage.googleapis.com/v0/b/dev-stack-app.appspot.com/o/github-blog-img%2Fweb-and-mobile-development-github-img.jpg?alt=media&token=1b5eeecc-c9fb-49f5-9e03-50cf2e309555" alt="web-and-mobile-development" width="100%">
</a>
</p>

