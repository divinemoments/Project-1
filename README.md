# Project-1: MySQL Practice
## Skill: SQL
## Difficulty: ★☆☆☆☆

### Goal:
Practice basic SQL SELECT statements, including column/row selection, aliasing, filtering, ordering, and derived columns by following SQL TUTORIAL of AnShul Gupta in Youtube
### SQL Tool:
MySQL

#

### Selecting Database
Use the 'orders' database.

Subsequent queries will operate on tables within 'orders' unless specified otherwise.
```sql
USE orders;
```


### Selecting Columns
Select the 'Created_Date' and 'Order_ID' columns from the 'orders_details' table.
```sql
SELECT Created_date, Order_ID
FROM orders.orders_details;
```

Rename the 'Created_Date' column to 'Date'.
```sql
SELECT Created_Date AS Date
FROM orders.orders_details;
```

Rename the 'Created_Date' column to "Created Name".
```sql
SELECT Created_Date AS "Created Name"
FROM orders.orders_details;
```

Get unique 'Order_Type' values.
```sql
SELECT DISTINCT Order_Type
FROM orders.orders_details;
```

Get unique combinations of 'Order_ID' and 'Order_Type'.
```sql
SELECT DISTINCT Order_ID, Order_Type
FROM orders.orders_details;
```


### Seleting Rows (Filtering with WHERE Clause)
Select all columns from 'orders_details' where 'Order_Type' is "Online".
```sql
SELECT *
FROM orders.orders_details
WHERE Order_Type = "Online";
```

Select all columns from 'orders_details' where 'Amount' is 3000 or greater.
```sql
SELECT *
FROM orders.orders_details
WHERE Amount >= 3000;
```

Select all columns from 'orders_details' where 'Order_Type' is not "Online".
```sql
SELECT *
FROM orders.orders_details
WHERE Order_Type != "Online";
```

Select all columns from 'orders_details' where 'Invoice_Date' is after "2025-04-05".
```sql
SELECT *
FROM orders.orders_details
WHERE Invoice_Date > "2025-04-05";
```

Select all columns from 'orders_details' where 'Invoice_Date' is after "2025-04-05" AND 'Order_Type' is "Online".
```sql
SELECT *
FROM orders.orders_details
WHERE Invoice_Date > "2025-04-05" AND Order_Type = "Online";
```

Select all columns from 'orders_details' where 'Invoice_Date' is after "2025-04-05" OR 'Order_Type' is "Online".
```sql
SELECT *
FROM orders.orders_details
WHERE Invoice_Date > "2025-04-05" OR Order_Type = "Online";
```

Select all columns from 'orders_details' where 'Order_Type' is not "Online" AND 'Invoice_Date' is after "2025-04-05".
```sql
SELECT *
FROM orders.orders_details
WHERE NOT Order_Type = "Online" AND Invoice_Date > "2025-04-05";
```

Select all columns from 'orders_details' where it's NOT true that ('Order_Type' is "Online" AND 'Invoice_Date' is after "2025-04-05").
```sql
SELECT *
FROM orders.orders_details
WHERE NOT (Order_Type = "Online" AND Invoice_Date > "2025-04-05");
```

Select all columns from 'orders_details' where it's NOT true that ('Order_Type' is "Online" OR 'Invoice_Date' is after "2025-04-05").
```sql
SELECT *
FROM orders.orders_details
WHERE NOT (Order_Type = "Online" OR Invoice_Date > "2025-04-05");
```

### Ordering Results (ORDER BY Clause)
Select all columns from 'orders_details' where 'Order_Type' is "Online", ordered by 'Order_ID' in descending order.
```sql
SELECT *
FROM orders.orders_details
WHERE Order_Type = "Online"
ORDER BY Order_ID desc;
```

Select all columns from 'orders_details' where 'Order_Type' is "Online", ordered by 'Payment_Method' ascending, then 'Invoice_Date' descending.
```sql
SELECT *
FROM orders.orders_details
WHERE Order_Type = "Online"
ORDER BY Payment_Method asc, Invoice_Date desc;
```

### Adding New/Derived Columns
Select all columns from 'orders_details' where 'Order_Type' is "Online", adding 'Customer_ID' as 'old_customer_id'.
```sql
SELECT *, Customer_ID AS old_customer_id
FROM orders.orders_details
WHERE Order_Type = "Online";
```

Select all columns from 'orders_details' where 'Order_Type' is "Online", adding 'Amount' multiplied by 0.1 as 'Tax'.
```sql
SELECT *, Amount * 0.1 AS Tax
FROM orders_details
WHERE Order_Type = "Online";
```

Select all columns from 'orders_details' where 'Order_Type' is "Online", adding 'Tax' (Amount * 0.1) and 'Total_Value' (Amount + Tax).
```sql
SELECT *,
       Amount * 0.1 AS Tax,
       Amount + (Amount * 0.1) AS Total_Value
FROM orders_details
WHERE Order_Type = "Online";
```

### Challenge Query
From the orders table, select all columns, add 'Order_Date' plus 3 days as "Shipment Date", filter for orders between '2025-04-02' and '2025-04-08' (inclusive of start, exclusive of end), include only orders with an even 'Order_ID' (assuming it's numeric), and order results by 'Order_Date' descending.
```sql
SELECT *,
	DATE(Order_Date + 3) AS "Shipment Date"
FROM orders.orders
WHERE
	Order_Date BETWEEN '2025-04-02' AND '2025-04-07'
	AND MOD(Order_ID, 2) = 0
ORDER BY Order_Date DESC;
```

### Important Reminders
| Category               | Detail                                     | Explanation / Usage                                                                                   |
| :--------------------- | :----------------------------------------- | :------------------------------------------------------------------------------------------------------ |
| **Comparison Operators** | `=`, `>`, `<`, `>=`, `<=`, `!=`, `<>`   | Used in `WHERE` clauses to filter rows. `!=` and `<>` both mean "not equal to."                         |
| **Date Format** | `YYYY-MM-DD`                               | Always use this format for date literals (e.g., `'2025-04-05'`) when comparing with date columns.     |
| **Operator Precedence**| **BODMAS** | **B**rackets, **O**rders (powers/roots), **D**ivision, **M**ultiplication, **A**ddition, **S**ubtraction. SQL calculations follow this order. |
| **Query Impact** | Filters and additions do **not** affect main database | `SELECT` queries, `WHERE` filters, and columns created with `AS` are temporary; they only modify the query's output, not the actual table data. |
