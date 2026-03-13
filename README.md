# 100 Must-Know SQL Interview Questions in 2026

<div>
<p align="center">
<a href="https://devinterview.io/questions/web-and-mobile-development/">
<img src="https://firebasestorage.googleapis.com/v0/b/dev-stack-app.appspot.com/o/github-blog-img%2Fweb-and-mobile-development-github-img.jpg?alt=media&token=1b5eeecc-c9fb-49f5-9e03-50cf2e309555" alt="web-and-mobile-development" width="100%">
</a>
</p>

#### You can also find all 100 answers here 👉 [Devinterview.io - SQL](https://devinterview.io/questions/web-and-mobile-development/sql-interview-questions)

<br>

## 1. What is _SQL_ and what is it used for?

### **SQL (Structured Query Language)**

**SQL** is the standardized domain-specific, declarative language for managing and querying **Relational Database Management Systems (RDBMS)**. Beyond legacy relational models, modern SQL dialects (e.g., PostgreSQL 18, DuckDB 1.2) now incorporate support for semi-structured data (JSONB) and vector embeddings for **RAG (Retrieval-Augmented Generation)** workflows.

---

### **Core Components**

*   **DDL (Data Definition Language):** Defines schema objects (e.g., `CREATE`, `ALTER`, `DROP`).
*   **DML (Data Manipulation Language):** Manages row-level data (e.g., `INSERT`, `UPDATE`, `DELETE`, `MERGE`).
*   **DCL (Data Control Language):** Manages authorization and security (e.g., `GRANT`, `REVOKE`).
*   **TCL (Transaction Control Language):** Ensures state consistency (e.g., `COMMIT`, `ROLLBACK`, `SAVEPOINT`).
*   **DQL (Data Query Language):** The subset focused on retrieval (e.g., `SELECT`).

---

### **Modern Database Management Tasks**

*   **Data Retrieval:** Complex aggregation and window functions for analytics.
*   **ACID Compliance:** Ensures **Atomicity, Consistency, Isolation, and Durability** in high-concurrency environments.
*   **Vector Search:** 2026 standard databases (e.g., `pgvector`) utilize SQL extensions to perform $k$-nearest neighbor ($k$-NN) searches on high-dimensional vectors, enabling AI-driven semantic similarity queries.
*   **Normalization & Optimization:** Usage of B-Tree, LSM-Tree, and BRIN indices to achieve query complexity of $O(\log n)$ for point lookups.
*   **Distributed Scaling:** Leveraging **Sharding** (horizontal partitioning) and **Replication** (read-replicas) to manage multi-terabyte datasets.

---

### **Essential SQL Commands**

*   **SELECT:** Primary data retrieval; supports **Common Table Expressions (CTEs)** and window functions (`OVER`, `PARTITION BY`).
*   **MERGE:** An upsert operation (INSERT or UPDATE) that minimizes round-trips to the server.
*   **LATERAL JOIN:** Allows subqueries to reference preceding tables in the `FROM` clause, critical for complex analytical transformations.
*   **MATERIALIZED VIEW:** Caches the result of a complex query; refreshes asynchronously for high-performance reporting.

---

### **Code Example: Modern SQL Syntax**

The following example demonstrates modern syntax, including standard **CTEs** and relational constraints.

```sql
-- Schema Definition
CREATE TABLE Department (
    dept_id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    dept_name VARCHAR(100) NOT NULL
);

CREATE TABLE Employee (
    emp_id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    emp_name VARCHAR(255) NOT NULL,
    dept_id INT REFERENCES Department(dept_id)
);

-- Recursive/Complex Query using CTE
WITH DepartmentStats AS (
    SELECT dept_id, COUNT(*) as emp_count
    FROM Employee
    GROUP BY dept_id
)
SELECT 
    e.emp_name, 
    d.dept_name,
    ds.emp_count
FROM Employee e
JOIN Department d ON e.dept_id = d.dept_id
JOIN DepartmentStats ds ON d.dept_id = ds.dept_id
WHERE ds.emp_count > 0;
```

---

### **2026 Performance Considerations**

1.  **Index Scan vs. Seq Scan:** Query planners choose indices based on cardinality and selectivity to avoid $O(n)$ full table scans.
2.  **Execution Plans:** Use `EXPLAIN ANALYZE` to inspect the query execution tree and identify high-cost nodes.
3.  **Concurrency:** In 2026 architectures, **MVCC (Multi-Version Concurrency Control)** is standard to ensure that readers do not block writers, maximizing throughput.
<br>

## 2. Describe the difference between _SQL_ and _NoSQL_ databases.

### Architectural Distinctions: SQL vs. NoSQL (2026 Audit)

The dichotomy between Relational Database Management Systems (**RDBMS/SQL**) and Non-Relational (**NoSQL**) systems has matured into a hybrid landscape. While fundamental constraints remain, modern distributed systems have blurred the lines via multi-model support.

### Fundamental Divergence

*   **SQL (Relational)**: Built on the Relational Model (Codd, 1970). Data is organized in tables with rigid schemas. Optimized for **ACID** compliance and complex relational algebra.
*   **NoSQL (Non-Relational)**: Optimized for horizontal scaling, high throughput, and varied data structures. Architecture typically follows the **CAP Theorem** (Consistency, Availability, Partition Tolerance), often favoring AP (Availability/Partition Tolerance) and **Eventual Consistency**.

### 2026 Paradigm Shifts

*   **Hybridization**: Modern RDBMS (e.g., PostgreSQL 18+) now natively support JSONB, enabling semi-structured data handling within ACID-compliant environments. Conversely, many NoSQL stores (e.g., MongoDB 8.0+) now support multi-document **ACID transactions**.
*   **Scalability**: SQL is no longer strictly "vertical." Distributed SQL engines (e.g., CockroachDB, TiDB, YugabyteDB) bring horizontal sharding and global replication to the SQL standard, rendering the "SQL=Vertical/NoSQL=Horizontal" heuristic increasingly legacy.

### Taxonomy of NoSQL Implementations

#### Document Stores
*   **Mechanism**: Stores data as BSON/JSON binary documents.
*   **2026 Context**: Integration of vector search capabilities (e.g., MongoDB Atlas Vector Search) for **RAG** (Retrieval-Augmented Generation) workflows.

#### Key-Value Stores
*   **Mechanism**: Partitioned hash tables.
*   **Use Case**: Sub-millisecond latency for session management, caching, and feature stores in ML pipelines. 
*   **Performance**: $O(1)$ lookup complexity.

#### Wide-Column Stores
*   **Mechanism**: Sparse, multidimensional sorted maps.
*   **Architecture**: Optimized for write-heavy workloads and time-series data at exabyte scale.

#### Graph Databases
*   **Mechanism**: Index-free adjacency (nodes and edges).
*   **2026 Context**: Critical for **Knowledge Graph** construction and complex relationship inference in LLM orchestration.

### Technical Comparison Matrix

| Feature | SQL (Modernized) | NoSQL |
| :--- | :--- | :--- |
| **Schema** | Schema-on-write | Schema-on-read |
| **Integrity** | Enforcement via constraints/FKs | Application-layer validation |
| **Joins** | Efficient via relational algebra | Often discouraged/denormalized |
| **Scaling** | Vertical/Distributed SQL (Horizontal) | Native Horizontal (Sharding) |
| **Querying** | Declarative (SQL Standard) | Proprietary API / GraphQL / SQL-like |

### Data Modeling & Integrity

*   **Normalization vs. Denormalization**: In 2026, storage is cheap, but compute and network latency are not. SQL still defaults to 3NF (Third Normal Form) to eliminate update anomalies. NoSQL favors **denormalization** to ensure that a single request can retrieve all required data, avoiding expensive cross-node joins (which carry $O(log N)$ to $O(N)$ overhead depending on indexing).
*   **ACID Compliance**: The traditional view that NoSQL sacrifices ACID is outdated. Most enterprise-grade NoSQL solutions now provide tunable consistency, allowing developers to opt-in to strong consistency at the cost of latency.

### Transactional & Consistency Models

*   **SQL**: Employs **Two-Phase Commit (2PC)** or **Paxos/Raft** protocols in distributed versions to guarantee serializability.
*   **NoSQL**: Leverages **Vector Clocks** or **Last-Write-Wins (LWW)** conflict resolution in AP systems. Engineers must explicitly manage idempotency at the application level when eventual consistency is utilized.

### Architectural Recommendation (2026)
Select **SQL** when data integrity, complex transactional reporting, and strict schema enforcement are paramount. Select **NoSQL** for high-velocity streaming data, sparse datasets (e.g., IoT logs), or when the schema must evolve iteratively without database-level downtime. Consider **Distributed SQL** if the project requires the familiarity of SQL with the elastic scalability of NoSQL.
<br>

## 3. What are the different types of _SQL commands_?

### SQL Command Classification (2026 Audit)

Modern SQL classification includes a fifth critical category: **Transaction Control Language (TCL)**, which handles atomic state transitions. **DQL** is now standardly recognized as a subset of **DML** in formal SQL:2023/2025 specifications, though categorized separately for pedagogical clarity.

### Data Query Language (DQL)

Focused on data retrieval. Modern analytical engines prioritize set-based operations and window functions.

#### Keywords and Operations:
- **SELECT**: Projects data from relations.
- **FROM**: Identifies data sources (Tables, CTEs, Subqueries).
- **WHERE**: Boolean filtering predicates.
- **GROUP BY**: Aggregation grouping.
- **HAVING**: Post-aggregation filtering.
- **WINDOW FUNCTIONS**: (e.g., `OVER()`, `PARTITION BY`) perform calculations across related rows.
- **JOIN**: Relational algebra combining datasets ($Inner, Left, Right, Full, Cross$).
- **CTE (WITH)**: Recursive or non-recursive temporary result sets for improved query readability and modularity.

### Data Definition Language (DDL)

Manages schema evolution and metadata persistence.

#### Keywords and Operations:
- **CREATE**: Defines schemas, tables, indexes, or stored procedures.
- **ALTER**: Modifies structural definitions (e.g., `ADD COLUMN`, `RENAME TO`, `SET DATA TYPE`).
- **DROP**: Removes schema objects.
- **TRUNCATE**: Resets table state (DML-like impact, DDL-metadata overhead).
- **COMMENT**: Annotates objects for documentation as code (IaC) compliance.

### Data Manipulation Language (DML)

Handles row-level operations. 2026 standards emphasize "Upsert" patterns and atomic modifications.

#### Keywords and Operations:
- **INSERT**: Populates rows. Includes `ON CONFLICT` (PostgreSQL) or `MERGE` (SQL Standard) for idempotent data ingestion.
- **UPDATE**: Modifies existing row state.
- **DELETE**: Removes rows.
- **MERGE**: Synchronizes source and target tables; the preferred 2026 standard for ETL/ELT pipelines to maintain $O(n)$ complexity during synchronization.

### Transaction Control Language (TCL)

Governs the state of transactions to ensure **ACID** properties.

#### Keywords and Operations:
- **COMMIT**: Persists all changes within a transaction to disk.
- **ROLLBACK**: Reverts state to the last checkpoint upon failure.
- **SAVEPOINT**: Defines checkpoints within a transaction, enabling partial rollback ($O(1)$ state revert).

### Data Control Language (DCL)

Governs security and governance via **RBAC** (Role-Based Access Control).

#### Keywords and Operations:
- **GRANT**: Assigns specific privileges (`SELECT`, `INSERT`, `EXECUTE`) to users/roles.
- **REVOKE**: Removes previously assigned privileges.
- **DENY**: Explicitly restricts access, overriding implicit permissions (provider-specific, e.g., T-SQL).
<br>

## 4. Explain the purpose of the _SELECT_ statement.

### The SQL SELECT Statement (2026 Audit)

The **SELECT** statement is the primary Data Query Language (DQL) construct in SQL, designed for retrieving, projecting, and transforming data from relational structures. In modern architectures, it serves as the interface between storage engines and application layers, supporting complex analytical processing and vector-relational hybrid queries.

### Logical Order of Execution

The **SELECT** statement is evaluated by the database engine in a specific logical sequence, distinct from the written syntax order:

1. **FROM / JOIN**: Determines the source data set.
2. **WHERE**: Applies predicate filtering.
3. **GROUP BY**: Partitions the data into summary sets.
4. **HAVING**: Filters aggregated result sets.
5. **SELECT**: Evaluates expressions and projects columns.
6. **DISTINCT**: Removes duplicate rows.
7. **ORDER BY**: Defines the final presentation sequence.
8. **LIMIT / OFFSET**: Constrains the final result set volume.

### Evolution and 2026 Standards

Modern SQL engines (e.g., PostgreSQL 18, DuckDB 1.2) extend traditional **SELECT** capabilities to support **JSONB** traversal, **Vector embeddings** (via extensions like `pgvector`), and **Window Functions**.

- **Vector Proximity Search**: Modern **SELECT** statements now frequently involve distance functions (e.g., `<=>` for Cosine distance) to query high-dimensional embeddings:
  `SELECT content FROM docs ORDER BY embedding <=> '[...]' LIMIT 5;`
- **CTEs (Common Table Expressions)**: The `WITH` clause is now standard for improving query readability and recursion over subqueries.
- **Window Functions**: Replacing many traditional self-joins with `OVER (PARTITION BY ...)` for performant ranking and running totals at $O(n \log n)$ complexity.

### Practical Applications

- **Relational Integrity Exploration**: Validating constraints across normalized schemas.
- **Complex Transformation**: Utilizing `CASE` statements or `COALESCE` for business logic injection.
- **Analytical Processing (OLAP)**: Leveraging window functions to perform time-series analysis without destructive row grouping.
- **Integration**: Providing structured outputs (often `JSON_AGG`) directly for REST or GraphQL API consumers.

### Refined Query Example (2026 Standard)

Using modern syntax, including standard **JOIN** formatting and a **CTE** for improved readability:

```sql
WITH OrderSummary AS (
    SELECT 
        o.OrderID,
        o.OrderDate,
        c.CustomerName,
        e.LastName AS SalesRep,
        SUM(od.UnitPrice * od.Quantity) AS TotalValue
    FROM Orders o
    JOIN Customers c ON o.CustomerID = c.CustomerID
    JOIN Employees e ON o.EmployeeID = e.EmployeeID
    JOIN OrderDetails od ON o.OrderID = od.OrderID
    GROUP BY 1, 2, 3, 4
)
SELECT * 
FROM OrderSummary
WHERE TotalValue > 1000
ORDER BY OrderDate DESC
LIMIT 100;
```

### Complexity Note
The execution cost of a `SELECT` query typically scales $O(n)$ with full table scans or $O(\log n)$ when utilizing B-Tree or GIN indices. In 2026, developers are expected to analyze query plans using `EXPLAIN ANALYZE` to ensure that join strategies (Nested Loop vs. Hash Join) are optimized for the data distribution.
<br>

## 5. What is the difference between _WHERE_ and _HAVING_ clauses?

### WHERE vs. HAVING: Architectural Distinction

The fundamental difference lies in the **logical order of operations** within the SQL execution pipeline. While both clauses filter rows, they function at distinct stages of the query lifecycle.

#### WHERE Clause: Row-Level Predicate
The `WHERE` clause acts as a pre-aggregation filter. It evaluates conditions against individual rows before any `GROUP BY` operation occurs. 

*   **Execution Order:** Applied immediately after the `FROM`/`JOIN` phase.
*   **Performance:** Highly efficient when used with **SARGable** (Search ARGumentable) expressions. Indexing columns referenced in a `WHERE` clause allows for $O(\log n)$ lookup performance via B-tree index traversal.
*   **Restrictions:** Cannot reference aggregate functions (e.g., `SUM()`, `AVG()`) because the aggregation state has not yet been computed.

#### HAVING Clause: Group-Level Predicate
The `HAVING` clause serves as a post-aggregation filter. It evaluates conditions against the resulting sets generated by a `GROUP BY` clause.

*   **Execution Order:** Applied after the `GROUP BY` phase and before the `SELECT` projection.
*   **Performance:** Higher computational cost as it operates on the filtered set after data has been aggregated into buckets. It generally forces a full scan or a sort of the intermediate result set, typically $O(n \log n)$ complexity.
*   **Capabilities:** Designed to filter based on aggregate results (e.g., `HAVING COUNT(*) > 100`).

### Execution Pipeline Summary

The logical processing order in modern RDBMS (PostgreSQL 17+, SQL Server 2026) follows this sequence:

1.  `FROM` / `JOIN`
2.  `WHERE` (Row Filtering)
3.  `GROUP BY` (Aggregation)
4.  `HAVING` (Group Filtering)
5.  `SELECT` (Projection)
6.  `ORDER BY` (Sorting)

**Note:** In modern analytical query optimization, if a `HAVING` clause contains no aggregates, most optimizers will rewrite it to a `WHERE` clause internally to benefit from indexing, though writing explicit `WHERE` clauses remains the standard for query readability and intent.
<br>

## 6. Define what a _JOIN_ is in SQL and list its types.

### SQL JOIN Architecture and Taxonomy (2026 Standards)

A **JOIN** clause in SQL is a relational operator used to combine rows from two or more tables based on a join predicate. Conceptually, JOINs implement the relational algebra **Join** operation. While foreign keys define referential integrity, joins operate on any expression satisfying the join predicate.

#### Complexity Analysis
Given two tables $T_1$ and $T_2$ with $n$ and $m$ rows, the time complexity for a standard **Nested Loop Join** is $O(n \times m)$. Modern query optimizers prefer **Hash Joins** or **Sort-Merge Joins**, which operate in $O(n+m)$ average time, depending on index availability and memory allocation for hash buffers.

---

### Classification of JOIN Types

1.  **INNER JOIN**: Returns only rows where the join predicate evaluates to `TRUE`.
2.  **OUTER JOIN**: Returns all rows from the specified table(s) plus matching rows.
    *   **LEFT JOIN**: Preserves all rows from the left table.
    *   **RIGHT JOIN**: Preserves all rows from the right table.
    *   **FULL JOIN**: Preserves all rows from both tables, filling non-matches with `NULL`.
3.  **CROSS JOIN**: Produces the **Cartesian Product** of two tables. Complexity: $O(n \times m)$.
4.  **SELF JOIN**: A standard join where a table is joined with itself using table aliases.

---

### Implementation Details & Corrective Refinements

#### Inner Join
The predicate evaluates equality or inequality. Use `INNER` keyword explicitly for semantic clarity.

```sql
SELECT T1.A, T1.B, T2.C
FROM Table1 AS T1
INNER JOIN Table2 AS T2 ON T1.B = T2.B;
```

#### Outer Joins: Null-Handling
When using `FULL JOIN`, use `COALESCE()` or `IFNULL()` to normalize result sets if the join keys differ.

```sql
SELECT COALESCE(T1.B, T2.B) AS B, T1.A, T2.C
FROM Table1 AS T1
FULL JOIN Table2 AS T2 ON T1.B = T2.B;
```

#### Self Join: Hierarchical Resolution
Self joins are frequently used in Recursive Common Table Expressions (CTEs) for recursive hierarchy traversals (e.g., organizational charts).

**Modern Pattern (Recursive CTE):**
```sql
WITH RECURSIVE Hierarchy AS (
    SELECT EmpID, Name, ManagerID FROM Employee WHERE ManagerID IS NULL
    UNION ALL
    SELECT E.EmpID, E.Name, E.ManagerID
    FROM Employee E
    INNER JOIN Hierarchy H ON E.ManagerID = H.EmpID
)
SELECT * FROM Hierarchy;
```

---

### 2026 Audit Notes
*   **Performance**: Avoid `SELECT *` in joins. Explicitly list columns to reduce I/O overhead and minimize the risk of schema drift.
*   **Optimizer Hints**: In distributed SQL environments (e.g., CockroachDB, AlloyDB), consider hash distribution hints to minimize data shuffling during large joins.
*   **Semantic Note**: The original content's "Self Join" example incorrectly labeled the manager names. In practice, a self-join to retrieve human-readable manager names would be:
    ```sql
    SELECT E.Name AS Employee, M.Name AS Manager
    FROM Employee E
    LEFT JOIN Employee M ON E.ManagerID = M.EmpID;
    ```
    *This creates a semantic link between the `ManagerID` column of the primary alias and the `EmpID` of the secondary alias.*
<br>

## 7. What is a _primary key_ in a database?

### Definition: Primary Key (PK)

A **Primary Key** is a constraint that uniquely identifies each tuple (record) within a relation (table). It serves as the immutable anchor for **Entity Integrity**.

### Key Characteristics

- **Uniqueness**: The database engine enforces a `UNIQUE` constraint, ensuring no two rows share the same key value.
- **Non-Nullity**: The column must be `NOT NULL`. Absence of value is logically incompatible with identification.
- **Immutability**: Once assigned, the PK value should not change. Updates to PKs trigger cascading updates across dependent indexes and foreign key relationships, incurring significant $O(n)$ overhead.

### Data Integrity & Structural Role

- **Entity Identity**: Enforces that the row represents a single, distinct real-world object.
- **Relational Anchoring**: Acts as the target for **Foreign Keys (FK)**, forming the backbone of normalized relational schema design.
- **Clustered Indexing**: In most RDBMS (PostgreSQL, SQL Server, MySQL/InnoDB), the PK is the default key for the **Clustered Index**, physically ordering data on disk.

### Performance & Scaling Considerations

- **Indexing Density**: Since the PK dictates physical storage in clustered indexes, using narrow data types (e.g., `BIGINT` or `UUIDv7`) minimizes index fragmentation and I/O latency.
- **Join Optimization**: Highly performant joins rely on PK-FK alignment. Query optimizers use PK statistics to estimate cardinality, which is critical for choosing efficient join algorithms (e.g., Hash Join vs. Merge Join).
- **UUIDs vs. Sequences**: While integers are performant for small-scale systems, distributed systems in 2026 prefer **UUIDv7** (time-ordered) to avoid B-Tree page splits and contention common with monotonic integer sequences.

### Industry Best Practices (2026 Standards)

- **Prefer Surrogate Keys**: Avoid "Natural Keys" (e.g., Email, SSN). Business rules evolve; `student_email` may change, breaking references. Use synthetic identifiers (e.g., `BIGINT IDENTITY` or `UUIDv7`).
- **UUIDv7 Adoption**: Move away from random `UUIDv4` to `UUIDv7`. The monotonic timestamp prefix ensures index-friendly insertion patterns, mitigating the $O(\log n)$ rebalancing costs of random inserts.
- **Minimize Width**: Keep keys as small as possible to minimize memory usage in the **Buffer Pool** and index pages.
- **Composite Keys**: Use only if the relationship is inherently many-to-many or polymorphic. Ensure the leading column is the most frequently filtered attribute.

### Code Example: 2026 Best Practice

Using `BIGINT` with an identity sequence for high-performance single-node databases, or `UUID` for distributed environments.

```sql
-- Standard sequence-based PK (High Performance)
CREATE TABLE Students (
    student_id BIGINT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    student_uuid UUID DEFAULT gen_random_uuid(), -- For distributed systems
    grade_level INT NOT NULL,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    created_at TIMESTAMPTZ DEFAULT CURRENT_TIMESTAMP
);

-- Optimization: Adding a covering index for lookup on the UUID
CREATE UNIQUE INDEX idx_students_uuid ON Students(student_uuid);
```
<br>

## 8. Explain what a _foreign key_ is and how it is used.

### Definition of a Foreign Key
A **Foreign Key (FK)** is a database constraint that enforces **referential integrity** between two tables. It identifies a column (or set of columns) in a referencing table (the **child**) that links to the primary or unique key of a referenced table (the **parent**).

### Key Functions
*   **Referential Integrity**: Guarantees that every value in the FK column must either match an existing value in the parent table's primary key or be `NULL` (unless defined as `NOT NULL`).
*   **Logical Relationship Mapping**: Establishes the structural foundation for relational algebra, enabling efficient `JOIN` operations.
*   **Declarative Referential Integrity (DRI)**: Offloads consistency management from the application layer to the database engine, reducing the risk of orphaned records.
*   **Lifecycle Management**: Automates consistency via `ON DELETE` and `ON UPDATE` triggers (e.g., `CASCADE`, `SET NULL`, `RESTRICT`).

### Correcting Constraints (2026 Audit)
*   **Referential Consistency**: The foreign key must match the **Primary Key** or a **Unique Key** of the parent table. 
*   **Nullability**: FK columns allow `NULL` by default. If the business logic mandates a mandatory relationship, the FK column must be constrained with `NOT NULL`.
*   **Performance Note**: In modern RDBMS (e.g., PostgreSQL 18+, SQL Server 2026), foreign key columns are not automatically indexed. To prevent full table scans during `JOIN` operations and `ON DELETE CASCADE` checks, explicit **B-tree indexes** are required on FK columns where query frequency is high. 
    *   *Complexity:* Verification of an FK constraint during DML operations is $O(\log n)$ per operation given an indexed parent key.

### Use Cases and Best Practices
*   **Normalization**: Essential for adhering to 3rd Normal Form (3NF), minimizing redundancy by splitting data into related tables.
*   **Enforcement of Business Rules**: Use `ON DELETE RESTRICT` to prevent the deletion of a parent record if child records exist, ensuring business-critical data is not accidentally purged.
*   **Distributed Systems**: In distributed SQL architectures (e.g., CockroachDB, YugabyteDB), minimize cross-node FK constraints where possible to reduce latency overhead during transactional commits.

### Implementation: Standard SQL (2026)

```sql
-- Parent Table
CREATE TABLE departments (
    department_id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL
);

-- Child Table with explicit constraint naming for better error handling
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    department_id INT,
    CONSTRAINT fk_department
        FOREIGN KEY (department_id) 
        REFERENCES departments(department_id)
        ON DELETE RESTRICT
        ON UPDATE CASCADE
);

-- Optimization: Explicit index on the FK column to optimize JOIN performance
CREATE INDEX idx_employees_department_id ON employees(department_id);
```

### 2026 Technical Note: "Uniqueness" Clarification
The original text incorrectly stated that the foreign key itself must be unique. **Correction**: The foreign key column in the **child** table does not need to be unique (as in a 'One-to-Many' relationship, many children reference one parent). It is the **referenced key** in the **parent** table that must be unique.
<br>

## 9. How can you prevent _SQL injections_?

### Modernized SQL Injection (SQLi) Defense Strategies (2026)

**SQL Injection (SQLi)** occurs when an application improperly neutralizes user-supplied input, allowing an attacker to interfere with query logic. Defense relies on the principle of **separation of data from code**.

---

### 1. Parameterized Queries (Prepared Statements)
**Description**: The industry-standard primary defense. The SQL query structure is sent to the database engine first, and user inputs are sent later as bound parameters. The database driver ensures inputs are treated strictly as data, never as executable code, reducing the risk to $O(1)$ complexity regarding query logic manipulation.

- **Python (SQLAlchemy 2.0 / `psycopg3`) Example**:
```python
# Using modern Pythonic ORM practices
from sqlalchemy import text
stmt = text("SELECT * FROM users WHERE username = :u AND password = :p")
result = session.execute(stmt, {"u": username, "p": password})
```

- **Benefits**:
  - Eliminates the category of "In-band" SQLi.
  - Improves performance via **query execution plan caching**.

---

### 2. Secure Stored Procedures
**Description**: Stored procedures isolate data access logic. However, they only prevent SQLi if the procedure body itself uses parameterized logic. Constructing strings dynamically *inside* a procedure remains vulnerable.

- **Implementation Note**: In 2026, favor **Application-Level ORMs** (e.g., Prisma, SQLAlchemy, or Entity Framework) over Stored Procedures for business logic to maintain **Type Safety** and database portability.

---

### 3. Strict Input Validation (Allow-listing)
**Description**: Validate input against a defined schema. In 2026, utilize **Pydantic (Python)** or **Zod (TypeScript/Node.js)** for runtime type checking and constraint enforcement.

- **Example (Pydantic v2.10+)**:
```python
from pydantic import BaseModel, StringConstraints
from typing import Annotated

class UserLogin(BaseModel):
    # Enforce strict regex at the boundary
    username: Annotated[str, StringConstraints(pattern=r'^[a-zA-Z0-9_]{3,20}$')]
```

- **Benefits**:
  - Provides "Defense in Depth."
  - Catches malicious payloads before they hit the database layer.

---

### 4. Principle of Least Privilege (PoLP)
**Description**: A critical 2026 infrastructure requirement. The database user account assigned to the web application should possess only the minimum permissions necessary.

- **Requirements**:
  - The application account should **never** run as `db_owner` or `superuser`.
  - Use **Role-Based Access Control (RBAC)** to restrict access to sensitive tables (e.g., `audit_logs` or `sys_users`).
  - Drop permissions for `DROP`, `TRUNCATE`, or `GRANT` operations.

---

### 5. ORM Security vs. Code Filtering
**Deprecated/Caution**: Manual **Code Filtering** (sanitization/escaping via regex) is now considered an anti-pattern. It is error-prone, difficult to maintain, and often bypassable via encoding tricks (e.g., Unicode normalization).

- **2026 Standard**: Utilize modern **Object-Relational Mappers (ORMs)**. High-quality ORMs default to parameterized queries and provide an abstraction layer that makes it difficult to accidentally write raw, insecure SQL. If custom raw queries are necessary, use strictly enforced parameter binding APIs only.
<br>

## 10. What is _normalization_? Explain with examples.

### Normalization: 2026 Architectural Audit

**Normalization** is a database design process that minimizes data redundancy and eliminates insertion, update, and deletion anomalies by organizing columns and tables according to functional dependencies. 

#### Core Normal Forms

*   **1NF (Atomic):** Every attribute contains only atomic values; no sets or arrays.
*   **2NF (No Partial Dependency):** Table must be in 1NF and every non-prime attribute must be **fully functionally dependent** on the primary key.
*   **3NF (No Transitive Dependency):** Table must be in 2NF and no non-prime attribute is dependent on another non-prime attribute.
*   **BCNF (Boyce-Codd):** A stricter version of 3NF where for every functional dependency $X \to Y$, $X$ must be a superkey.
*   **4NF (No Multi-valued Dependencies):** Table must be in BCNF and contain no non-trivial multi-valued dependencies.

---

### Normalization in Action: Case Study

#### Unnormalized Table (0NF)
Storing data in a single flat structure forces **denormalization**, leading to $O(N \cdot M)$ redundancy where $N$ is customers and $M$ is line items. 

| ID | Name | Invoice No. | Item No. | Description | Price |
|----|------|-------------|----------|-------------|-------|

#### First Normal Form (1NF)
Enforces atomicity and uniqueness. We identify the **composite key** `(InvoiceNo, ItemNo)`.

*   **Customers:** `(ID [PK], Name)`
*   **Invoices:** `(InvoiceNo [PK], Customer_ID [FK], Date)`
*   **Invoice_Items:** `(InvoiceNo [FK], ItemNo [PK], Description, Price)`

#### Second Normal Form (2NF)
If we stored `ItemDescription` in the `Invoice_Items` table, it would depend only on `ItemNo`, not the full PK `(InvoiceNo, ItemNo)`. To reach 2NF, we move `Description` to a **Products** catalog table.

#### Third Normal Form (3NF)
We ensure no non-prime attribute depends on another. If `Invoice` table included `Customer_Address`, that would be a **transitive dependency** (`InvoiceNo -> Customer_ID -> Customer_Address`). We move address data exclusively to the `Customers` table.

---

### Practical Implications & 2026 Context

*   **OLTP vs. OLAP:** While 3NF remains the gold standard for **OLTP** (Online Transaction Processing) to ensure ACID compliance, modern **OLAP** (Online Analytical Processing) systems—such as those utilizing **Snowflake** or **Databricks**—often utilize **Star Schema** or **Data Vault** modeling. These patterns intentionally introduce redundancy to optimize analytical query latency via reduced join depth.
*   **Performance:** Normalization increases join complexity. In high-scale distributed systems, consider the cost of distributed joins ($O(\text{network latency})$) against the risk of anomalies.

---

### 2026 Implementation (SQL:2023 Standard)

Using standardized constraints to enforce integrity:

```sql
-- Core Entity: Products (Normalization prevents update anomalies)
CREATE TABLE Products (
    ProductID INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    Description TEXT NOT NULL,
    UnitPrice DECIMAL(12, 2) CHECK (UnitPrice >= 0)
);

-- Normalized Relationship Tables
CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    CustomerName VARCHAR(255) NOT NULL
);

CREATE TABLE Invoices (
    InvoiceNo INT PRIMARY KEY,
    CustomerID INT NOT NULL REFERENCES Customers(CustomerID),
    InvoiceDate TIMESTAMPTZ DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE Invoice_Items (
    InvoiceNo INT REFERENCES Invoices(InvoiceNo),
    ProductID INT REFERENCES Products(ProductID),
    Quantity INT CHECK (Quantity > 0),
    PRIMARY KEY (InvoiceNo, ProductID)
);
```

**Audit Note:** The implementation above utilizes `TIMESTAMPTZ` and `GENERATED ALWAYS AS IDENTITY`, aligning with modern RDBMS capabilities (PostgreSQL 17+, SQL Server 2025) for superior concurrency and type safety.
<br>

## 11. Describe the concept of _denormalization_ and when you would use it.

### Denormalization in Modern RDBMS and Data Architecture

**Denormalization** is the intentional introduction of redundancy into a schema to optimize **Read-Latency** and reduce computational overhead for complex join operations. In 2026, this remains a critical architectural pattern, particularly when balancing the $O(n \log n)$ cost of joins against the $O(1)$ cost of direct column access.

### Refined Techniques

1. **Flattening Relationships**:
   - Consolidating tables to avoid $N$-way joins. In distributed architectures, this minimizes **cross-node communication overhead** (network I/O), which often exceeds local CPU costs.
2. **Pre-aggregation and Materialized Views**:
   - Moving from runtime `SUM()` or `COUNT()` calculations to precomputed columns or **Materialized Views**. Modern RDBMS (e.g., PostgreSQL 18+, SQL Server 2026) support automated concurrent refresh, mitigating traditional staleness issues.
3. **Redundant Attribute Replication**:
   - Storing frequently accessed dimension attributes (e.g., `Customer_Region`) directly in the fact table. This creates a "Star Schema" optimized for **OLAP (Online Analytical Processing)** workloads.

### 2026 Use Cases and Contextual Application

*   **OLAP vs. OLTP**:
    *   **OLTP (Transactional)**: Maintain **3NF (Third Normal Form)** to ensure ACID compliance and prevent update anomalies.
    *   **OLAP (Analytical)**: Adopt **Star/Snowflake Schemas**. Denormalization here is standard practice to support BI tools and vector-search-enabled databases.
*   **High-Volume Distributed Systems**:
    *   In systems utilizing **sharded architectures**, data is denormalized to ensure that queries satisfy the "Locality Principle"—retrieving all required fields from a single shard without cross-shard `JOIN` operations.
*   **Vector Search Integration**:
    *   Modern SQL engines now store embeddings alongside business metadata. Denormalizing metadata into the table containing vectors allows for combined **semantic and relational filtering** in a single scan.

### Considerations and Architectural Trade-offs

*   **Consistency Protocols**:
    *   Denormalization shifts the burden of **Referential Integrity** from the database engine to the application layer. Implementation requires **Idempotent Background Jobs** or **Change Data Capture (CDC)** pipelines (e.g., Debezium) to ensure eventual consistency across redundant fields.
*   **Write Amplification**:
    *   Every update to a source record may now trigger multiple `UPDATE` statements across denormalized replicas. Engineers must calculate the **Write Amplification Factor (WAF)**:
    $$WAF = \frac{\text{Total writes to storage}}{\text{App-level writes}}$$
    If $WAF > \text{threshold}$, normalization should be re-evaluated.
*   **Schema Evolution**:
    *   Denormalized structures are notoriously fragile. Use **Schema Registry** services (e.g., Confluent or internal equivalents) to manage versions, as changing a replicated column requires a multi-table migration strategy.

### Modern Verdict
Denormalization is a **read-optimization strategy**, not a design default. In 2026, favor **Normalization** for transactional integrity, and utilize **Materialized Views or Read Replicas** for denormalized query performance. Reserve physical denormalization only when profiling indicates that query execution plans are constrained by join depth rather than I/O throughput.
<br>

## 12. What are _indexes_ and how can they improve query performance?

### Technical Audit: SQL Indexing (2026 Edition)

**Indexes** are auxiliary data structures that decouple physical data storage from logical retrieval patterns. By maintaining a pointer-based reference system, they reduce the search space from $O(n)$ (full table scan) to $O(\log n)$ (tree-based traversal) or $O(1)$ (hash-based lookup).

### Mechanism of Performance Gains

*   **Logarithmic Complexity**: Using balanced tree structures, the engine navigates a height-constrained path to locate specific row identifiers (RIDs) or clustered keys.
*   **Disk I/O Optimization**: Indexes permit **Index-Only Scans**, allowing the database to satisfy a query directly from the index tree without fetching the full data page from secondary storage.
*   **Join Optimization**: Indexes on foreign keys and join predicates allow the engine to employ **Merge Joins** or **Hash Joins** more effectively, preventing expensive nested-loop operations on large datasets.
*   **Covering Indexes**: By including additional columns in an index leaf node (`INCLUDE` clause), the engine avoids the "bookmark lookup" penalty, keeping the entire query lifecycle within the index structure.

### Modern Index Taxonomy

*   **B+Tree**: The industry standard for range-based queries. In 2026, most engines utilize **B+Trees** where internal nodes store keys and leaf nodes store pointers or data, ensuring predictable $O(\log n)$ performance.
*   **LSM-Trees (Log-Structured Merge-Trees)**: Increasingly prevalent in distributed databases and NoSQL-to-SQL hybrid engines (e.g., RocksDB-based backends). Optimized for write-heavy workloads by buffering updates in memory.
*   **In-Memory Hash Indexes**: Optimized for $O(1)$ point lookups in high-concurrency, volatile memory tables.
*   **BRIN (Block Range Indexes)**: The 2026 standard for massive datasets (e.g., time-series data); they store the minimum/maximum values per page range, providing massive footprint reduction compared to B-Trees.
*   **GIN/GiST (Generalized Inverted/Search Trees)**: Standard for full-text search, JSONB documents, and multidimensional spatial data.

### Architectural Constraints & Trade-offs

*   **Write Amplification**: Every `INSERT`, `UPDATE`, or `DELETE` requires updating the index structure. An excessive index count increases the **Write Penalty** ($O(k \cdot \log n)$ where $k$ is the number of indexes).
*   **Storage Overhead**: Indexes consume primary storage. **Index Fragmentation** can lead to "bloat," necessitating periodic `REINDEX` or `VACUUM` operations to maintain optimal fill factors.
*   **Optimizer Limitations**: The query optimizer may ignore an index if the **Selectivity** (the ratio of distinct values to total rows) is low, defaulting to a sequential scan if the estimated cost of random disk I/O exceeds sequential I/O.

### 2026 Best Practices

1.  **Selectivity Analysis**: Only index columns with high cardinality. Use `EXPLAIN ANALYZE` or `EXPLAIN (FORMAT JSON)` to audit cost-to-performance ratios.
2.  **Partial Indexing**: Utilize **Filtered/Partial Indexes** (e.g., `CREATE INDEX ... WHERE active = true`) to significantly reduce index size and maintenance overhead.
3.  **Composite Index Ordering**: Follow the **Left-Prefix Rule**. In a composite index `(a, b)`, the index is only usable for filters on `a` or `(a, b)`, but not `b` alone.
4.  **Covering Indexes**: Use `INCLUDE` columns to store non-indexed data in leaf nodes, satisfying common queries entirely within the index.
5.  **Automated Statistics**: Ensure the database's `ANALYZE` daemon (autovacuum/auto-stats) is configured to prevent the optimizer from making stale decisions based on outdated distribution statistics.

### Keys vs. Indexes
*   **Primary/Unique Keys**: These enforce logical constraints and *automatically* create a backing index.
*   **Foreign Keys**: These do not automatically create an index in many RDBMS; **explicit manual indexing** on foreign keys is a critical performance requirement for join-heavy schemas.
<br>

## 13. Explain the purpose of the _GROUP BY_ clause.

### Purpose of the `GROUP BY` Clause

The `GROUP BY` clause in SQL is a fundamental relational operation used to partition a result set into summary rows based on the values of one or more columns. It acts as a mandatory precursor for vector-based aggregate functions.

### Key Functions

- **Data Aggregation**: Transforms multiple input rows into a single output row per group.
- **Dimensional Analysis**: Enables multi-dimensional reporting by grouping across hierarchies (e.g., `Region`, `Product`).
- **Post-Aggregation Filtering**: Facilitates group-level predicate logic via the `HAVING` clause, distinct from row-level filtering (`WHERE`).

### Usage and Syntax Patterns

Consider a `Sales` table with columns: `Product`, `Region`, and `Amount`.

#### Data Aggregation
The engine collapses non-aggregated columns into the grouping set.

```sql
-- Standard aggregation for regional metrics
SELECT Region, SUM(Amount) AS TotalSales
FROM Sales
GROUP BY Region;
```

#### Filtering (Row-level vs. Group-level)
The `WHERE` clause filters data *before* aggregation, whereas the `HAVING` clause filters result sets *after* aggregation.

```sql
-- Filtering records > 100 before grouping, then excluding regions with low volume
SELECT Region, COUNT(*) AS HighValueTransactions
FROM Sales
WHERE Amount > 100
GROUP BY Region
HAVING COUNT(*) > 50;
```

#### Window Functions vs. Grouping
For relative contributions, 2026 industry standards favor **Window Functions** over subqueries for performance efficiency ($O(n \log n)$ vs $O(n^2)$ complexity).

```sql
-- Optimized relative contribution using Analytic Window Functions
SELECT Region, Product, 
       SUM(Amount) / SUM(SUM(Amount)) OVER(PARTITION BY Region) AS RelativeContribution
FROM Sales
GROUP BY Region, Product;
```

### Performance and Architectural Considerations

- **Indexing**: `GROUP BY` operations typically trigger internal sort or hash-aggregate operations. Indexing the grouping columns significantly reduces the cost of the `Sort` phase.
- **Hash vs. Stream Aggregation**: Modern Query Optimizers (e.g., PostgreSQL 18+, SQL Server 2026) prefer **Hash Aggregation** when the group cardinality is high and memory allows, as it avoids expensive disk-based sorting.
- **Cardinality Estimation**: Incorrect statistics on grouping columns can lead the optimizer to choose an inefficient scan method (e.g., choosing `Nested Loop` instead of `Hash Aggregate`).
- **Complexity**: The time complexity of a `GROUP BY` operation is generally $O(N \log N)$ due to the sorting required for grouping, or $O(N)$ if using hash-based aggregation, where $N$ is the number of rows processed.

### Modern Best Practices
- **Strict Mode**: Ensure `ONLY_FULL_GROUP_BY` is enabled in your SQL dialect (e.g., MySQL/MariaDB) to prevent non-deterministic query results where non-aggregated, non-grouped columns are selected.
- **Partitioning**: When aggregating petabyte-scale datasets, utilize partitioned tables to enable "partition-wise aggregation," allowing the engine to aggregate within local memory segments before merging.
<br>

## 14. What is a _subquery_, and when would you use one?

### Definition and Scope
A **Subquery** (or nested query) is an inner `SELECT` statement embedded within an outer query (e.g., `SELECT`, `INSERT`, `UPDATE`, or `DELETE`). In modern RDBMS architectures, subqueries are classified based on their interaction with the outer scope: **Non-Correlated** (independent, executed once) and **Correlated** (dependent on the outer query, executed once per row).

### Common Subquery Classifications

#### Scalar Subquery
Returns exactly one row and one column.
*   **Use Case:** Comparisons against atomic values.
*   **Optimization:** Modern optimizers utilize memoization to avoid redundant execution if the subquery is non-correlated.

#### Table (Row/Column) Subquery
Returns one or more rows/columns.
*   **Use Case:** Providing sets for `IN`, `EXISTS`, or `ANY/ALL` operators.
*   **Performance:** In 2026, many query optimizers perform **Subquery Unnesting** (transforming subqueries into `JOIN` operations) to improve execution plan efficiency.

### Advantages and Modern Alternatives
While subqueries provide logical encapsulation, they are increasingly superseded by **Common Table Expressions (CTEs)** for readability and recursive operations.

*   **CTEs (`WITH` clause):** Preferred over subqueries for complex logic as they improve maintainability and allow for recursive tree traversal.
*   **Window Functions:** Should be used instead of correlated subqueries for calculating running totals, ranks, or moving averages to reduce complexity from $O(n^2)$ to $O(n \log n)$ via window partitioning.
*   **`LATERAL` Joins (PostgreSQL/Modern SQL):** Replaces correlated subqueries in `FROM` clauses, allowing columns from the outer query to be referenced within a subquery or table-valued function.

### Limitations and Optimization
*   **Performance:** Unoptimized correlated subqueries introduce an $O(n \cdot m)$ complexity where $n$ is the outer table size and $m$ is the inner. Always check `EXPLAIN ANALYZE` outputs to identify unnecessary row-by-row scanning.
*   **Debugging:** Deeply nested subqueries (e.g., nesting depth > 3) significantly increase cognitive load. CTEs are the 2026 standard for modularizing these patterns.

### Code Examples: 2026 Standards

```sql
-- 1. Scalar Subquery: Retrieving records above average using CTE for clarity
WITH AvgValue AS (
    SELECT AVG(salary) AS global_avg FROM employees
)
SELECT emp_name, salary 
FROM employees, AvgValue 
WHERE salary > AvgValue.global_avg;

-- 2. Correlated Subquery/Lateral Join: 
-- Fetching the most recent order for each customer
SELECT c.customer_name, o.order_date
FROM customers c
CROSS JOIN LATERAL (
    SELECT order_date 
    FROM orders 
    WHERE customer_id = c.id 
    ORDER BY order_date DESC 
    LIMIT 1
) o;
```

### Audit Summary
*   **Accuracy:** Updated to reflect the industry preference for **CTEs** and **Lateral Joins** over legacy deeply-nested subqueries. 
*   **Mathematical Context:** Clarified performance implications; nested operations often lead to non-linear performance degradation.
*   **Modernization:** Explicitly identified `LATERAL` joins as the replacement for correlated subquery patterns in modern analytical workloads.
<br>

## 15. Describe the functions of the _ORDER BY_ clause.

### Technical Audit: ORDER BY Clause

The **ORDER BY** clause specifies the sorting order of a query's result set. In relational theory, rows in a table are inherently unordered; **ORDER BY** provides a deterministic sequence for the output.

### Key Functionality

*   **Multivariate Sorting**: Defines precedence using a comma-separated list. Evaluation proceeds from left to right.
*   **Directional Directives**: **ASC** (ascending, default) and **DESC** (descending).
*   **NULL Handling**: Modern SQL standards (ISO/IEC 9075) utilize **NULLS FIRST** or **NULLS LAST** to explicitly dictate the positioning of null values, which vary by default across engines (e.g., PostgreSQL defaults to **NULLS LAST** for **ASC**).

### Complexity and Performance

Sorting is a blocking operation. The performance complexity is $O(N \log N)$ where $N$ is the number of rows processed. 

*   **Index Utilization**: Engines utilize B-Tree indices to optimize sorting. If the **ORDER BY** columns match the index prefix, the engine performs a sequential scan, reducing complexity to $O(N)$.
*   **Memory Constraints**: Large datasets exceeding the sort buffer (e.g., `work_mem` in PostgreSQL) trigger **External Merge Sorts**, involving disk I/O, which significantly degrades latency.

### 2026 Standards and Refinements

#### SQL Server/Generic Syntax
The use of **Column Position** (e.g., `ORDER BY 1`) is discouraged in 2026. This practice is considered technical debt; it breaks if the `SELECT` list is modified and hinders static analysis and query plan stability. Use explicit column names or aliases.

#### Windowing and Ranking
For "Top-N" queries, modern standards prefer **Window Functions** over `LIMIT` for complex partitioning:
```sql
-- Standard Top-N pattern using Window Functions
SELECT product_name, units_sold
FROM (
    SELECT product_name, units_sold, 
           RANK() OVER (ORDER BY units_sold DESC) as rnk
    FROM sales
    WHERE sale_date = '2026-05-20'
) t
WHERE rnk <= 3;
```

#### Randomization
The `RAND()` function is engine-specific and non-deterministic. For production-grade randomization, use cryptographically secure seeds if available, or the standard `RANDOM()` function (PostgreSQL) or `RAND()` (MySQL/MariaDB). Note that `ORDER BY RANDOM()` performs a full table scan and is computationally expensive ($O(N \log N)$).

### Updated Code Example: Best Practices

```sql
-- Explicit aliasing and NULLS handling
SELECT product_name, sale_date, units_sold
FROM sales
WHERE sale_date = '2026-05-20'
ORDER BY 
    units_sold DESC NULLS LAST, 
    product_name ASC
LIMIT 3;
```

### Audit Findings Summary
1.  **Deprecated Practice**: Dropped "Column Position" reference in production recommendations.
2.  **Standards Compliance**: Added `NULLS FIRST/LAST` syntax, which is critical for deterministic results in 2026.
3.  **Efficiency**: Warned against `ORDER BY RAND()` for large datasets due to $O(N \log N)$ disk-heavy overhead.
4.  **Architectural Shift**: Introduced **Window Functions** as the preferred mechanism for ranking over simple `LIMIT` clauses.
<br>



#### Explore all 100 answers here 👉 [Devinterview.io - SQL](https://devinterview.io/questions/web-and-mobile-development/sql-interview-questions)

<br>

<a href="https://devinterview.io/questions/web-and-mobile-development/">
<img src="https://firebasestorage.googleapis.com/v0/b/dev-stack-app.appspot.com/o/github-blog-img%2Fweb-and-mobile-development-github-img.jpg?alt=media&token=1b5eeecc-c9fb-49f5-9e03-50cf2e309555" alt="web-and-mobile-development" width="100%">
</a>
</p>

