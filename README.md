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
```

## 🧹 Data Cleaning & Exploration

- The following checks were performed before analysis:
- Total record count
- Unique customer count
- Distinct product categories
- Identification and removal of null values

```sql
SELECT COUNT(*) FROM retail_sales;
SELECT COUNT(DISTINCT customer_id) FROM retail_sales;
SELECT DISTINCT category FROM retail_sales;
```

## 📊 Business Analysis & SQL Queries
1️⃣ Sales on a specific date
```sql
SELECT *
FROM retail_sales
WHERE sale_date = '2022-11-05';
```

2️⃣ Clothing sales with quantity ≥ 4 (Nov 2022)
```sql
SELECT *
FROM retail_sales
WHERE category = 'Clothing'
  AND TO_CHAR(sale_date, 'YYYY-MM') = '2022-11'
  AND quantity >= 4;
```


3️⃣ Total revenue and orders by category
```sql
SELECT 
    category,
    SUM(total_sale) AS total_revenue,
    COUNT(*) AS total_orders
FROM retail_sales
GROUP BY category;
```

4️⃣ Average customer age (Beauty category)
```sql
SELECT ROUND(AVG(age), 2) AS avg_age
FROM retail_sales
WHERE category = 'Beauty';
```

5️⃣ High-value transactions (sales > 1000)
```sql
SELECT *
FROM retail_sales
WHERE total_sale > 1000;
```

6️⃣ Transactions by gender and category
```sql
SELECT 
    category,
    gender,
    COUNT(*) AS transaction_count
FROM retail_sales
GROUP BY category, gender
ORDER BY category;
```

7️⃣ Best-selling month of each year
```sql
SELECT year, month, avg_sale
FROM (
    SELECT 
        EXTRACT(YEAR FROM sale_date) AS year,
        EXTRACT(MONTH FROM sale_date) AS month,
        AVG(total_sale) AS avg_sale,
        RANK() OVER (
            PARTITION BY EXTRACT(YEAR FROM sale_date)
            ORDER BY AVG(total_sale) DESC
        ) AS rank
    FROM retail_sales
    GROUP BY 1, 2
) ranked_sales
WHERE rank = 1;
```

8️⃣ Top 5 customers by total sales
```sql
SELECT 
    customer_id,
    SUM(total_sale) AS total_sales
FROM retail_sales
GROUP BY customer_id
ORDER BY total_sales DESC
LIMIT 5;
```


9️⃣ Unique customers per category
```sql
SELECT 
    category,
    COUNT(DISTINCT customer_id) AS unique_customers
FROM retail_sales
GROUP BY category;
```

🔟 Sales by shift (Morning / Afternoon / Evening)
```sql
WITH sales_shift AS (
    SELECT *,
        CASE
            WHEN EXTRACT(HOUR FROM sale_time) < 12 THEN 'Morning'
            WHEN EXTRACT(HOUR FROM sale_time) BETWEEN 12 AND 17 THEN 'Afternoon'
            ELSE 'Evening'
        END AS shift
    FROM retail_sales
)
SELECT shift, COUNT(*) AS total_orders
FROM sales_shift
GROUP BY shift;
```

## 🔍 Key Insights

- Sales are distributed across multiple product categories
- Clothing and Beauty categories show strong performance
- High-value transactions significantly impact total revenue
- Certain months record peak sales activity
- Evening shift records the highest number of orders

## 📚 Skills Practiced

- SQL Data Cleaning
- Aggregation & Grouping
- Window Functions
- Date & Time Analysis
- Business-Oriented Querying


## 🙌 Credits & Acknowledgment

This project is inspired by a public SQL learning project created by Zero Analyst (Najir H).
Original repository:
https://github.com/najirh/Retail-Sales-Analysis-SQL-Project--P1

This version is recreated and modified by me for educational and practice purposes.

## 👤 Author

Ayush Mishra
