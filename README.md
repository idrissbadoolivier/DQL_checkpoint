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
