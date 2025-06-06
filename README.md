
# 📊 Superstore Sales Dataset Analysis

## 👥 Team Members
- Anas Alaa  
- Mahmoud Hossam  
- Omar Mohamed  
- Menna Tallah Mahmoud  
- Mohamed Haytham  
- Abdelrahman Ibrahim  

---

## 📁 Data Source
Provided by DEPI  
[Link to Dataset](https://drive.google.com/file/d/1QE_uoS8Aywd7ZFhmMvDmVf7jf0XN6mhw/view?usp=sharing)
## 📁 Link of project
https://drive.google.com/drive/folders/1MrjqMPDy4m0gnn5LhBdJRRLggc7VoJ7d?usp=drive_link

---

## 🎯 Project Objective

This project analyzes sales data to answer the following business questions:

1. 💰 What is the total sales revenue generated by the store?  
2. 📦 How many orders were placed?  
3. 👤 How many unique customers made purchases?  
4. 💳 What is the average sales per order?  
5. 📅 What is the average monthly sales?  
6. 🛍️ Which categories and sub-categories generated the highest sales?  
7. 🏅 Who are the top customers in terms of sales?  
8. 🌎 Which regions and states contributed most to the sales?  
9. 🚚 How were sales distributed across different shipping modes?  
10. 👥 How did sales perform across customer segments?

---

## 🧹 Data Cleaning Steps

1. Removed null values  
2. Removed duplicate rows  
3. Removed "Country" column (only one country present)  
4. Converted `Order Date` and `Ship Date` columns to date format  
5. Changed ID column types to integer  

---

## 🧮 DAX Measures & Calculations

### 📆 Calendar Table:
```DAX
CalendarTable = 
ADDCOLUMNS (
    CALENDAR (MINX (Sales, Sales[OrderDate]), MAXX (Sales, Sales[OrderDate])),
    "Year", YEAR([Date]),
    "Month", FORMAT([Date], "MMMM"),
    "Month Number", MONTH([Date]),
    "Quarter", "Q" & FORMAT([Date], "Q"),
    "Weekday", FORMAT([Date], "dddd"),
    "Weekday Number", WEEKDAY([Date])
)
```

### 📐 Calculated Measures:
```DAX
1. Avg Sales per Order = [Total Sales] / DISTINCTCOUNT('Superstore Sales Dataset'[Order ID])

2. Monthly Sales = TOTALMTD([Total Sales], 'Superstore Sales Dataset'[Order Date])

3. Sales Year Growth = 
VAR CurrentYearSales = [Total Sales]
VAR PreviousYearSales = CALCULATE([Total Sales], SAMEPERIODLASTYEAR('Superstore Sales Dataset'[Order Date]))
RETURN IF(
    NOT ISBLANK(PreviousYearSales),
    (CurrentYearSales - PreviousYearSales) / PreviousYearSales,
    BLANK()
)

4. Total Orders = COUNT('Superstore Sales Dataset'[Order ID])

5. Total Sales = SUM('Superstore Sales Dataset'[Sales])

6. Unique Customers = DISTINCTCOUNT('Superstore Sales Dataset'[Customer ID])
```

---

## 📊 Key Insights

- **Total Sales Revenue**: $2.26M  
- **Total Orders Placed**: 9,800  
- **Unique Customers**: 793  
- **Average Sales per Order**: $459.48  
- **Average Monthly Sales**: ~$83K  

---

## ✅ Recommendations

1. **Optimize High-Performing Categories**  
   Focus on **Furniture** and **Office Supplies** categories that contribute 65% of revenue.

2. **Target Top Customers**  
   Launch loyalty programs for the top 10 customers who contributed over **$420K** in sales.

3. **Improve Underperforming Regions**  
   Analyze low sales in the **Central region** and consider targeted marketing campaigns.

4. **Enhance Shipping Experience**  
   Reduce dependency on **Standard Class** shipping (average 5-day delay). Promote **First Class** for faster delivery.

5. **Boost Consumer Segment Growth**  
   Introduce discounts and promotions for the **Consumer** segment to increase its contribution.

---

> _“Great insights drive great decisions.”_

