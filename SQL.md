- https://sites.google.com/revature.com/studyguide/databasesql

- Structured Query Language
- Developed based on the [ANSI SQL Standard](https://www.itl.nist.gov/div897/ctg/dm/sql_info.html). 
    - However, there are a lot of different vendor specific implementations available.

## Data Types

- Each column must have a data type which restricts the type of data that can be assigned to it.

| Category  | Sub 1        | Sub 2           | Sub 3          |
| --------- | ------------ | --------------- | -------------- |
| Character | Fixed-length | Variable-length | --             |
| Numeric   | Decimal      | Integer         | Floating point |
| Temporal  | Date         | Time            | Timestamp      |

```sql
CREATE TABLE Employee (
    EmployeeID INT,
    FirstName VARCHAR(50),
    LastName VARCHAR(50),
    Gender CHAR(1),
    DateOfBirth DATE,
    Salary DECIMAL(10, 2),
    IsManager BOOLEAN,
    DepartmentID INT,
    JoinDate TIMESTAMP
);
```

## Constraints

| Constraint  | Use                                                                                                                       |
| ----------- | ------------------------------------------------------------------------------------------------------------------------- |
| Not Null    | Ensures that a column's value is not null.                                                                                |
| Unique      | Ensures that a column's value is unique in the table.                                                                     |
| Primary Key | Combines `unique` and `not null`. Uniquely identifies each row.                                                           |
| Foreign Key | Links to a row in another table. Prevents the destruction of those links.                                                 |
| Default     | Specifies a value for a column, if one is not given. Must be a literal constant.                                          |
| Check       | Ensures the value of a column satisfies a specific condition.<br><br>e.g. `size DECIMAL CHECK (size > 0 AND size <= 100)` |

- It's possible to use a combination of constraints on each column of a table, but in some cases it might lead to redundancy (e.g. `NOT NULL DEFAULT`) and/or conflicting requirements (e.g. `DEFAULT CHECK`).
- To generate an auto-incrementing number column:
    - **PostgreSQL** - `SERIAL`
    - **MySQL** - `AUTO_INCREMENT`
    - **SQLite** - `AUTOINCREMENT`

```sql
CREATE TABLE table_name(
    variable_name variable_datatype AUTO_INCREMENT,
    -- Other columns...
);

CREATE TABLE table_name(
    variable_name variable_datatype PRIMARY KEY AUTOINCREMENT,
    -- Other columns...
);

CREATE TABLE table_name (
    variable_name SERIAL PRIMARY KEY, -- Type and Value implicitly created
    -- Other columns...
);
```

- Modifying the `DEFAULT` constraint of a column:

```sql
-- Add a `DEFAULT` constraint to an existing column of a table
ALTER TABLE table_name ALTER col_name SET DEFAULT default_value;

-- Remove a `DEFAULT` constraint from an existing column of a table.
ALTER TABLE table_name ALTER col_name DROP DEFAULT;
```

### Keys

```sql
CREATE TABLE [IF NOT EXISTS] Users(
    ID    INT           NOT NULL,
    NAME  VARCHAR(20)   NOT NULL,
    AGE   INT           NOT NULL,
    PRIMARY KEY(ID)
);

CREATE TABLE Orders(
    OID      INT        NOT NULL,
    DATE     DATETIME,
    AMOUNT   INT,
    USER_ID  INT,
    FOREIGN KEY (USER_ID) references Users(ID),
    -- or USER_ID INT references Users(ID),
    PRIMARY KEY(OID)
);
```

```mysql
-- Add a Primary Key to an existing table
ALTER TABLE Users ADD PRIMARY KEY (ID);

-- Add a Foreign Key to an existing table
ALTER TABLE Orders
   ADD FOREIGN KEY (USER_ID) REFERENCES Users(ID);
```

- `CASCADE` 
    - Used to simultaneously delete or update data from both the child and parent tables.
    - Allows us to perform operations in a single command without violating the referential integrity.
    - Used in conjunction while writing a query with `ON DELETE` or `ON UPDATE`.

```mysql
CREATE TABLE Orders(
    OID      INT        NOT NULL,
    DATE     DATETIME,
    AMOUNT   INT,
    UID  INT,
    PRIMARY KEY(OID),
    FOREIGN KEY (UID) references Users(ID) ON DELETE CASCADE ON UPDATE CASCADE
);
```

- A `UNIQUE` key allows for `NULL` column values for records.
    - For databases that allow `NULL` values for a `UNIQUE` field, the `UNIQUE` constraint applies only to the non-null values. 
        - i.e. Multiple `NULL` entries for a `UNIQUE` field won't be considered as duplicates.

```sql
CREATE TABLE users (
    user_id INT UNIQUE,
    first_name VARCHAR(255)
);

INSERT INTO students (studentId, firstName, lastName) VALUES
    (1, 'John'),
    (2, 'Jane'),
    (NULL, 'Alice'),  -- Valid
    (NULL, 'Bob');    -- Valid
```

- A candidate key is a field or combination of fields that uniquely identifies each row in a table.
- All candidate keys that are not primary keys are *secondary* or *alternate* keys.
    - Not related to foreign keys.
    - Help ensure data integrity.
    - Used for indexing.

```sql
CREATE TABLE Book (
    BookID INT PRIMARY KEY,   -- Primary Key
    ISBN VARCHAR(20) UNIQUE,  -- Secondary Key
    Name VARCHAR(100)
);
```

## Sublanguages

### DDL

- Data Definition Language 
- Defines data structure

#### `CREATE`

- Used to create objects on the server.
- Can be used to create:
    - Database
    - User
    - Table
    - Index
    - Trigger
    - Function
    - Stored Procedure
    - View
- In certain RDBMS with transactional DDL (e.g. Postgres, SQLite), rollbacks are allowed.

```mysql
CREATE DATABASE [IF NOT EXISTS] my_db;

-- Required in MySQL
USE my_db; 

CREATE [TEMPORARY] TABLE [IF NOT EXISTS] my_table (
    col_name data_type constraints,
    -- ...
);
```

#### `DROP`

- Used to remove objects from the server. 
- Can't be rolled back.
- Any object created using `CREATE` can be dropped using `DROP`.
- It's not allowed to drop a table referenced by foreign key constraint.
    - Objects related to the table like views, procedures needs to be explicitly dropped.

```sqlite
-- Completely remove a table from database.
DROP [TABLE] table_name;
```

#### `ALTER`

- Used to change some characteristics of an object, i.e. to add, drop, or modify some option on the object.
- Commonly used to change table characteristics, like:
    - Add/Drop columns
    - Add/Drop constraints
    - Modify column data types
    - Modify column constraints

```mysql
-- Alter the table.
ALTER TABLE table_name;

-- Rename a table.
ALTER TABLE old_table_name 
RENAME TO new_table_name;

-- Add a column to a table.
ALTER TABLE table_name
ADD column_name INT;

-- MySQL - Modify a column.
ALTER TABLE table_name
MODIFY COLUMN column_name TEXT;

-- Drop a column from a table.
ALTER TABLE table_name
DROP COLUMN column_name;
```

#### `TRUNCATE`

- Used to remove all data from a table along with all space allocated for the records.
    - Also deallocates memory for removed objects.
- Can't be rolled back.
- Conditions aren't allowed.
- Unlike `DROP` truncate will preserve the structure of the table.

```sql
-- Remove all the data and not the table itself.
TRUNCATE [TABLE] table_name;
```

#### `RENAME`

- Used to rename objects.
- Availability and syntax of `RENAME` varies between different DBMS.

```mysql
RENAME TABLE old_name TO new_name [, old_name2 TO new_name2] -- ...
```

#### `COMMENT`

- Typically used to add comments or descriptions to database objects like tables, columns, or views. 
- Comments are not used by the database itself but can be helpful for documentation purposes or for providing additional information about the structure of the database. 
    - Could also be written using `--` for single line and `/* */` for multi-line comments.

### DML

- Data Manipulation Language
- `INSERT`, `UPDATE`, `DELETE`

#### `INSERT`

```sql
INSERT INTO table_name (column1,...columnN)
VALUES (value1,...valueN)[, (valueA,...valueZ)];
```

#### `UPDATE`

- Used to modify whole records or parts of records in a database table.
- Can modify multiple records if conditions don't provide unique results.

```sql
UPDATE table_name 
SET col_name = value[, col2_name = value2, ...]
[WHERE condition];
```

#### `DELETE`

- Used to remove data from a database table.

```sql
DELETE FROM table_name 
[WHERE condition];
```

### DQL

- Data Query Language 
- Search, filter, group, aggregate stored data

#### `SELECT`

```mysql
SELECT <projection> 
FROM <table_name> 
<filter> 
<grouping> 
<ordering> 
<offset>

-- OR

SELECT [ALL | DISTINCT]
    select_expr [, select_expr] ...
    [into_option]
    [FROM table_ref]
    [WHERE where_condition]
    [GROUP BY {col_name | expr | position}]
    [HAVING having_condition]
    [ORDER BY {col_name | expr | position}]
        [ASC | DESC]
    [LIMIT {[offset,] row_count | row_count OFFSET offset}];
```

```sql
SELECT column1, column2, columnN FROM table_name;

-- Aliases
SELECT column1 as col1, column2 as col2, columnN FROM table_name;

SELECT * FROM table_name;

SELECT *           -- SELECT Users.age
FROM table_name    -- FROM Users
WHERE [condition]; -- WHERE name = 'John'
```

##### Filtering using `WHERE`

> [!note]
> The `WHERE` clause is used in `SELECT`, `INSERT` and `UPDATE` statements

| Operator | Meaning                                                                                                                                                                                                               |
| -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| AND      | true if both boolean expressions evaluate to true                                                                                                                                                                     |
| IN       | true if the operand is included in a list of expressions<br><br>e.g. `WHERE id IN (23, 45, 67)`                                                                                                                       |
| NOT      | Reverses the value of any boolean expression<br><br>e.g. `WHERE NOT (id=100)`                                                                                                                                         |
| OR       | true if either or both boolean expressions is true                                                                                                                                                                    |
| LIKE     | true if the operand matches a pattern (`%` for zero or more characters & `_` to match any single character)<br><br>e.g. `WHERE type LIKE 'a%'` (starts with 'a'), `WHERE type LIKE '___'` (exactly 3 characters long) |
| BETWEEN  | true if the operand falls within a range<br><br>e.g. `WHERE price BETWEEN 1.5 and 2.5`, `WHERE name BETWEEN 'm' AND 'p'`                                                                                              |

##### Grouping using `GROUP BY`

- Group rows that have the same values into summary rows.
- Often mandatory to be used with aggregate functions like `count`, `max` and `min`.
- Grouping is done based on the similarity of the row's attribute values.
- Always used before the `ORDER BY` clause in `SELECT`.

```mysql
SELECT type, AVG(price) FROM cars GROUP BY type;
```

- `HAVING` can be used to filter out groups that meet a certain condition.

##### Ordering using `ORDER BY`

- Ensures presentation of columns.
- Output is sorted based on the column's values.
- Always used after the `GROUP BY` clause in `SELECT`.

```sql
SELECT columns FROM table_name ORDER BY col1 [, col2, ...] [ASC | DESC];

SELECT name, price FROM cars ORDER BY name ASC;
```

##### Offset using `LIMIT` and `OFFSET`

- `LIMIT` restricts the number of records returned from a `SELECT` statement.

```sql
SELECT name, price FROM cars ORDER BY name ASC LIMIT 10;
```

- `OFFSET` specifies from which record position to start counting from.
    - Often used in conjunction with the `LIMIT` clause.
    - Some SQL implementations use the `SKIP` keyword instead of `OFFSET`.

```sql
SELECT name, price, type FROM produce ORDER BY name ASC LIMIT 5 OFFSET 5;
```

#### `JOIN`

- Used to combine records from two or more tables in a database. 
- A means for combining fields from two tables by using values common to each.
- Different Types of Joins
    - INNER JOIN
    - OUTER JOIN
        - LEFT JOIN
        - RIGHT JOIN
        - FULL JOIN

> [!quote] SQL Joins Diagram
 > ![SQL Joins Diagram](assets/images/sql.joins-diagram.png)
 > 
 > **Source**: [DbVisualizer](https://dbvis.com/)

```sql
-- Implicit Join without using 'JOIN' ()
SELECT Users.ID, Users.Name, Orders.Amount, Orders.OrderDate
FROM Users, Orders
ON Users.ID = Orders.UserID;

-- Inner Join (Explicit Join - Recommended)
SELECT Users.ID, Users.Name, Orders.Amount, Orders.OrderDate
FROM Users 
INNER JOIN Orders
ON Users.ID = Orders.UserID;
```

> [!quote] SQL Joins
 > ![[SQL Joins (Datacamp).pdf]]
 > 
 > **Source**: [Datacamp](https://datacamp.com/)

-  CROSS JOIN / CARTESIAN JOIN
    - Used to return all possible row combinations from each table.
    - If no condition is provided, the result set is obtained by multiplying each row of the first table with all rows in the second table.
    - Common use cases:
        - Creating a comprehensive dataset for testing
        - Finding missing relationships

```sqlite
SELECT *  
FROM table_1
CROSS JOIN table_2;
```

- SELF JOIN
    - Used to intersect or join a table in the database to itself.

```sqlite
SELECT table_1.col_1 AS col_a, table_2.col_2 AS col_b
FROM my_table table_1
JOIN my_table table_2 ON table_1.col_3 = table_2.col_4;

-- or

SELECT table_1.col_1 AS col_a, table_2.col_2 AS col_b
FROM my_table table_1, my_table table_2
WHERE table_1.col_3 = table_2.col_4;
```

#### Set Operations

- Set operators are used to combine the result of two queries.
- To perform set operations,
    - The order and number of columns must be the same.
    - Data types must be compatible.

- `UNION` - merges result sets of multiple `SELECT` statements into a single result set, removing duplicates.
    - `UNION ALL` doesn't remove duplicate rows.
- `INTERSECT` - used to retrieve the common rows that appear in the result sets of two `SELECT` statements.
    - Unsupported by MySQL
- `EXCEPT` - used to retrieve rows present in the result set of the first SELECT statement but not in the second SELECT statement.
    - `MINUS` is found in some databases, and is functionally equivalent to `EXCEPT`.

### DCL

- Data Control Language 
- Grants or revokes access permissions to database objects
- `GRANT`, `REVOKE`

### TCL

- Transaction Control Language 
- Defines concurrent operation boundaries
- `SAVEPOINT`, `ROLLBACK`, `COMMIT`

## Views

- A virtual table based on the result of a `SELECT` query.
- Provide a way to represent the result of a query as if it were a table.
- Can be used to restrict access to specific columns or rows of a table. 
    - Users can be granted permission to access a view without granting direct access to the underlying table.

```sqlite
CREATE VIEW view_name AS
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```

## Subquery

- A query nested inside of a larger query. 
- Can occur in various subsections of a query:
    - SELECT clause (Inner Query)
        - Create temporary columns on the result set
            - The column created by an inner query has a value equal to the result of the query.
        - Can also be called `inner query` or `inner select` while the container query is called the `outer query` or `outer select`
        - The `inner query` executes before the `outer query`
    - WHERE clause (Nested Query)
        - Can return single or multiple rows
    - FROM clause (Inline View)
        - Create temporary tables
- Can be nested in a `SELECT`, `INSERT`, `UPDATE`, `DELETE`, or even inside of another subquery.
- Logical operators can be used to compare the results of the subquery
- While convenient, subqueries perform worse than joins.

```sql
CREATE TABLE IF NOT EXISTS students(
    id INT PRIMARY KEY,
    name VARCHAR(40) NOT NULL UNIQUE
);

CREATE TABLE IF NOT EXISTS evaluations (
    id INT PRIMARY KEY,
    studentId INT NOT NULL,
    evalName VARCHAR(10) NOT NULL,
    mark INT DEFAULT 0,
    FOREIGN KEY(studentId) REFERENCES students(id),
    CONSTRAINT mark_check CHECK(mark >= 0), CHECK(mark <= 100)
);

INSERT INTO students (id, name) 
VALUES (1, 'Steve'), (2, 'Jane'), (3, 'Casey');

INSERT INTO evals (id, studentId, evalName, mark) 
VALUES 
    (1, 1, 'quiz 1', 98),
    (2, 2, 'quiz 1', 80), 
    (3, 3, 'quiz 1', 95), 
    (4, 1, 'test 1', 72), 
    (5, 2, 'test 1', 100), 
    (6, 3, 'test 1', 68);

-- To find all students that scored higher than Jane (2) on 'quiz 1'

-- Nested Query
SELECT a.id, a.name, b.evalName, b.mark
FROM students a, evals b 
WHERE a.id = b.studentId AND b.evalName = 'quiz 1' AND b.mark > (
    SELECT mark 
    FROM evals 
    WHERE evalName = 'quiz 1' AND studentId = 2
);

-- Inline View (Temporary Tables)
SELECT a.name, b.evalName, b.mark 
FROM students a, (
    SELECT studentId, evalName, mark
    FROM evals 
    WHERE mark > 90
) b 
WHERE a.id = b.studentId;

-- Inline Query (Temporary Columns)
SELECT a.id, a.name, (
    SELECT AVG(mark) 
    FROM evals 
    WHERE studentId = a.id 
    GROUP BY studentId
) avg 
FROM students a;
```

## Schemas

```mysql
CREATE SCHEMA employment;

-- Generate a table inside a specific schema
CREATE TABLE employment.employees(
    employee_id INT PRIMARY KEY IDENTITY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    department VARCHAR(50)
);
```

## Postgres

### Concepts

- Architecture: https://www.youtube.com/watch?v=Q56kljmIN14
- Playlist: https://www.youtube.com/playlist?list=PLQnljOFTspQWGrOqslniFlRcwxyY94cjj

---

## Further

### Learn 🧠

- [Complete SQL and Databases Bootcamp - Udemy](https://www.udemy.com/course/complete-sql-databases-bootcamp-zero-to-mastery/)

- [SQL Tutorial - freeCodeCamp](https://youtube.com/watch?v=HXV3zeQKqGY)

### Roadmaps 🗺

- [PostgreSQL Roadmap](https://roadmap.sh/postgresql-dba)

### Videos 🎥

![SQL Joins Explained](https://www.youtube.com/watch?v=9yeOJ0ZMUYw)