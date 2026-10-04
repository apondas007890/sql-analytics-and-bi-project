# 🔍 Exploratory Data Analysis (EDA)

## What is EDA?

**Exploratory Data Analysis (EDA)** means exploring data to understand it before using it for reports, dashboards, or analysis.

In simple words:

> **EDA = Getting to know your data before making decisions from it.**

EDA helps us understand:

- What data we have
- How the data is structured
- What values and categories exist
- What time period the data covers
- How large the important numbers are
- How values differ between groups
- Which entities perform best or worst
- What patterns or unusual results exist

---

## 📍 Where EDA Fits

```text
Raw Data
   ↓
Bronze Layer
   ↓
Silver Layer
   ↓
Gold Layer
   ↓
EDA / Exploration
   ↓
Dashboards / Reports / Insights
```

EDA is usually done on business-ready data, such as the **Gold Layer**.

---

# 🧠 EDA Mindset

EDA should start with a **question**, not with a SQL function.

Instead of:

```text
❌ Which SQL query should I write?
```

Think:

```text
✅ What do I want to understand?
```

Then choose the SQL technique needed to answer the question.

### Example

Question:

> Which products generate the most revenue?

SQL thinking:

```text
Product + Revenue
        ↓
GROUP BY Product
        ↓
SUM(Revenue)
        ↓
ORDER BY Revenue DESC
```

Another question:

> How has revenue changed over time?

```text
Date + Revenue
        ↓
GROUP BY Month
        ↓
SUM(Revenue)
        ↓
ORDER BY Month
```

### Main idea

> **Question → Data needed → SQL technique → Result → Understanding**

---

# 📂 Exploration Scripts

A common EDA folder can be organized like this:

```text
exploration/
│
├── README.md
├── 01_database_exploration.sql
├── 02_dimension_exploration.sql
├── 03_date_range_exploration.sql
├── 04_measures_exploration.sql
├── 05_magnitude_analysis.sql
└── 06_ranking_analysis.sql
```

| Script | Main Purpose |
|---|---|
| `01_database_exploration.sql` | Understand database structure |
| `02_dimension_exploration.sql` | Explore categories and entities |
| `03_date_range_exploration.sql` | Understand time coverage |
| `04_measures_exploration.sql` | Calculate important numbers |
| `05_magnitude_analysis.sql` | Compare values across groups |
| `06_ranking_analysis.sql` | Find top and bottom performers |

---

# 🥇 Gold Layer Data

EDA can be performed on the analytical **Gold Layer**.

Example tables:

| Table | Type | Represents |
|---|---|---|
| `gold.fact_sales` | Fact | Sales transactions |
| `gold.dim_customers` | Dimension | Customer information |
| `gold.dim_products` | Dimension | Product information |

These tables allow us to answer questions such as:

```text
Who?       → Customer
What?      → Product
When?      → Order Date
How much?  → Sales / Quantity
Where?     → Country
```

---

# 🔎 01 — Database Exploration

## Purpose

First understand **what data is available**.

### Check:

- Schemas
- Tables
- Columns
- Data types
- Metadata
- Relationships

### Questions

```text
What tables exist?

What columns are available?

What data types are used?

Which tables contain the data I need?

How are the tables related?
```

### Mental model

```text
Database
   ↓
Schema
   ↓
Tables
   ↓
Columns
   ↓
Relationships
```

### Why?

> You need to understand the data before you can analyze it.

---

# 🧩 02 — Dimension Exploration

**Dimensions** describe the data and are used to group or filter measures.

Examples:

```text
Customer
Product
Country
Category
Subcategory
```

### Check:

- Unique values
- Categories
- Countries
- Product groups
- Customer attributes

### Questions

```text
What countries exist?

What product categories exist?

What subcategories exist?

How many unique customers are there?

Are there unexpected values?
```

### Example

```text
Category
────────────
Bikes
Components
Clothing
Accessories
```

We can then analyze:

```text
Revenue by Category
Quantity by Category
Orders by Category
```

### Key idea

> **Dimension = By what do we want to analyze?**

---

# 📅 03 — Date Range Exploration

Time tells us **when the data happened** and how much historical data we have.

### Check:

```text
Earliest date
Latest date
Historical coverage
Data freshness
Possible gaps
```

Common SQL:

```sql
MIN(order_date)
MAX(order_date)
```

### Example

```text
First Order → 2019-01-01
Last Order  → 2025-12-31
```

This tells us the available time period.

### Why?

Suppose revenue in December is 50% lower.

Before saying revenue dropped, check:

```text
Is December complete?

Is some data missing?

Is December only partially loaded?
```

> A number can be correct but still be misunderstood without time context.

---

# 🔢 04 — Measures Exploration

**Measures** are the numbers we want to understand.

Examples:

```text
Revenue
Quantity
Orders
Customers
Price
```

### Common SQL functions

```sql
SUM()
COUNT()
COUNT(DISTINCT ...)
AVG()
MIN()
MAX()
```

### Questions

| Question | Example |
|---|---|
| How much? | Total Revenue |
| How many units? | Total Quantity |
| How many orders? | Total Orders |
| How many customers? | Unique Customers |
| What is the average? | Average Price |

### Important relationship

```text
Dimension + Measure
        ↓
Analytical Question
```

Examples:

```text
Country  + Revenue
Category + Quantity
Customer + Orders
Product  + Sales
```

A measure gives a number.

A measure + dimension gives **context**.

---

# 📊 05 — Magnitude Analysis

Magnitude analysis asks:

> **Where is the total amount coming from?**

Example:

```text
Total Revenue = $50M
```

Break it down:

```text
Country A → $20M
Country B → $15M
Country C → $10M
Country D → $5M
```

Now we can see which countries contribute the most.

### Common analysis

```text
Revenue  → by Country
Revenue  → by Category
Quantity → by Product
Orders   → by Customer
```

### Common SQL pattern

```sql
SELECT
    country,
    SUM(sales_amount) AS total_sales
FROM gold.fact_sales
GROUP BY country
ORDER BY total_sales DESC;
```

### Questions

```text
Which country contributes the most?

Which category is largest?

Which products drive sales?

Which customers contribute the most?
```

### Mental model

```text
Measure
   ↓
GROUP BY Dimension
   ↓
Compare Values
   ↓
Understand Contribution
```

---

# 🏆 06 — Ranking Analysis

Magnitude analysis shows the size of each group.

Ranking asks:

> **Who or what is at the top or bottom?**

### Examples

```text
Top 5 Products by Revenue
Top 10 Customers by Sales
Top 5 Countries by Quantity
```

Bottom examples:

```text
Bottom 5 Products by Revenue
Bottom 10 Customers by Orders
Lowest-performing Categories
```

### SQL functions

```sql
RANK()
DENSE_RANK()
ROW_NUMBER()
```

### Example

```text
Rank   Product       Revenue
----------------------------
1      Product A     $500K
2      Product B     $420K
3      Product C     $350K
```

### Why?

Ranking helps find:

- Top performers
- Weak performers
- Areas needing attention
- Important business contributors

---

# 📈 Beyond Basic Exploration

EDA can go deeper when the question requires it.

## Trend Analysis

Understand how a measure changes over time.

Examples:

```text
Revenue by Month
Orders by Year
Quantity by Quarter
```

---

## 📊 Distribution Analysis

Understand how values are spread.

Questions:

```text
Are most customers low-value?

Are sales concentrated among a few customers?

Are product prices evenly distributed?
```

---

## 🔗 Relationship Analysis

Understand how values or attributes relate.

Examples:

```text
Does higher product price relate to lower quantity sold?

Do high-value customers buy more products?

Which categories are commonly purchased?
```

---

## ⚠️ Anomaly Investigation

Look for unusual results.

Examples:

```text
Unusually high sales
Unexpectedly low prices
Very large quantities
Missing date periods
Sudden performance changes
```

Important:

> An unusual value does not automatically mean the data is wrong. It means it should be investigated.

---

# 💡 From Query Result to Insight

A **query result is not automatically an insight**.

Example result:

```text
Category A → $20M
Category B → $12M
Category C → $5M
```

This tells us:

> Category A has the highest revenue.

But we can ask more:

```text
Why is Category A higher?

Does it have more products?

Does it have more customers?

Is the average price higher?

Has it always performed this way?

Which countries are driving it?
```

The process is:

```text
SQL Result
    ↓
Observation
    ↓
Question
    ↓
Further Exploration
    ↓
Finding
    ↓
Insight
```

> **EDA turns data results into understanding.**

---

# ⚖️ EDA vs Data Quality vs BI

These are related but have different purposes.

| Activity | Main Question | Example |
|---|---|---|
| Data Quality | Is the data valid? | Are there duplicate keys? |
| EDA | What is happening in the data? | Which category has the most revenue? |
| BI | How do we monitor the business? | Monthly Revenue Dashboard |

## 🧪 Data Quality

Checks whether data follows expected rules.

Examples:

```text
Is the primary key unique?

Are required fields NULL?

Are foreign keys valid?

Are dates valid?
```

## 🔍 EDA

Explores and investigates the data.

Examples:

```text
Which customers generate the most revenue?

What patterns exist?

Which category dominates?

What changed over time?
```

## 📊 BI

Communicates and monitors business information.

Examples:

```text
Revenue KPI
Order KPI
Customer KPI
Sales by Country
Top Products
```

### Easy way to remember

```text
Data Quality
"Is the data valid?"
        ↓
EDA
"What is happening?"
        ↓
BI
"How do we monitor and communicate it?"
```

---

# 🚶 Practical EDA Process

When working with a new dataset, follow these steps.

## 1. Understand the Data Model

Ask:

```text
What does each table represent?

What does one row represent?

What are the dimensions?

What are the measures?

How are the tables related?
```

---

## 2. Inspect the Structure

Check:

```text
Schemas
Tables
Columns
Data Types
Keys
Relationships
```

---

## 3. Explore Dimensions

Check:

```text
Unique categories
Countries
Products
Customers
Segments
```

Look for unexpected values.

---

## 4. Check the Time Period

Find:

```text
Minimum date
Maximum date
Historical coverage
Possible gaps
```

---

## 5. Calculate Main Measures

Start with the overall numbers:

```text
Total Revenue
Total Orders
Total Quantity
Total Customers
Average Price
```

---

## 6. Break Down the Numbers

Move from:

```text
Total Revenue
```

to:

```text
Revenue by Country
Revenue by Category
Revenue by Product
Revenue by Customer
```

---

## 7. Rank Important Entities

Find:

```text
Top Products
Top Customers
Top Countries
Bottom Products
Bottom Customers
```

---

## 8. Investigate Interesting Results

When something stands out, ask:

```text
Why?

When?

Where?

Who contributed?

What changed?

Is the pattern consistent?
```

---

## 9. Form an Insight

Do not just copy the SQL output.

Explain what the result means.

Example:

```text
Result:
Country A → $20M revenue

Meaning:
Country A generates the highest revenue.

Next question:
Which products and customers are driving it?
```

---

## 10. Use the Findings

EDA findings can help with:

```text
EDA
 ↓
Insights
 ↓
 ┌───────────────┐
 ↓               ↓
Dashboard    Further Analysis
 ↓
Business Decisions
```

---

# 🧭 Simple EDA Question Framework

When you do not know where to start, ask these questions:

```text
1. What data do we have?

2. What does each table represent?

3. What values and categories exist?

4. What time period is available?

5. What are the main measures?

6. How do the measures differ by group?

7. Who or what performs best?

8. What looks interesting or unusual?

9. What did we learn?
```

This keeps EDA focused instead of becoming random SQL queries.

---

# 📌 Quick Reference

| Need to understand | Start with |
|---|---|
| Database structure | Metadata / catalog queries |
| Categories | `DISTINCT` |
| Date range | `MIN()` / `MAX()` |
| Total revenue | `SUM()` |
| Number of orders | `COUNT()` |
| Unique customers | `COUNT(DISTINCT ...)` |
| Average price | `AVG()` |
| Performance by country | `GROUP BY country` |
| Performance by category | `GROUP BY category` |
| Top performers | `ORDER BY ... DESC` |
| Ranking | `RANK()` / `DENSE_RANK()` |
| Combine tables | `JOIN` |
| Complex analysis | CTEs / subqueries |
| Trends | Date + aggregation |
| Unusual behavior | Filtering + comparison |

---

# 🎯 Final Takeaway

```text
EDA = Understand the data before using it for decisions.
```

The basic flow is:

```text
Understand Structure
        ↓
Explore Dimensions
        ↓
Check Time
        ↓
Calculate Measures
        ↓
Compare Groups
        ↓
Rank Results
        ↓
Investigate Interesting Findings
        ↓
Create Insights
```

### Remember

> **Start with a question, explore the data, understand the result, and then form an insight.**
