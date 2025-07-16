# SQL Database Assignment Solution

## Database Schema Implementation

### Table Creation
```sql
-- Customer table
CREATE TABLE Customer (
    Customer_id INT PRIMARY KEY,
    customer_Name VARCHAR(100) NOT NULL,
    customer_Tel VARCHAR(20)
);

-- Product table
CREATE TABLE Product (
    Product_id INT PRIMARY KEY,
    product_name VARCHAR(100) NOT NULL,
    category VARCHAR(50),
    Price DECIMAL(10,2) NOT NULL
);

-- Orders table
CREATE TABLE Orders (
    Customer_id INT,
    Product_id INT,
    OrderDate DATE NOT NULL,
    quantity INT NOT NULL,
    total_amount DECIMAL(10,2) NOT NULL,
    PRIMARY KEY (Customer_id, Product_id, OrderDate),
    FOREIGN KEY (Customer_id) REFERENCES Customer(Customer_id),
    FOREIGN KEY (Product_id) REFERENCES Product(Product_id)
);
```
### Sample Data Insertion
```sql
-- Customers
INSERT INTO Customer VALUES
(1, 'John Smith', '555-1234'), (2, 'Emily Johnson', '555-2345'),
(3, 'Michael Brown', '555-3456'), (4, 'Sarah Davis', '555-4567'),
(5, 'David Wilson', '555-5678'), (6, 'Jessica Miller', NULL),
(7, 'Robert Taylor', '555-7890');

-- Products
INSERT INTO Product VALUES
(101, 'Laptop', 'Electronics', 8999.99), (102, 'Smartphone', 'Electronics', 7999.99),
(103, 'Desk Chair', 'Furniture', 5999.99), (104, 'Coffee Table', 'Furniture', 7499.99),
(105, 'Blender', 'Appliances', 2799.99), (106, 'Headphones', 'Electronics', 4499.99),
(107, 'Bookshelf', 'Furniture', 4299.99), (108, '4K TV', 'Electronics', 35999.99),
(109, 'Microwave', 'Appliances', 2899.99), (110, 'Gaming Console', 'Electronics', 14999.99);

-- Orders
INSERT INTO Orders VALUES
(1, 101, '2023-01-15', 1, 8999.99), (1, 106, '2023-01-15', 2, 8999.98),
(2, 102, '2023-02-20', 1, 7999.99), (3, 108, '2023-03-10', 1, 35999.99),
/* Additional orders omitted for brevity */
```
# Step 2: Assignment Questions and Answers

## 1. Display all customer data
```sql
SELECT * FROM Customer;
```
| CUSTOMER_ID | CUSTOMER_NAME  | CUSTOMER_TEL |
|------------|---------------|-------------|
| 1          | John Smith     | 555-1234    |
| 2          | Emily Johnson  | 555-2345    |
| 3          | Michael Brown  | 555-3456    |
| 4          | Sarah Davis    | 555-4567    |
| 5          | David Wilson   | 555-5678    |
| 6          | Jessica Miller | NULL        |
| 7          | Robert Taylor  | 555-7890    |

```
## 2. Products priced between 5000-10000
```sql
SELECT product_name, category FROM Product WHERE Price BETWEEN 5000 AND 10000;
```
## 3. All products sorted by price (descending)

```sql
SELECT * FROM Product ORDER BY Price DESC;

(2, 110, '2020-05-30', 1, 14999.99);
```
## 4. 📊 Order Statistics

```sql
SELECT COUNT(*) AS total_orders, 
       AVG(total_amount) AS average_amount,
       MAX(total_amount) AS highest_amount,
       MIN(total_amount) AS lowest_amount
FROM Orders;
## 4. 📊 Order Statistics

```sql
SELECT COUNT(*) AS total_orders, 
       AVG(total_amount) AS average_amount,
       MAX(total_amount) AS highest_amount,
       MIN(total_amount) AS lowest_amount
FROM Orders;
```

```text
| TOTAL_ORDERS | AVERAGE_AMOUNT | HIGHEST_AMOUNT | LOWEST_AMOUNT |
|--------------|----------------|----------------|----------------|
| 20           | 10949.988      | 35999.99       | 2799.99        |
```

---

## 5. 📦 Orders Per Product

```sql
SELECT Product_id, COUNT(*) AS number_of_orders
FROM Orders 
GROUP BY Product_id 
ORDER BY Product_id;
```

```text
| PRODUCT_ID | NUMBER_OF_ORDERS |
|------------|------------------|
| 101        | 2                |
| 102        | 2                |
| 103        | 2                |
| 104        | 2                |
| 105        | 2                |
| 106        | 2                |
| 107        | 2                |
| 108        | 2                |
| 109        | 2                |
| 110        | 2                |
```

---

## 6. 👥 Customers with More Than 2 Orders

```sql
SELECT Customer_id 
FROM Orders 
GROUP BY Customer_id 
HAVING COUNT(*) > 2;
```

```text
| CUSTOMER_ID |
|-------------|
| 1           |
| 4           |
| 5           |
```

---

## 7. 📅 2020 Monthly Orders

```sql
SELECT EXTRACT(MONTH FROM OrderDate) AS month, 
       COUNT(*) AS number_of_orders
FROM Orders 
WHERE EXTRACT(YEAR FROM OrderDate) = 2020
GROUP BY EXTRACT(MONTH FROM OrderDate) 
ORDER BY month;
```

```text
| MONTH | NUMBER_OF_ORDERS |
|-------|------------------|
| 1     | 1                |
| 2     | 1                |
| 3     | 1                |
| 4     | 1                |
| 5     | 1                |
| 11    | 1                |
| 12    | 1                |
```

---

## 8. 📄 Order Details with Names

```sql
SELECT p.product_name, c.customer_Name, o.OrderDate
FROM Orders o
JOIN Product p ON o.Product_id = p.Product_id
JOIN Customer c ON o.Customer_id = c.Customer_id
ORDER BY o.OrderDate;
```

```text
| PRODUCT_NAME    | CUSTOMER_NAME   | ORDERDATE |
|----------------|------------------|-----------|
| Headphones     | Michael Brown    | 20-JAN-20 |
| Bookshelf      | Sarah Davis      | 14-FEB-20 |
| 4K TV          | David Wilson     | 08-MAR-20 |
| Microwave      | John Smith       | 22-APR-20 |
| Gaming Console | Emily Johnson    | 30-MAY-20 |
| ...            | ...              | ...       |
```

---

## 9. 📆 Orders from Three Months Ago

```sql
SELECT * FROM Orders
WHERE OrderDate BETWEEN 
    ADD_MONTHS(TRUNC(SYSDATE, 'MONTH'), -3) 
    AND 
    ADD_MONTHS(TRUNC(SYSDATE, 'MONTH'), -2);
```

> ⚠️ *Note: Results depend on the current system date.*

---

## 10. ❌ Customers Who Never Ordered

```sql
SELECT c.Customer_id
FROM Customer c
LEFT JOIN Orders o ON c.Customer_id = o.Customer_id
WHERE o.Customer_id IS NULL;
```

```text
CUSTOMER_ID
-----------
6
7
```

