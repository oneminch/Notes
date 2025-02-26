- In the context of [[Databases]], *denormalization* is a technique used to improve read performance and query efficiency by selectively adding redundant data or combining tables.
    - Typically applied after a database has been normalized.
    - Optimize read-heavy workloads.
    - Can be achieved in various different ways:
        - *Partitioning*
        - *Materialized Views* 
            - Pre-computed query results stored as separate tables.
        - *Storing Derivable Data*
            - Pre-calculating and storing values that are frequently queried.
        - *Combining Tables*

```sql
CREATE TABLE DenormalizedOrders AS
SELECT o.OrderID, o.OrderDate, c.CustomerName, c.CustomerAddress, p.ProductName
FROM Orders o
JOIN Customers c ON o.CustomerID = c.CustomerID
JOIN Products p ON o.ProductID = p.ProductID;
```