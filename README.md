# 📝 Assignment: Database Design and Normalization

## 🎯 **Learning Objectives**
* 🛠️ **Understand the principles of good database design** and **normalization**.
* 💡 **Apply normalization techniques** to improve database structure and efficiency.
* 🔍 **Learn First, Second, and Third Normal Forms** (1NF, 2NF, 3NF) to eliminate redundancy and optimize data storage.

---

## 📋 **What You'll Need**
* 💻 A computer with internet access.
* ✍️ A code editor (e.g., Visual Studio Code).
* 🖥️ MySQL Workbench or another SQL database environment.

---


## 📝 Submission Instructions  
📂 Write all your SQL queries in the **answers.sql** file.  
✍️ Answer each question concisely and make sure your queries are clear and correct.  
🗣️ Structure your responses clearly, and use comments if necessary to explain your approach.

--- 

## 📚 Assignment Questions

---

### Question 1 Achieving 1NF (First Normal Form) 🛠️
Task:
- You are given the following table **ProductDetail**:

| OrderID | CustomerName  | Products                        |
|---------|---------------|---------------------------------|
| 101     | John Doe      | Laptop, Mouse                   |
| 102     | Jane Smith    | Tablet, Keyboard, Mouse         |
| 103     | Emily Clark   | Phone                           |


- In the table above, the **Products column** contains multiple values, which violates **1NF**.
- **Write an SQL query** to transform this table into **1NF**, ensuring that each row represents a single product for an order
```sql
CREATE DATABASE store;

USE store;
CREATE TABLE orders(
order_id INT PRIMARY KEY AUTO_INCREMENT,
first_name VARCHAR(30),
second_name VARCHAR(30));

INSERT INTO orders(order_id, first_name, second_name) 
VALUES (101, "John", "Doe"), (102 , "Jane", "Smith"),
(103, "Emily", "Clark");

SELECT * FROM orders;

CREATE TABLE products(
product_id INT PRIMARY KEY AUTO_INCREMENT,
product_name VARCHAR(30),
order_id INT,
FOREIGN KEY (order_id) REFERENCES orders(order_id));

INSERT INTO products(product_name, order_id) 
VALUES ("Laptop", 101), ("Mouse", 101),
("Tablet", 102), ("Keyboard", 102), ("Mouse", 102),
("Phone", 103);

SELECT * FROM products;
```
--- 

### Question 2 Achieving 2NF (Second Normal Form) 🧩

- You are given the following table **OrderDetails**, which is already in **1NF** but still contains partial dependencies:

| OrderID | CustomerName  | Product      | Quantity |
|---------|---------------|--------------|----------|
| 101     | John Doe      | Laptop       | 2        |
| 101     | John Doe      | Mouse        | 1        |
| 102     | Jane Smith    | Tablet       | 3        |
| 102     | Jane Smith    | Keyboard     | 1        |
| 102     | Jane Smith    | Mouse        | 2        |
| 103     | Emily Clark   | Phone        | 1        |

- In the table above, the **CustomerName** column depends on **OrderID** (a partial dependency), which violates **2NF**. 

- Write an SQL query to transform this table into **2NF** by removing partial dependencies. Ensure that each non-key column fully depends on the entire primary key.
```sql
USE store;
DROP TABLE products;
DROP TABLE orders;

CREATE TABLE orders(
order_id INT PRIMARY KEY AUTO_INCREMENT,
first_name VARCHAR(30),
second_name VARCHAR(30));

INSERT INTO orders(order_id, first_name, second_name) 
VALUES (101, "John", "Doe"), (102 , "Jane", "Smith"),
(103, "Emily", "Clark");

SELECT * FROM orders;

CREATE TABLE products(
product_id INT PRIMARY KEY AUTO_INCREMENT,
product_name VARCHAR(30),
quantity INT,
order_id INT,
FOREIGN KEY (order_id) REFERENCES orders(order_id));

INSERT INTO products(product_name, order_id, quantity) 
VALUES ("Laptop", 101, 2), ("Mouse", 101, 1),
("Tablet", 102, 3), ("Keyboard", 102, 1), ("Mouse", 102, 2),
("Phone", 103, 1);

SELECT * FROM products;
```
---
Good luck 🚀
