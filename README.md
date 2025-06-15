# Project-1: MySQL Practice
## Skill: SQL
## Difficulty: ★☆☆☆☆

### Goal:
Practice basic SQL SELECT statements, including column/row selection, aliasing, filtering, ordering, and derived columns by following SQL TUTORIAL of AnShul Gupta in Youtube
### SQL Tool:
MySQL

#

### Selecting Database
-- This command sets the 'orders' database as the current default database.

-- Subsequent queries will operate on tables within 'orders' unless specified otherwise.
```sql
USE orders;
```


### Selecting Columns
Columns: Created_Date and Order_ID

Database: orders.

Table: order_details
```sql
SELECT Created_date, Order_ID
FROM orders.orders_details;
```

Rename the column name from Created_Date to Date
```sql
SELECT Created_Date AS Date
FROM orders.orders_details;
```

Rename the column name from Created_Date to Created Date
```sql
SELECT Created_Date AS "Created Name"
FROM orders.orders_details;
```

Getting unique data of Order_Type
```sql
SELECT DISTINCT Order_Type
FROM orders.orders_details;
```

Getting unique data of Order_ID per Order_Type
```sql
SELECT DISTINCT Order_ID, Order_Type
FROM orders.orders_details;
```

### Selection of rows
Columns: All

Database: orders

Table: order_details

Rows: Order_Type is Online
```sql
SELECT *
FROM orders.orders_details
WHERE Order_Type = "Online";
```

Rows: Amount is greater than 3000
```sql
SELECT *
FROM orders.orders_details
WHERE Amount >= 3000;
```

-- Signs: =, >, <, >=, <=, !=, <>

Rows: Order_Type is NOT Online
```sql
SELECT *
FROM orders.orders_details
WHERE Order_Type != "Online";
```

-- Always follow the date format in the table

Rows: Invoice_Date is past April 5, 2025
```sql
SELECT *
FROM orders.orders_details
WHERE Invoice_Date > "2025-04-05";
```

Rows: Invoice_Date is past April 5, 2025 and Order_Type is Online
```sql
SELECT *
FROM orders.orders_details
WHERE Invoice_Date > "2025-04-05" AND Order_Type = "Online";
```

Rows: Invoice_Date is past April 5, 2025 or Order_Type is Online
```sql
SELECT *
FROM orders.orders_details
WHERE Invoice_Date > "2025-04-05" OR Order_Type = "Online";
```

Rows: Order_Type is not Online and Invoice_Date is past April 5, 2025
```sql
SELECT *
FROM orders.orders_details
WHERE NOT Order_Type = "Online" AND Invoice_Date > "2025-04-05";
```

Rows: Order_Type is not Online and Invoice_Date is not past April 5, 2025
```sql
SELECT *
FROM orders.orders_details
WHERE NOT (Order_Type = "Online" AND Invoice_Date > "2025-04-05");
```

Rows: Order_Type is not Online or Invoice_Date is not past April 5, 2025
```sql
SELECT *
FROM orders.orders_details
WHERE NOT (Order_Type = "Online" OR Invoice_Date > "2025-04-05");
```

### Selection of rows with order
Columns: All

Database: orders

Table: order_details

Rows: Order_Type is Online

Order: Order_ID is descending
```sql
SELECT *
FROM orders.orders_details
WHERE Order_Type = "Online"
ORDER BY Order_ID desc;
```

Order1: Payment_Method ascending (least to most or alpha)

Order2: Invoice_Date is descending (most to least or reverse alpha)
```sql
SELECT *
FROM orders.orders_details
WHERE Order_Type = "Online"
ORDER BY Payment_Method asc, Invoice_Date desc;
```

/* Add new columns
Columns: All
Database: orders
Table: order_details
Rows: Order_Type is Online
Add: old_customer_id based on Customer_ID*/
SELECT *, Customer_ID AS old_customer_id
FROM orders.orders_details
WHERE Order_Type = "Online";

-- Add: Tax based on Amount multiply by 10%
SELECT *, Amount*0.1 AS Tax
FROM orders.orders_details
WHERE Order_Type = "Online";

/* Add1: Tax based on Amount multiply by 10%
Add2: Total_Value based on Amount plus Tax */
SELECT *, Amount*0.1 AS Tax, Amount + Amount*0.1 AS Total_Value
FROM orders.orders_details
WHERE Order_Type = "Online";

-- BODMAS (Brakets, Orders, Division, Multiplication, Addition, Subtraction
-- All filters and additions are not applied to the main database

-- Challenge: Om the Orders Table, filter the 
SELECT *,
	date(Order_Date+3) AS "Shipment Date"
FROM orders.orders
WHERE
	Order_Date > '2025-04-02' AND Order_Date < '2025-04-08'
    AND NOT(Order_No = 'ORD003' OR Order_No = 'ORD005' OR Order_No = 'ORD007')
ORDER BY Order_Date desc;
