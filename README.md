# BlinkIT Grocery Sales Analysis using MySQL

## Project Overview
This project focuses on analyzing BlinkIT grocery sales data using MySQL.
The dataset was cleaned, transformed, and analyzed using SQL queries 
to generate business insights related to sales performance, 
outlet performance, item categories, customer ratings, and inventory trends.
	
## The goal of this project is to demonstrate:
SQL data cleaning skills
Data aggregation techniques
Business KPI analysis
Analytical thinking using MySQL

## Database Used
MySQL 8.0

## Dataset Information
Item Fat Content
Item Identifier	Item Type
Outlet Establishment Year
Outlet Identifier
Outlet Location Type
Outlet Size
Outlet Type
Item Visibility
Item Weight
Total Sales
Rating


## Database Creation

create database blinkit;
use blinkit;

## Table Structure

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


## Data Import

LOAD DATA INFILE 'C:/ProgramData/MySQL/MySQL Server 8.0/Uploads/BlinkIT Grocery Data.csv'
INTO TABLE blinkit_data
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS
(
  Item_Fat_Content,
  Item_Identifier,
  Item_Type,
  Outlet_Establishment_Year,
  Outlet_Identifier,
  Outlet_Location_Type,
  Outlet_Size,
  Outlet_Type,
  Item_Visibility,
  @Item_Weight,
  @Total_Sales,
  Rating
)
SET
Item_Weight = NULLIF(@Item_Weight, ''),
Total_Sales = NULLIF(REPLACE(@Total_Sales, ',', ''), '');


## Data Cleaning Performed

UPDATE blinkit_data
SET Item_Fat_Content = 
    CASE 
        WHEN Item_Fat_Content IN ('LF', 'low fat') THEN 'Low Fat'
        WHEN Item_Fat_Content = 'reg' THEN 'Regular'
        ELSE Item_Fat_Content
    END;


# Key Business KPIs Analyzed

1. Total Sales in Millions

select concat(cast(sum(total_sales)/1000000 as decimal(10,2)),' ','Million') as Total_Sales_Millions
from blinkit_data;

2. Average Sales

select Cast(avg(total_sales) as decimal(10,0)) as Avg_Sales
from blinkit_data;

3.Number of Items

select count(*) as No_of_Items 
from blinkit_data;

4.Total Sales by Fat Content

select cast(sum(total_sales)/1000000
        as decimal(10,2))
            as Total_Sales_Millions
from blinkit_data
 where Item_Fat_Content = 'Low Fat';

5.Average_Rating
 select Cast(avg(Rating)
 as decimal(10,0)) 
 as Avg_Rating
from blinkit_data;

6.Item Fat Content-wise Sales Performance

select Item_Fat_Content,
cast(Sum(Total_Sales)as decimal(10,2)) as Total_Sales,
cast(avg(Total_Sales) as decimal(10,2)) as Avg_Sales,
count(*) as No_of_Items,
cast(avg(Rating) as decimal(10,2)) as Avg_Rating
from blinkit_data
group by Item_Fat_Content
order by Total_Sales Desc;

7.Sales Analysis by Item Fat Content (2022)

 select Item_Type,
cast(Sum(Total_Sales)as decimal(10,2)) as Total_Sales,
cast(avg(Total_Sales) as decimal(10,2)) as Avg_Sales,
count(*) as No_of_Items,
cast(avg(Rating) as decimal(10,2)) as Avg_Rating
from blinkit_data
group by Item_Type
order by Total_Sales desc
limit 5;

8.-- Total Sales by Outlet Location Type
select Outlet_Location_Type,
    cast(sum(Total_Sales)
       as decimal(10,2))
         as Total_Sales
from blinkit_data
group by Outlet_Location_Type
order by Total_Sales;

9. Fat Content by Outlet for Total Sales
SELECT Outlet_Type, 
CAST(SUM(Total_Sales) AS DECIMAL(10,2)) AS Total_Sales,
		CAST(AVG(Total_Sales) AS DECIMAL(10,0)) AS Avg_Sales,
		COUNT(*) AS No_Of_Items,
		CAST(AVG(Rating) AS DECIMAL(10,2)) AS Avg_Rating,
		CAST(AVG(Item_Visibility) AS DECIMAL(10,2)) AS Item_Visibility
FROM blinkit_data
GROUP BY Outlet_Type
ORDER BY Total_Sales DESC;

10. 4. Total Sales by Outlet Establishment
select Outlet_Type,
	cast(sum(Total_Sales) as decimal(10,2)) as Total_Sales,
		cast(avg(Total_Sales) as decimal(10,2)) as Item_Visibility
from blinkit_data
group by Outlet_Type
order by Total_Sales desc;


11. Sales percentage

select 
     Outlet_Size,
     cast(sum(Total_Sales) as decimal(10,2)) as Total_Sales,
     concat(cast(
         sum(Total_Sales) * 100.0/
          (select sum(Total_Sales) from blinkit_data)
         as decimal(10,2)),' ','%') as Sales_Percentage
from blinkit_data
group by Outlet_Size
order by Total_Sales;


12. Sales by Outlet Location:

select 
     Outlet_Location_Type,
     cast(sum(Total_Sales) as decimal(10,2)) as Total_Sales,
     cast(avg(Total_Sales) as decimal(10,2)) as Avg_Sales,
     COUNT(*) AS No_of_Items,
     cast(avg(Rating) AS DECIMAL(10,2)) AS Avg_Rating
from blinkit_data
group by Outlet_Location_Type
order by Total_Sales 

13.All Metrics by Outlet Type

select 
     Outlet_Type,
     cast(sum(Total_Sales) as decimal(10,2)) as Total_Sales,
     cast(avg(Total_Sales) as decimal(10,2)) as Avg_Sales,
     COUNT(*) AS No_of_Items,
     cast(avg(Rating) AS DECIMAL(10,2)) AS Avg_Rating
from blinkit_data
group by Outlet_Type
order by Total_Sales desc;











