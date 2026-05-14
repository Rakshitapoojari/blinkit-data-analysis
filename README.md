# 🛒 BlinkIT Grocery Sales Analysis (MySQL Project)

## 📌 Project Overview

This project focuses on analyzing **BlinkIT grocery sales data** using **MySQL** to extract meaningful business insights.

The dataset was cleaned, transformed, and analyzed to understand:

* Sales performance trends
* Outlet performance comparison
* Product category analysis
* Customer rating behavior
* Inventory and visibility patterns

The goal of this project is to demonstrate **real-world SQL analytics skills** for business decision-making.

---

## 🎯 Key Objectives

* Clean and standardize raw dataset using SQL
* Perform exploratory data analysis using aggregations
* Build KPIs for business performance tracking
* Identify high-performing outlets and product categories
* Generate actionable business insights

---

## 🛠️ Tools & Technologies Used

* MySQL 8.0
* SQL (Data Cleaning + Analysis)

---

## 📂 Dataset Information

The dataset contains grocery sales information including:

* Item Fat Content
* Item Identifier
* Item Type
* Outlet Type
* Outlet Size
* Outlet Location Type
* Item Weight
* Item Visibility
* Total Sales
* Customer Rating

---

## 🧹 Data Cleaning Process

Key cleaning steps performed:

* Standardized inconsistent values in `Item_Fat_Content`
* Handled missing values using NULL conversion
* Cleaned numeric fields during data import

```sql
UPDATE blinkit_data
SET Item_Fat_Content =
CASE
    WHEN Item_Fat_Content IN ('LF', 'low fat')
    THEN 'Low Fat'
    WHEN Item_Fat_Content = 'reg'
    THEN 'Regular'
    ELSE Item_Fat_Content
END;
```

---

## 📊 Key Business KPIs

### 💰 Total Sales

* Overall revenue generated from all items

### 📦 Total Items Sold

* Total number of transactions/items in dataset

### 📈 Average Sales

* Average revenue per transaction

### ⭐ Average Rating

* Customer satisfaction indicator

---

## 🏪 Business Insights Derived

### 1. Outlet Performance Analysis

* Compared sales across outlet types and sizes
* Identified high-performing outlet categories

### 2. Product Category Analysis

* Found top-performing item types based on revenue
* Identified low-performing categories

### 3. Fat Content Analysis

* Compared Low Fat vs Regular product sales behavior

### 4. Location-based Insights

* Evaluated performance across different outlet locations

---

## 🧠 Key Insights

* Certain outlet types contribute significantly higher revenue
* Medium/Large outlets perform better in overall sales
* Specific product categories dominate total revenue
* Customer ratings help identify high-demand products
* Outlet location plays a key role in performance differences

---

## 📊 Sample SQL Analysis

Example: Sales by Outlet Type

```sql
SELECT Outlet_Type,
SUM(Total_Sales) AS Total_Sales,
AVG(Total_Sales) AS Avg_Sales,
COUNT(*) AS No_Of_Items,
AVG(Rating) AS Avg_Rating
FROM blinkit_data
GROUP BY Outlet_Type
ORDER BY Total_Sales DESC;
```

---

## 🚀 What This Project Demonstrates

✔ SQL Data Cleaning
✔ Data Aggregation & Grouping
✔ Business KPI Development
✔ Analytical Thinking
✔ Real-world Retail Data Analysis

---

## 📈 Future Improvements

* Build Power BI dashboard for visualization
* Add Python-based EDA layer
* Perform predictive sales analysis
* Automate reporting pipeline

---

## 👩‍💻 Author

**Rakshita Poojari**
Aspiring Data Analyst
Skills: SQL | Excel | Power BI | Data Visualization
