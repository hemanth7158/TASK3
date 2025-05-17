# Task 3: SQL for Data Analysis – Data Analyst Internship



##  Project Overview

This project focuses on using **SQL** to analyze structured ecommerce data. The goal was to simulate a real-world scenario where one would extract business insights such as revenue, category-based sales, and customer behavior using SQL queries.

---

##  Tools Used
- SQL (tested on MySQL)
- Any RDBMS supporting standard SQL (MySQL / PostgreSQL / SQLite)
- GitHub for version control and submission

---

##  Database Structure

Four primary tables were created:

- **`customers`** – Contains customer details  
- **`products`** – Contains product information  
- **`orders`** – Links customers with order records  
- **`order_items`** – Holds order details including quantity and product

---

##  Data Inserted
Manually inserted sample data:
- 2 customers
- 3 products
- 2 orders
- 3 order items

---

## SQL Tasks Completed

### 1. Data Filtering & Sorting
```sql
SELECT * FROM products WHERE price > 100 ORDER BY price DESC;
```

---

### 2. Total Revenue Calculation
```sql
SELECT SUM(p.price * oi.quantity) AS total_revenue
FROM order_items oi
JOIN products p ON oi.product_id = p.product_id;
```

---

### 3. Revenue by Product Category
```sql
SELECT p.category, SUM(p.price * oi.quantity) AS revenue
FROM order_items oi
JOIN products p ON oi.product_id = p.product_id
GROUP BY p.category;
```

---

### 4. Customer Order Details
```sql
SELECT c.name, o.order_id, o.order_date, p.name AS product, oi.quantity
FROM customers c
JOIN orders o ON c.customer_id = o.customer_id
JOIN order_items oi ON o.order_id = oi.order_id
JOIN products p ON oi.product_id = p.product_id;
```

---

### 5. Subquery – Customers Spending > $1000
```sql
SELECT name FROM customers
WHERE customer_id IN (
    SELECT o.customer_id
    FROM orders o
    JOIN order_items oi ON o.order_id = oi.order_id
    JOIN products p ON oi.product_id = p.product_id
    GROUP BY o.customer_id
    HAVING SUM(p.price * oi.quantity) > 1000
);
```

---

### 6. Create a View – Revenue by Category
```sql
CREATE VIEW category_revenue AS
SELECT p.category, SUM(p.price * oi.quantity) AS revenue
FROM order_items oi
JOIN products p ON oi.product_id = p.product_id
GROUP BY p.category;
```

---

### 7. Query Optimization – Add Index
```sql
CREATE INDEX idx_product_id ON order_items(product_id);
```

---

### 8. Null Handling
```sql
SELECT SUM(COALESCE(p.price, 0) * oi.quantity) AS total_revenue
FROM order_items oi
JOIN products p ON oi.product_id = p.product_id;
```

---



## Concepts Practiced
- DDL: Table creation
- DML: Data insertion
- SELECT, WHERE, ORDER BY
- JOINs (INNER JOIN)
- Aggregate functions: `SUM`, `GROUP BY`, `COALESCE`
- Subqueries
- Views
- Indexing for performance
