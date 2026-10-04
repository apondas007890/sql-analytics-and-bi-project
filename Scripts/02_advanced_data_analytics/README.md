# 📊 Advanced Data Analytics

## What is Advanced Data Analytics?

Advanced Data Analytics uses SQL to answer **more complex business questions** from the Gold Layer.

It goes beyond basic exploration by using techniques such as:

- Window functions
- CTEs
- Subqueries
- Aggregations
- CASE statements
- Complex SQL logic

In simple words:

> **Advanced Analytics = Using SQL to understand business performance in more detail.**

---

# 🎯 Objectives

This layer is used to:

- Analyze business performance
- Find trends and patterns
- Compare current and historical performance
- Segment customers and products
- Measure business contribution
- Support business decisions
- Build KPI and reporting logic

---

# 🧠 Core Analytical Flow

The basic flow is:

```text
Business Question
        ↓
SQL Logic
        ↓
Result
        ↓
Insight
        ↓
Business Decision
```

The goal is not only to get a number, but to understand what the number means.

---

# ⚙️ Main Techniques

The main SQL techniques used in this layer are:

```text
Complex SQL Queries
Window Functions
CTEs
Subqueries
Aggregations
CASE Logic
Analytical Reporting
```

---

# 📂 Folder Structure

```text
advanced_data_analytics/
│
├── 01_change_over_time_analysis.sql
├── 02_cumulative_analysis.sql
├── 03_performance_analysis.sql
├── 04_data_segmentation.sql
├── 05_part_to_whole_analysis.sql
└── README.md
```

Each script focuses on a different type of business analysis.

---

# 🗂️ Tables Used

The analysis uses the Gold Layer tables:

```text
gold.fact_sales
gold.dim_customers
gold.dim_products
```

These tables provide sales, customer, and product information for analysis.

---

# 📈 01 — Change Over Time Analysis

This analysis shows how a business measure changes over time.

### Core idea

```text
Measure + Date
       ↓
Group by Time
       ↓
Compare Values
       ↓
Find Trend
```

Example:

```text
Sales by Month
Sales by Year
Orders by Month
```

### Used for

- Sales trends
- Growth tracking
- Seasonality
- Historical comparison

### Business value

Helps understand how the business is changing over time.

---

# 📊 02 — Cumulative Analysis

Cumulative analysis shows how values build up over time.

### Core idea

```text
Current Value
      +
Previous Values
      ↓
Running Total
```

Example:

```text
Month 1 → $10K
Month 2 → $25K
Month 3 → $40K
Month 4 → $60K
```

The value keeps accumulating over time.

### Used for

- Running revenue
- Growth tracking
- Performance accumulation
- Financial reporting

### Common SQL

```sql
SUM(sales) OVER (
    ORDER BY date
)
```

---

# 📉 03 — Performance Analysis

Performance analysis compares one value with another value or a reference point.

### Core idea

```text
Current Value
      -
Reference Value
      ↓
Performance Difference
```

Examples:

```text
Current Sales vs Previous Year Sales
Product Sales vs Average Sales
Current Month vs Previous Month
```

### Used for

- KPI analysis
- Year-over-year comparison
- Performance evaluation
- Finding strong or weak performance

### Common SQL

```sql
LAG()
AVG() OVER()
```

---

# 🧩 04 — Data Segmentation

Segmentation divides data into meaningful groups.

### Core idea

```text
Condition
    ↓
Segment
```

Example:

```text
Customer
   ↓
Revenue
   ↓
CASE
   ↓
VIP / Regular / New
```

Another example:

```text
Product
   ↓
Sales
   ↓
CASE
   ↓
High / Medium / Low Value
```

### Used for

- Customer classification
- Product classification
- Customer targeting
- Marketing strategies

### Common SQL

```sql
CASE
    WHEN condition THEN 'Segment A'
    WHEN condition THEN 'Segment B'
    ELSE 'Other'
END
```

---

# 📊 05 — Part-to-Whole Analysis

Part-to-whole analysis shows how much each part contributes to the total.

### Core idea

```text
Part ÷ Whole × 100
```

Example:

```text
Total Revenue = $100M

Category A = $50M
Category B = $30M
Category C = $20M
```

Contribution:

```text
Category A → 50%
Category B → 30%
Category C → 20%
```

### Used for

- Revenue contribution
- Market share
- Category comparison
- Business contribution analysis

### Key question

> **How much does this part contribute to the whole?**

---

# ⚙️ SQL Concepts Used

## Aggregations

Used to calculate business measures.

```sql
SUM()
AVG()
COUNT()
MIN()
MAX()
```

Examples:

```text
Total Sales
Average Sales
Number of Orders
Minimum Value
Maximum Value
```

---

## Window Functions

Used to perform calculations across related rows without grouping them into one row.

Common examples:

```sql
SUM() OVER()
AVG() OVER()
LAG()
LEAD()
```

Used for:

```text
Running totals
Previous values
Next values
Moving comparisons
Rankings
```

---

## CASE Statements

Used to apply conditions and create categories.

```sql
CASE
    WHEN condition THEN value
    ELSE value
END
```

Example:

```text
High Value
Medium Value
Low Value
```

---

## CTEs

**CTE = Common Table Expression**

CTEs help break a complex query into smaller and easier-to-understand steps.

```sql
WITH sales_data AS (
    ...
)
SELECT ...
FROM sales_data;
```

---

## Subqueries

A subquery is a query inside another query.

It is useful when one query needs the result of another query.

```text
Main Query
    ↓
Subquery Result
    ↓
Final Result
```

---

## Joins

Joins combine data from different tables.

Example:

```text
fact_sales
    +
dim_customers
    +
dim_products
```

This allows analysis using sales, customer, and product information together.

---

# 🔄 How the Analyses Work Together

The different analysis types answer different questions:

```text
Change Over Time
"What is changing?"
        ↓
Cumulative Analysis
"How is it building up?"
        ↓
Performance Analysis
"How does it compare?"
        ↓
Segmentation
"Which groups exist?"
        ↓
Part-to-Whole
"How much does each group contribute?"
```

Together, they provide a deeper understanding of business performance.

---

# 💡 From Analysis to Insight

Advanced analytics should not stop at the SQL result.

Example:

```text
Result:
Sales increased by 20%.
```

Then ask:

```text
Why did sales increase?

Which products caused the increase?

Which customers contributed?

Which countries performed better?

Was the increase consistent over time?
```

This turns a SQL result into a business insight.

---

# 📊 Advanced Analytics vs Basic EDA

Basic EDA mainly focuses on:

```text
What data do we have?
What values exist?
What are the totals?
What are the top performers?
```

Advanced Analytics goes further:

```text
How is performance changing?
How does it compare with the past?
How does it accumulate?
Which groups behave differently?
How much does each group contribute?
```

### Simple difference

```text
EDA
 ↓
Understand the data
 ↓
Advanced Analytics
 ↓
Analyze business performance
 ↓
Insight
```

---

# 🚀 Outcome

This layer converts Gold Layer data into deeper business analysis.

It helps answer:

```text
What is happening?
        ↓
How is it changing?
        ↓
How does it compare?
        ↓
Which groups are important?
        ↓
How much does each group contribute?
        ↓
What can we learn?
```

The final goal is:

> **Turn analytical data into meaningful business insights for decision-making.**

---

# 📌 Quick Reference

| Analysis | Main Question |
|---|---|
| Change Over Time | How is the data changing? |
| Cumulative Analysis | How is the value building up? |
| Performance Analysis | How does it compare? |
| Data Segmentation | Which groups exist? |
| Part-to-Whole | How much does each part contribute? |

### Common SQL

| Need | SQL |
|---|---|
| Total | `SUM()` |
| Average | `AVG()` |
| Count | `COUNT()` |
| Previous value | `LAG()` |
| Next value | `LEAD()` |
| Running total | `SUM() OVER()` |
| Conditional logic | `CASE` |
| Complex query structure | `CTE` |
| Query inside query | `Subquery` |
| Combine tables | `JOIN` |

---

# 🎯 Final Takeaway

> **Advanced Data Analytics uses SQL techniques to move from simple data exploration to deeper business analysis.**

Remember:

```text
Business Question
       ↓
SQL Analysis
       ↓
Comparison / Pattern
       ↓
Insight
       ↓
Business Decision
```
