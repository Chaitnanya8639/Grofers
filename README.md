# Grofers Database System

## Overview

This project implements a comprehensive database system for a Grofers-like application. It includes entities for employees, products, customers, orders, and geographical locations, with well-defined relationships, constraints, and optimized performance features.

## Features

### 1. **Entities and Tables**

- **Employee Table**: Stores employee details like name, department, grade, age, and salary.
- **Department Table**: Contains department information, linked with employees.
- **Product Tables**: Covers products, product groups, old products, and imported products.
- **Customer Table**: Stores customer details such as credit rating and location.
- **Order and Order Details Tables**: Manages order tracking and product quantities.
- **Geographical Tables**: Includes states and cities, linked to customers.

### 2. **Key Database Components**

- **Constraints**: Defined primary keys, foreign keys, and unique constraints to ensure data integrity.
- **Procedures**: Includes reusable procedures for operations like:
  - Assigning employee managers.
  - Adding new departments and product groups.
  - Querying employee details.
  - Fetching imported product data.
- **Functions**: Implements business logic like:
  - Retrieving products above a certain price.
  - Calculating total customer orders.
  - Determining actual sales prices after removing profit margins.
  - Counting products in a product group.
- **Packages**: Groups procedures and functions for tasks like counting employees per department and identifying the most purchased product.

### 3. **Performance Enhancements**

- **Indexes**: Created on frequently queried columns (e.g., employee names, order details) to improve query efficiency.
- **Views**: Simplified data access through predefined views for employees, products, and orders.
- **Sequences**: Used for auto-generating unique identifiers for key fields like customer codes and order numbers.

## How to Use

1. **Database Setup**:
   - Create tables using the provided SQL scripts.
   - Define constraints, relationships, and indexes for optimized performance.
2. **Data Population**:
   - Use sequences for unique ID generation.
   - Insert sample data as demonstrated in the scripts.
3. **Query Execution**:
   - Run predefined queries to analyze data, such as finding employees with high salaries or fetching product sales details.
4. **Procedures and Functions**:
   - Execute procedures to automate tasks like adding departments or querying product details.
   - Call functions to calculate metrics like total orders or profit margins.
5. **Performance Tuning**:
   - Leverage indexes and analyze query performance using tools like `EXPLAIN PLAN`.

## Key SQL Highlights

- **Procedures**:
  ```sql
  CREATE OR REPLACE PROCEDURE add_dept(dcode VARCHAR2, dname VARCHAR2) AS
  BEGIN
      INSERT INTO depttable VALUES (deptid.NEXTVAL, dcode, dname);
      DBMS_OUTPUT.PUT_LINE('Added department: ' || dcode || ', ' || dname);
  END;
  ```
- **Functions**:
  ```sql
  CREATE OR REPLACE FUNCTION prod(price NUMBER) RETURN NUMBER AS
      CURSOR c1 IS SELECT profit_margin, brand_name FROM prodtable WHERE sale_price > price;
      margin prodtable.profit_margin%TYPE;
      brand prodtable.brand_name%TYPE;
  BEGIN
      OPEN c1;
      LOOP
          FETCH c1 INTO margin, brand;
          EXIT WHEN c1%NOTFOUND;
          DBMS_OUTPUT.PUT_LINE(margin || ', ' || brand);
      END LOOP;
      CLOSE c1;
      RETURN margin;
  END;
  ```
- **Views**:
  ```sql
  CREATE OR REPLACE VIEW v_emp AS
      SELECT emp_code, emp_name, dept_code FROM emptable;
  ```

## Done By

- J. Chaitanya Venkata Sai Narayana


