# E-Commerce-Customer-Churn-Analysis
**Project Overview**

Customer churn is a key challenge for e-commerce businesses. This project analyzes churn behavior using historical transactional data. Various customer attributes such as demographics, order behavior, payment preferences, satisfaction score, and complaint history are used to identify churn patterns. The aim is to generate actionable insights to improve retention strategies.

**Objectives**

Clean and prepare the dataset for analysis.

Handle missing values, outliers, inconsistencies.

Transform data (new columns, renaming, standardization).

Analyze customer behavior (churn patterns, complaints, payment modes, category preferences).

Perform exploratory data analysis (EDA) using SQL.

Create additional tables (e.g., customer_returns) and join with main dataset.

**Tools Used**

MySQL / SQL Workbench – Data cleaning, transformation, querying

ecomm Database – Storage for customer_churn and customer_returns tables

SQL Joins & Aggregations – For detailed customer-return analysis

CASE Statements – Categorization (e.g., distance-based segmentation)

Subqueries & Nested Queries – For advanced filtering (average-based filtering)

**Key SQL Operations Used**

UPDATE with subqueries

CASE statements

GROUP BY with aggregates

ORDER BY sorting

Subqueries for average calculations

Conditional aggregations

JOIN operations (customer + returns)

**Project Workflow**

Data Import – Load CSV into the MySQL database.

Data Cleaning – Handle missing values, outliers, and inconsistencies.

Data Transformation – Create new fields and rename columns.

Exploratory Data Analysis (EDA) – Run analytical SQL queries.

Feature Engineering – Add segmentation (distance categories, churn labels).

Table Creation & Joins – Build customer_returns table and join with main data.

Insights & Reporting – Deliver churn insights and retention recommendations.

🧹 Step 1: Data Cleaning
1.1 Handling Missing Values

Imputed mean (rounded) for:

WarehouseToHome

HoursSpentOnApp

OrderAmountHikeFromlastYear

DaySinceLastOrder

Imputed mode for:

Tenure

CouponUsed

OrderCount

1.2 Handling Outliers

Removed rows where WarehouseToHome > 100 using CustomerID for safe deletion.

🔄 Step 2: Data Standardization
2.1 Replacing inconsistent values

PreferredLoginDevice: "Phone" → "Mobile Phone"

PreferredOrderCat: "Mobile" → "Mobile Phone"

2.2 Standardizing payment mode

COD → "Cash on Delivery"

CC → "Credit Card"

2.3 Renaming Columns

PreferedOrderCat → PreferredOrderCat

HourSpendOnApp → HoursSpentOnApp

🏗 Step 3: Feature Engineering
3.1 New Columns

ComplaintReceived: Yes/No based on complain flag.

ChurnStatus: Churned/Active based on churn flag.

Distance segmentation using CASE:

Very Close Distance (<=5 km)

Close Distance (<=10 km)

Moderate Distance (<=15 km)

Far Distance (>15 km)

📊 Step 4: Exploratory Data Analysis (SQL Queries)

Below are the major analytical questions answered using SQL:

✔ Churn Analysis

Count of churned vs active customers.

Percentage of churned customers who complained.

Churn breakdown by distance category.

✔ Customer Behavior Insights

Average tenure and cashback for churned customers.

Preferred payment mode among active customers.

Gender distribution of customers who complained.

City tier with highest number of customers.

Category preference for high coupon users (>5 coupons).

✔ Category & Order Insights

Top 3 categories with highest average cashback.

Customers whose order count is above overall average.

Preferred order category for mobile phone users.

✔ Device & Satisfaction Insights

Avg devices registered by UPI users.

Avg satisfaction score of customers who complained.

🗃 Step 5: Additional Tables
Customer Returns Table

A separate table customer_returns was created in the ecomm database with return details.

Joining Churn & Return Data

A detailed join query was written to fetch customer + return details for customers who:

Have churned

Have complained

Have return records

📝 SQL Code Samples

Below are examples of common SQL patterns used throughout the project:

1. Handling Missing Values
UPDATE customer_churn
SET HoursSpentOnApp = (SELECT ROUND(AVG(HoursSpentOnApp)) FROM customer_churn)
WHERE HoursSpentOnApp IS NULL;
2. Categorizing Data
CASE
  WHEN WarehouseToHome <= 5 THEN 'Very Close Distance'
  WHEN WarehouseToHome <= 10 THEN 'Close Distance'
  WHEN WarehouseToHome <= 15 THEN 'Moderate Distance'
  ELSE 'Far Distance'
END
3. Joining Tables
   SELECT cc.*, cr.*
FROM customer_churn cc
JOIN customer_returns cr ON cc.CustomerID = cr.CustomerID;

📌 Conclusion

This project provides a complete SQL-based approach to cleaning, transforming, and analyzing customer churn data. The insights help identify:

Drivers of churn

Behavioral patterns (complaints, category preference, payment modes)

City-tier distribution

High-value customer segments

It also demonstrates strong proficiency in SQL operations such as joins, transformations, aggregations, and EDA logic.

