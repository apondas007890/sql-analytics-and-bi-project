# Power BI Sales & Logistics Dashboard

An interactive Power BI report built on clean **Gold Layer** data from a data warehouse project I built end-to-end. It covers sales performance, product trends, customer demographics, and shipping logistics — all in one executive-ready dashboard.

🔗 **Data Warehouse Project:** [sql-data-warehouse-project](https://github.com/apondas007890/sql-data-warehouse-project)

---

## 📌 What This Project Shows

- A proper **star schema** (fact + dimension tables)
- **DAX measures** for KPIs, time intelligence, and profitability
- **Power Query** transformations for data cleaning
- A report designed for executives, product teams, and logistics

---

## 🛠️ Data Preparation (Power Query)

The data came from my [SQL data warehouse project](https://github.com/apondas007890/sql-data-warehouse-project) (Bronze → Silver → Gold), then was refined further in Power Query:

| Table | What was done |
|---|---|
| `dim_customers` | Merged first + last name into `customer_name`, trimmed whitespace, formatted `birthdate` |
| `dim_products` | Replaced blanks/nulls with `"Unknown"`, trimmed text, formatted `start_date` |
| `fact_sales` | Formatted `order_date`, `shipping_date`, `due_date` |
| `dim_date` | Created a calendar table in DAX: `CALENDAR(DATE(2010,1,1), DATE(2014,12,31))` |


## 📊 Key DAX Measures

All measures live in a dedicated `_Measures` table.

```dax
Total Sales           = SUM(fact_sales[sales_amount])
Total Orders          = DISTINCTCOUNT(fact_sales[order_number])
Total Quantity        = SUM(fact_sales[quantity])
Total Customers       = DISTINCTCOUNT(fact_sales[customer_key])

Avg Order Value       = DIVIDE([Total Sales], [Total Orders])
Total Cost            = SUMX(fact_sales, RELATED(dim_products[cost]) * fact_sales[quantity])
Gross Profit          = [Total Sales] - [Total Cost]
Profit Margin %       = DIVIDE([Gross Profit], [Total Sales])

Sales LY              = CALCULATE([Total Sales], SAMEPERIODLASTYEAR(dim_date[Date]))
Sales YoY %           = DIVIDE([Total Sales] - [Sales LY], [Sales LY])

Avg Shipping Days     = AVERAGEX(fact_sales, INT(fact_sales[shipping_date] - fact_sales[order_date]))
Total Shipping Volume = SUM(fact_sales[quantity])
```
---

## 📱 Report Pages

### 1. Sales Overview
High-level KPIs, revenue trend vs. last year, sales by category, and revenue split by country.

![Sales Overview](Images/Sales%20Overview.jpg)

### 2. Product Performance
Top 10 products, cost vs. sales by category, quantity by subcategory, and a product detail matrix.

![Product Performance](Images/Product%20Performance.jpg)

### 3. Customer Insights
Age & gender breakdown, marital status share, customers by country, and a Top 20 customer table.

![Customer Insights](Images/Customer%20Insights.jpg)

### 4. Fulfillment & Shipping
Average shipping days, total shipping volume, regional shipping timelines, and monthly order trends.

![Fulfillment & Shipping](Images/Fulfillment%20&%20Shipping%20Analytics.jpg)

---

📁 Repository Structure
```
text
├── Datasets/
│   ├── gold.dim_customers.csv
│   ├── gold.dim_products.csv
│   └── gold.fact_sales.csv
│
├── Images/
│   ├── Sales Overview.jpg
│   ├── Product Performance.jpg
│   ├── Customer Insights.jpg
│   └── Fulfillment & Shipping Analytics.jpg
│
└── PowerBI/
    └── project_first.pbix
```

---

🧰 Tools Used
SQL — data warehouse (Bronze → Silver → Gold)

Power Query — cleaning & shaping

DAX — measures & time intelligence

Power BI Desktop — semantic model + report
