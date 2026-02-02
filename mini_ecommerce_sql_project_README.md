# Mini E-Commerce SQL Database Project

## Overview
This project is a **Mini E-Commerce Database** built using **MySQL and SQL**.  
It demonstrates core database concepts such as table design, relationships, joins, and analytical queries.

---

## Step 1 – Create Database

```sql
CREATE DATABASE mini_ecommerce;
USE mini_ecommerce;
```

**Logic:**  
 Creates a container (database) to store all tables.
 `USE` tells SQL to work inside this database.

---

## Step 2 – Customers Table

```sql
CREATE TABLE Customers (
    customer_id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100),
    email VARCHAR(100) UNIQUE,
    city VARCHAR(50),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

**Concepts:**
 `PRIMARY KEY` → Unique identifier.
 `AUTO_INCREMENT` → Automatically increases ID.
 `UNIQUE` → Prevents duplicate emails.
 `TIMESTAMP DEFAULT CURRENT_TIMESTAMP` → Stores signup time automatically.

---

## Step 3 – Products Table

```sql
CREATE TABLE Products (
    product_id INT PRIMARY KEY AUTO_INCREMENT,
    product_name VARCHAR(100),
    price DECIMAL(10,2),
    stock INT,
    category VARCHAR(50)
);
```

**Concepts:**
 `DECIMAL(10,2)` → Used for money values.
 `stock` → Tracks inventory.

---

## Step 4 – Orders Table

```sql
CREATE TABLE Orders (
    order_id INT PRIMARY KEY AUTO_INCREMENT,
    customer_id INT,
    order_date DATE,
    status VARCHAR(30),
    FOREIGN KEY (customer_id) REFERENCES Customers(customer_id)
);
```

**Concepts:**
 `FOREIGN KEY` → Connects Orders to Customers.
 Ensures orders cannot exist without valid customers.

---

## Step 5 – OrderItems Table (Bridge Table)

```sql
CREATE TABLE OrderItems (
    order_item_id INT PRIMARY KEY AUTO_INCREMENT,
    order_id INT,
    product_id INT,
    quantity INT,
    FOREIGN KEY (order_id) REFERENCES Orders(order_id),
    FOREIGN KEY (product_id) REFERENCES Products(product_id)
);
```

**Concept: Many‑to‑Many Relationship**
 One order can contain many products.
 One product can appear in many orders.
 Bridge table solves this relationship.

---

## Step 6 – Payments Table

```sql
CREATE TABLE Payments (
    payment_id INT PRIMARY KEY AUTO_INCREMENT,
    order_id INT,
    amount DECIMAL(10,2),
    payment_method VARCHAR(30),
    payment_date DATE,
    FOREIGN KEY (order_id) REFERENCES Orders(order_id)
);
```

**Concepts:**
 Separates financial data from orders.
 Maintains clean database design.

---

## Sample Data Insert

```sql
INSERT INTO Customers (name, email, city)
VALUES ('Rit', 'rit@email.com', 'Pune');
```

**Purpose:** Add test data to run queries.

---

## Important Queries

### Join Example
```sql
SELECT o.order_id, c.name
FROM Orders o
JOIN Customers c ON o.customer_id = c.customer_id;
```

**Concept:** Combine tables using JOIN.

---

### Aggregate Example
```sql
SELECT SUM(quantity) FROM OrderItems;
```

**Concept:** Aggregation (SUM, AVG, COUNT, MAX, MIN).

---

### Group By Example
```sql
SELECT product_id, SUM(quantity)
FROM OrderItems
GROUP BY product_id;
```

**Concept:** Groups similar data for reporting.

---

### Order By Example
```sql
ORDER BY quantity DESC;
```

**Concept:** Sorting results.

---

## Key Concepts Learned
 Primary Key
 Foreign Key
 Normalization
 Many‑to‑Many Relationships
 Joins
 Aggregate Functions
 Constraints
 Data Types

---

## Tools Used
 MySQL 
 SQL
 MySQL Workbench

---
