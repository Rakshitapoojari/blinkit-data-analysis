## 🚀 BlinkIT Grocery Sales Analysis using MySQL

# 📌 Project Overview
This project analyzes BlinkIT grocery sales data using MySQL 8.0 to generate meaningful business insights.

# The dataset was cleaned, transformed, and analyzed using SQL to understand:
Sales performance
Outlet performance
Product category trends
Customer ratings
Inventory behavior

# 🎯 Goal
To demonstrate strong SQL skills in:
Data cleaning
Data aggregation
KPI calculation
Business insight generation

# 🛠️ Tools & Technologies
MySQL 8.0

# 📂 Dataset Information
Columns used in the dataset:
Item Fat Content
Item Identifier
Item Type
Outlet Establishment Year
Outlet Identifier
Outlet Location Type
Outlet Size
Outlet Type
Item Visibility
Item Weight
Total Sales
Rating

# 🗄️ Database Setup
Create Database
CREATE DATABASE blinkit;
USE blinkit;

# Table Structure
CREATE TABLE blinkit_data (
    Item_Fat_Content VARCHAR(20),
    Item_Identifier VARCHAR(20),
    Item_Type VARCHAR(50),
    Outlet_Establishment_Year INT,
    Outlet_Identifier VARCHAR(20),
    Outlet_Location_Type VARCHAR(50),
    Outlet_Size VARCHAR(20),
    Outlet_Type VARCHAR(50),
    Item_Visibility DECIMAL(10,9),
    Item_Weight DECIMAL(10,3),
    Total_Sales DECIMAL(10,4),
    Rating DECIMAL(3,2)
);

# 🧹 Data Cleaning
Standardized inconsistent values in fat content:
UPDATE blinkit_data
SET Item_Fat_Content =
CASE
    WHEN Item_Fat_Content IN ('LF', 'low fat') THEN 'Low Fat'
    WHEN Item_Fat_Content = 'reg' THEN 'Regular'
    ELSE Item_Fat_Content
END;

## 📊 Key Business KPIs

# 💰 Total Sales
SELECT CONCAT(CAST(SUM(Total_Sales)/1000000 AS DECIMAL(10,2)), ' Million') 
AS Total_Sales_Millions
FROM blinkit_data;

# 📦 Total Items
SELECT COUNT(*) AS No_of_Items FROM blinkit_data;

# 📈 Average Sales
SELECT CAST(AVG(Total_Sales) AS DECIMAL(10,0)) AS Avg_Sales
FROM blinkit_data;

# ⭐ Average Rating
SELECT CAST(AVG(Rating) AS DECIMAL(10,0)) AS Avg_Rating
FROM blinkit_data;

# 📊 Business Insights
# 🧈 Sales by Item Fat Content
Compared Low Fat vs Regular products
Measured sales, rating, and item count

# 🏪 Outlet Performance
Sales by outlet type
Sales by outlet size
Sales by location type

# 🥫 Product Analysis
Top-performing item categories
Sales contribution by item type

# 🏆 Key Insights
Certain outlet types contribute significantly higher revenue
Medium/Large outlets perform better in total sales
Specific item categories dominate revenue contribution
Customer ratings help identify high-performing products

# 📊 Sample Analysis Queries
Sales by Outlet Type
SELECT Outlet_Type,
SUM(Total_Sales) AS Total_Sales,
AVG(Total_Sales) AS Avg_Sales,
COUNT(*) AS No_Of_Items,
AVG(Rating) AS Avg_Rating
FROM blinkit_data
GROUP BY Outlet_Type
ORDER BY Total_Sales DESC;

# 🚀 What This Project Demonstrates
✔ SQL data cleaning
✔ Aggregation & grouping
✔ Business KPI creation
✔ Analytical thinking
✔ Real-world retail analysis

# 📌 Future Improvements
Power BI dashboard visualization
Python-based advanced analytics
Predictive sales modeling
Automated reporting system

# 👩‍💻 Author
Rakshita Poojari
Aspiring Data Analyst
Skills: SQL | Excel | Data Visualization 
