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
(2, 110, '2020-05-30', 1, 14999.99);
