- https://sites.google.com/revature.com/studyguide/databasesql

```sql
CREATE TABLE Users(
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

```sql
-- Add a Primary Key to an existing table
ALTER TABLE Users ADD PRIMARY KEY (ID);

-- Add a Foreign Key to an existing table
ALTER TABLE Orders
   ADD FOREIGN KEY (USER_ID) REFERENCES Users(ID);
```

## Statements

- **DDL** - Data Definition Language - CREATE, ALTER, DROP
- **DML** - Data Manipulation Language - SELECT, INSERT, UPDATE, DELETE
- **DCL** - Data Control Language - GRANT, REVOKE
- **TCL** - Transaction Control Language - SAVEPOINT, ROLLBACK, COMMIT

### `SELECT`

```sql
SELECT column1, column2, columnN FROM table_name;

SELECT * FROM table_name;

SELECT *           -- SELECT Users.age
FROM table_name    -- FROM Users
WHERE [condition]; -- WHERE name = 'John'
```

> [!note]
> The `WHERE` clause is used in `SELECT`, `INSERT` and `UPDATE` statements

### `INSERT`

```sql
INSERT INTO table_name (column1, column2,...columnN)
VALUES (value1, value2,...valueN);
```

### `JOIN`

- Used to combine records from two or more tables in a database. 
- A means for combining fields from two tables by using values common to each.
- Different Types of Joins
    - INNER JOIN
    - LEFT JOIN
    - RIGHT JOIN
    - FULL JOIN

```sql
SELECT ID, NAME, AGE, AMOUNT
   FROM Users 
   INNER JOIN Orders
   ON Users.ID = Orders.USER_ID;
```


---

## Further

### Learn 🧠

- [Complete SQL and Databases Bootcamp - Udemy](https://www.udemy.com/course/complete-sql-databases-bootcamp-zero-to-mastery/)

- [SQL Tutorial - freeCodeCamp](https://youtube.com/watch?v=HXV3zeQKqGY)

### Roadmaps 🗺

- [PostgreSQL Roadmap](https://roadmap.sh/postgresql-dba)

### Videos 🎥

![SQL Joins Explained](https://www.youtube.com/watch?v=9yeOJ0ZMUYw)