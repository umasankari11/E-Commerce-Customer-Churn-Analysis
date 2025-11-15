# E-Commerce Customer Churn Analysis

## 📌 Project Overview

Customer churn is a major concern for e-commerce platforms. This project analyzes churn behavior using historical transactional and behavioral data. It evaluates demographics, order patterns, payment preferences, complaints, and satisfaction to uncover key churn drivers and actionable retention strategies.

## 🎯 Objectives

* Clean and prepare the dataset for analysis.
* Handle missing values, inconsistencies, and outliers.
* Transform and standardize data (new columns, renaming, categorization).
* Analyze customer churn behavior, payment preferences, complaints, and category choices.
* Perform dataset-wide EDA using SQL.
* Create and integrate additional tables (like `customer_returns`).
* Generate insights for business decision-making.

## 🧰 Tools & Technologies Used

* **MySQL / SQL Workbench** for cleaning, transformation, and analysis.
* **E-Commerce Database** containing `customer_churn` and `customer_returns` tables.
* SQL techniques such as: joins, CASE statements, aggregations, nested queries, and conditional logic.

## 📁 Key SQL Operations Used

* `UPDATE` with subqueries
* `CASE` statements
* `GROUP BY` + aggregates
* `ORDER BY`
* Subqueries for average-based filtering
* Conditional aggregations
* Table joins (inner + left joins)

## 🔁 Project Workflow

1. **Data Import** – Load the CSV into MySQL.
2. **Data Cleaning** – Fix missing values, outliers, and inconsistencies.
3. **Data Transformation** – New fields & standardized columns.
4. **EDA (Exploratory Data Analysis)** – Run SQL analytical queries.
5. **Feature Engineering** – Distance segmentation, churn labels.
6. **Table Creation & Joins** – Create `customer_returns` table and join it.
7. **Insights & Reporting** – Identify churn drivers and retention strategies.

---

## 🧹 Step 1: Data Cleaning

### **1.1 Handling Missing Values**

**Mean Imputation (rounded)** for:

* WarehouseToHome
* HoursSpentOnApp
* OrderAmountHikeFromlastYear
* DaySinceLastOrder

**Mode Imputation** for:

* Tenure
* CouponUsed
* OrderCount

### **1.2 Handling Outliers**

* Removed rows where `WarehouseToHome > 100` using `CustomerID` for controlled deletion.

---

## 🔄 Step 2: Data Standardization

### **2.1 Replacing inconsistent values**

* `Phone` → `Mobile Phone`
* `Mobile` → `Mobile Phone`

### **2.2 Standardizing Payment Mode**

* `COD` → `Cash on Delivery`
* `CC` → `Credit Card`

### **2.3 Renaming Columns**

* `PreferedOrderCat` → `PreferredOrderCat`
* `HourSpendOnApp` → `HoursSpentOnApp`

---

## 🏗 Step 3: Feature Engineering

### **3.1 New Columns Created**

* `ComplaintReceived` → Yes/No based on complaint flag
* `ChurnStatus` → Churned/Active

### **3.2 Distance Segmentation (CASE)**

* Very Close Distance (<=5 km)
* Close Distance (<=10 km)
* Moderate Distance (<=15 km)
* Far Distance (>15 km)

---

## 📊 Step 4: Exploratory Data Analysis (SQL Queries)

### ✔ **Churn Analysis**

* Churned vs active customer count
* % of churned customers who complained
* Churn breakdown by distance category

### ✔ **Customer Behavior Insights**

* Avg tenure & cashback for churned customers
* Most preferred payment mode among active users
* Gender distribution of complaining customers
* City tier with highest customer count
* Category preference for high-coupon users (>5 coupons)

### ✔ **Category & Order Insights**

* Top 3 categories by average cashback
* Customers whose order count > overall average
* Preferred category for mobile phone users

### ✔ **Device & Satisfaction Insights**

* Avg devices registered by UPI users
* Avg satisfaction score among customers who complained

---

## 🗃 Step 5: Additional Tables

### **Customer Returns Table**

A separate table `customer_returns` was created in the e-commerce database to store return histories.

### **Joining Churn & Return Data**

Useful to extract:

* Churned customers
* Who also complained
* Who also returned products

---

## 📝 SQL Code Samples

### **1. Handling Missing Values**

```sql
UPDATE customer_churn
SET HoursSpentOnApp = (
    SELECT ROUND(AVG(HoursSpentOnApp)) FROM customer_churn
)
WHERE HoursSpentOnApp IS NULL;
```

### **2. Categorizing Data**

```sql
CASE
    WHEN WarehouseToHome <= 5 THEN 'Very Close Distance'
    WHEN WarehouseToHome <= 10 THEN 'Close Distance'
    WHEN WarehouseToHome <= 15 THEN 'Moderate Distance'
    ELSE 'Far Distance'
END
```

### **3. Joining Tables**

```sql
SELECT cc.*, cr.*
FROM customer_churn cc
JOIN customer_returns cr
ON cc.CustomerID = cr.CustomerID;
```

---

## 📌 Conclusion

This project showcases a full SQL-based churn analytics workflow — from cleaning and transformation to deep behavioral and churn analysis. The insights help identify:

* Major churn drivers
* Complaint and satisfaction patterns
* Preferred categories & payment modes
* City-tier distribution
* High-value customer segments

It demonstrates strong command of SQL querying, dataset preparation, segmentation logic, and analytical reporting.
