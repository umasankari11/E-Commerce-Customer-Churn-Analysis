**📦 E-Commerce Customer Churn Analysis**

A complete SQL-based project for cleaning, transforming, and analyzing customer churn behavior in an e-commerce environment.

**📝 Project Overview**

Customer churn is a critical challenge for e-commerce platforms. This project analyzes churn behavior using transactional and behavioral customer data. Various attributes—demographics, order history, satisfaction score, complaints, payment methods, and distance—are explored to identify patterns that drive customer churn.

The goal is to uncover actionable insights to strengthen customer retention strategies.

**🎯 Objectives**

Clean and prepare raw customer data.

Handle missing values, outliers, and inconsistent entries.

Perform data transformation & feature engineering.

Conduct Exploratory Data Analysis (EDA) using SQL.

Create and join auxiliary tables (e.g., customer returns).

Generate churn insights and recommendations.

**🧰 Tools & Technologies**
Tool / Technology	Purpose
MySQL / SQL Workbench	Data cleaning, transformations, SQL queries
ecomm Database	Storage for customer_churn & customer_returns tables
SQL Joins, CASE, Aggregations	Analytical insights
Subqueries & Nested Queries	Advanced filtering & metrics
**🧹 Step 1: Data Cleaning
✔ 1.1 Handling Missing Values**

Mean Imputation

WarehouseToHome

HoursSpentOnApp

OrderAmountHikeFromlastYear

DaySinceLastOrder

Mode Imputation

Tenure

CouponUsed

OrderCount

**✔ 1.2 Handling Outliers**

Removed WarehouseToHome > 100 km using CustomerID for safe deletion.

**🔄 Step 2: Data Standardization**

Phone → Mobile Phone

Mobile → Mobile Phone

COD → Cash on Delivery

CC → Credit Card

**Column Renaming**

PreferedOrderCat → PreferredOrderCat

HourSpendOnApp → HoursSpentOnApp

**🏗 Step 3: Feature Engineering**
✔ New Columns Added
1. ComplaintReceived
CASE WHEN complain = 1 THEN 'Yes' ELSE 'No' END

2. ChurnStatus
CASE WHEN churn = 1 THEN 'Churned' ELSE 'Active' END

3. Distance Segmentation
CASE
  WHEN WarehouseToHome <= 5 THEN 'Very Close Distance'
  WHEN WarehouseToHome <= 10 THEN 'Close Distance'
  WHEN WarehouseToHome <= 15 THEN 'Moderate Distance'
  ELSE 'Far Distance'
END

**📊 Step 4: Exploratory Data Analysis (SQL)**

The project covers:

✔ Churn Insights

Churn count & percentage

Complaints among churned customers

Churn by distance segment

✔ Behavioral Insights

Average tenure & cashback by churn status

Preferred payment method of active users

Gender distribution of customers who complained

City tier analysis

✔ Category & Ordering Insights

Top 3 categories with highest average cashback

Customers with above-average order count

Category preference among mobile-phone shoppers

✔ Device & Satisfaction Insights

Avg registered devices for UPI users

Avg satisfaction score of complaining customers

**🗃 Step 5: Additional Tables**
✔ Created customer_returns Table

Contains return behavior details per customer.

✔ Joined With Churn Data

Combined churn + complaint + return data using:

SELECT cc.*, cr.*
FROM customer_churn cc
JOIN customer_returns cr 
     ON cc.CustomerID = cr.CustomerID;

**🧪 Sample SQL Snippets**
1. Handling Missing Values
UPDATE customer_churn
SET HoursSpentOnApp = (
    SELECT ROUND(AVG(HoursSpentOnApp)) 
    FROM customer_churn
)
WHERE HoursSpentOnApp IS NULL;

2. Categorization Using CASE
CASE
  WHEN WarehouseToHome <= 5 THEN 'Very Close Distance'
  WHEN WarehouseToHome <= 10 THEN 'Close Distance'
  WHEN WarehouseToHome <= 15 THEN 'Moderate Distance'
  ELSE 'Far Distance'
END

3. Joining Customer + Returns
SELECT cc.*, cr.*
FROM customer_churn cc
JOIN customer_returns cr 
  ON cc.CustomerID = cr.CustomerID;

**📌 Conclusion Summary**

This project demonstrates a complete SQL-driven approach to churn analysis, covering:

Data cleaning & transformations

Feature engineering

Exploratory analysis

Joins with additional tables

Insight generation for business decision-making

**⭐The insights:**
✔ Key churn drivers
✔ Complaint & satisfaction patterns
✔ Preferred categories & payment methods
✔ High-value and at-risk customer segments

