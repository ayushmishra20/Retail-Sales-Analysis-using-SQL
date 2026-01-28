# Retail-Sales-Analysis-using-SQL

# 🛒 Retail Sales Analysis using SQL

## 📌 Project Overview

**Project Name**: Retail Sales Analysis using SQL  
**Skill Level**: Beginner  
**Database**: `p1_retail_db`

This project demonstrates how **SQL is used to analyze retail sales data** by performing database setup, data cleaning, exploratory data analysis (EDA), and business-focused queries.  
It was completed as part of my **SQL learning journey** to gain hands-on experience with real-world datasets.

---

## 🎯 Objectives

- Design and create a retail sales database  
- Clean and validate raw sales data  
- Perform exploratory data analysis using SQL  
- Answer real business questions using structured SQL queries  
- Build a portfolio-ready SQL project  

---

## 🗄 Database Design

### Database & Table Creation

```sql
CREATE DATABASE p1_retail_db;

CREATE TABLE retail_sales (
    transactions_id INT PRIMARY KEY,
    sale_date DATE,
    sale_time TIME,
    customer_id INT,
    gender VARCHAR(10),
    age INT,
    category VARCHAR(35),
    quantity INT,
    price_per_unit FLOAT,
    cogs FLOAT,
    total_sale FLOAT
);

#🧹 Data Cleaning & Exploration

The following checks were performed before analysis:

Total record count

Unique customer count

Distinct product categories

Identification and removal of null values

SELECT COUNT(*) FROM retail_sales;
SELECT COUNT(DISTINCT customer_id) FROM retail_sales;
SELECT DISTINCT category FROM retail_sales;


📊 Business Analysis & SQL Queries
1️⃣ Sales on a specific date
SELECT *
FROM retail_sales
WHERE sale_date = '2022-11-05';


2️⃣ Clothing sales with quantity ≥ 4 (Nov 2022)
SELECT *
FROM retail_sales
WHERE category = 'Clothing'
  AND TO_CHAR(sale_date, 'YYYY-MM') = '2022-11'
  AND quantity >= 4;

3️⃣ Total revenue and orders by category
SELECT 
    category,
    SUM(total_sale) AS total_revenue,
    COUNT(*) AS total_orders
FROM retail_sales
GROUP BY category;


4️⃣ Average customer age (Beauty category)
SELECT ROUND(AVG(age), 2) AS avg_age
FROM retail_sales
WHERE category = 'Beauty';

