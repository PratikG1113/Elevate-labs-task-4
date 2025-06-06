Elevate task 4

# 📊 SQL Data Analysis Project: E-commerce Database

## 📁 Project Overview

This project demonstrates the use of **SQL** for building and analyzing a basic **e-commerce database**. It includes customer, product, order, and order item records with realistic queries to extract insights. The focus is on relational data modeling, basic and advanced querying, and database normalization.

---

## 🛠 Tools Used

- **Database Engine**: MySQL
- **Interface**: MySQL Workbench (or compatible IDE)
- **SQL Features Practiced**:
  - DDL (Data Definition Language)
  - DML (Data Manipulation Language)
  - Aggregate functions
  - Joins and subqueries
  - Views
  - Normalization

---

## 🗃️ Database Schema

**Tables Created:**
- `customers`: Customer records
- `products`: Product catalog
- `orders`: Orders with total amount and customer references
- `order_items`: Line items for each order

**Relationships:**
- One-to-many: Customers → Orders
- Many-to-many: Orders ↔ Products (via `order_items`)

---

## 🧪 Sample Queries and Tasks Executed

### 1. Recent Orders
```sql
SELECT DISTINCT c.* 
FROM customers c
JOIN orders o ON c.id = o.customer_id
WHERE o.order_date >= DATE_SUB(CURDATE(), INTERVAL 30 DAY);
```

### 2. Total Spent by Customer
```sql
SELECT c.name, SUM(o.total_amount) AS total_spent
FROM customers c
LEFT JOIN orders o ON c.id = o.customer_id
GROUP BY c.id, c.name;
```

### 3. Update Product Price
```sql
UPDATE products
SET price = 45.00
WHERE name = 'Product C';
```

### 4. Add Discount Column
```sql
ALTER TABLE products
ADD COLUMN discount DECIMAL(5, 2) DEFAULT 0.00;
```

### 5. Top 3 Expensive Products
```sql
SELECT *
FROM products
ORDER BY price DESC
LIMIT 3;
```

### 6. Customers Who Ordered "Product A"
```sql
SELECT DISTINCT c.name
FROM customers c
JOIN orders o ON c.id = o.customer_id
JOIN order_items oi ON o.id = oi.order_id
JOIN products p ON oi.product_id = p.id
WHERE p.name = 'Product A';
```

### 7. Join: Customer Name with Order Date
```sql
SELECT c.name, o.order_date
FROM orders o
JOIN customers c ON o.customer_id = c.id;
```

### 8. High-Value Orders (> ₹150)
```sql
SELECT *
FROM orders
WHERE total_amount > 150.00;
```

### 9. Normalize Orders → `order_items`
```sql
CREATE TABLE order_items (
    id INT AUTO_INCREMENT PRIMARY KEY,
    order_id INT NOT NULL,
    product_id INT NOT NULL,
    quantity INT NOT NULL DEFAULT 1,
    price DECIMAL(10, 2) NOT NULL,
    FOREIGN KEY (order_id) REFERENCES orders(id),
    FOREIGN KEY (product_id) REFERENCES products(id)
);
```

### 10. Average Order Value
```sql
SELECT AVG(total_amount) AS average_order_total
FROM orders;
```

### 11. Create a View for Customers
```sql
CREATE VIEW view1 AS
SELECT name, email, address FROM customers;

-- Use the view
SELECT * FROM view1;
```

---

## 📸 Screenshots

Screenshots of query outputs are stored in the `/screenshots` folder.

---

## 📈 Key Learnings

- Learned how to design a normalized relational database schema
- Practiced complex joins and filtering logic
- Applied aggregate functions for business insights
- Understood database extensibility using views
- Worked with real-world logic (orders, customers, products)



