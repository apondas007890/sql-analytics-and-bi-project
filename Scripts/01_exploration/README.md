# 🔍 Exploration Layer — Exploratory Data Analysis


>
> **Exploratory Data Analysis (EDA)** is the process of investigating data to understand its structure, characteristics, distributions, relationships, patterns, and behavior before using it for reporting, dashboards, or advanced analytics.

The Exploration folder contains the SQL scripts used to **investigate the Gold Layer and understand what the analytical data is telling us**.

Rather than immediately building dashboards or KPIs, we first explore the data and answer questions such as:

```text
What data do we have?
        ↓
How is it structured?
        ↓
What does the data contain?
        ↓
What does the data look like over time?
        ↓
How large are the important measures?
        ↓
How do those measures differ across dimensions?
        ↓
Who / what performs best or worst?
        ↓
What patterns or interesting findings can we discover?
```

---

## 📑 Contents

* [EDA at a Glance](#-eda-at-a-glance)
* [Where EDA Fits](#️-where-eda-fits)
* [The EDA Mindset](#-the-eda-mindset)
* [Exploration Scripts](#-exploration-scripts)
* [Gold Layer Data](#-gold-layer-data)
* [01 — Database Exploration](#-01--database-exploration)
* [02 — Dimension Exploration](#-02--dimension-exploration)
* [03 — Date Range Exploration](#-03--date-range-exploration)
* [04 — Measures Exploration](#-04--measures-exploration)
* [05 — Magnitude Analysis](#-05--magnitude-analysis)
* [06 — Ranking Analysis](#-06--ranking-analysis)
* [Beyond Basic Exploration](#-beyond-basic-exploration)
* [From Query Result to Insight](#-from-query-result-to-insight)
* [EDA vs Data Quality vs BI](#️-eda-vs-data-quality-vs-bi)
* [Practical EDA Process](#-practical-eda-process)
* [Quick Reference](#-quick-reference)
* [Final Takeaway](#-final-takeaway)

---

# 🌟 EDA at a Glance

EDA is **not a single SQL query** and it is not simply “making some charts.”

It is a process of **asking questions, investigating the answers, and developing an understanding of the data**.

### In simple terms:

> **EDA = Getting to know your data before making decisions from it.**

A typical investigation looks like this:

| Stage            | Question                            |
| ---------------- | ----------------------------------- |
| 🧩 Structure     | What data exists?                   |
| 📦 Content       | What values and categories exist?   |
| 📅 Time          | What period does the data cover?    |
| 🔢 Measures      | How much / how many?                |
| 📊 Comparison    | How do values differ across groups? |
| 🏆 Ranking       | Who or what performs best?          |
| 🔬 Investigation | Why is something happening?         |
| 💡 Insight       | What did we learn?                  |


 EDA focuses on understanding:

        - 📦 Dimensions (categories)
        - 🔢 Measures (business metrics)
        - 📅 Date ranges (time coverage)
        - 📊 Data distribution
        - 🏆 Rankings
        - 📈 Business magnitude

---

# 🏗️ Where EDA Fits

```text
Raw Data
   ↓
Bronze Layer
   ↓
Silver Layer
   ↓
Gold Layer (Business Ready Data)
   ↓
🔍 EDA / Exploration Layer
   ↓
BI Dashboards / Reports / Insights
```
---

# 🧠 The EDA Mindset

Good EDA starts with a **question**, not with a SQL function.

Instead of thinking:

```text
❌ "Which SQL query should I write?"
```

think:

```text
✅ "What do I want to understand?"
```

Then select the SQL technique that can answer that question.

### Example

**Business question:**

> Which products generate the most revenue?

Translate the question into SQL thinking:

```text
Product
   +
Revenue
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
Date
   +
Revenue
   ↓
Group by Month
   ↓
SUM(Revenue)
   ↓
ORDER BY Month
```

Another:

> Who are the top customers?

```text
Customer
   +
Revenue
   ↓
SUM(Revenue) by Customer
   ↓
Ranking
   ↓
Top N
```

### ⭐ The principle

> **Start with the question → understand the data needed → choose the SQL technique → interpret the result.**

---
# 📂 Exploration Scripts

```text
📦 scripts/
│
└── 📁 exploration/
    │
    │
    ├── 📄 README.md
    │
    ├── 📄 01_database_exploration.sql     # Explore schemas, tables, columns, and metadata
    │
    ├── 📄 02_dimension_exploration.sql    # Analyze dimensions and categorical attributes
    │
    ├── 📄 03_date_range_exploration.sql   # Analyze historical timelines and date coverage
    │
    ├── 📄 04_measures_exploration.sql     # Calculate key business metrics and KPIs
    │
    ├── 📄 05_magnitude_analysis.sql       # Compare measures across business dimensions
    │
    └── 📄 06_ranking_analysis.sql         # Rank entities based on business performance
```

| #  | Script                       | Main Question                       |
| -- | ---------------------------- | ----------------------------------- |
| 01 | `database_exploration.sql`   | What is available?                  |
| 02 | `dimension_exploration.sql`  | What categories/entities exist?     |
| 03 | `date_range_exploration.sql` | What time period do we have?        |
| 04 | `measures_exploration.sql`   | How much / how many?                |
| 05 | `magnitude_analysis.sql`     | How does performance differ?        |
| 06 | `ranking_analysis.sql`       | Who or what performs best/worst?    |

Each script has a distinct analytical responsibility, so the folder stays organized instead of becoming one large SQL file.

---

# 🥇 Gold Layer Data

The exploration scripts operate on the [Data Warehouse project's](https://github.com/apondas007890/sql-data-warehouse-project) analytical Gold Layer.

### Core tables

| Table                | Type      | Represents                             |
| -------------------- | ----------| -------------------------------------- |
| `gold.fact_sales`    | Fact      | Sales transactions / measurable events |
| `gold.dim_customers` | Dimension | Customer descriptive info              |
| `gold.dim_products`  | Dimension | Product descriptive info               |

### Simplified model
![Data Model](../../docs/data_model.png)

This model lets us combine:

```text
Who?       → Customer
What?      → Product
When?      → Order Date
How much?  → Sales / Quantity
Where?     → Country
```

and turn them into analytical questions.

---

# 🔎 01 — Database Exploration

### Purpose

Before analyzing business data, first understand **what is available**.

### Investigate

* Schemas
* Tables
* Columns
* Data types
* Metadata
* Table structure

### Typical questions

```text
What tables exist?

What columns are available?

What data types are being used?

Which tables contain the analytical data?

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

### Why it matters

You cannot meaningfully analyze a dataset you do not understand.

This step establishes the **map of the data** before deeper exploration begins.

---

# 🧩 02 — Dimension Exploration

Dimensions provide the **descriptive context** used to group and segment measures.

Examples:

```text
👥 Customer
📦 Product
🌍 Country
🏷️ Category
📂 Subcategory
```

### Investigate

* Unique values
* Categories
* Geographic attributes
* Product hierarchy
* Customer attributes

### Questions

```text
What countries exist?

What product categories exist?

What subcategories exist?

How many unique customers are there?

Are there unexpected category values?
```

### Example

Suppose:

```text
Category
────────────
Bikes
Components
Clothing
Accessories
```

Now we can use those categories to investigate:

```text
Revenue by Category
Quantity by Category
Orders by Category
```

### Key idea

> **Dimensions provide the “by what?” part of an analysis.**

---

# 📅 03 — Date Range Exploration

Time gives analytical data its **historical context**.

### Investigate

```text
Earliest date
Latest date
Historical coverage
Data freshness
Time gaps
```

The basic SQL concepts are:

```sql
MIN(order_date)
MAX(order_date)
```

### Example

```text
First Order
    ↓
2019-01-01

Last Order
    ↓
2025-12-31
```

Now we know the dataset covers approximately seven years.

### Why this matters

Suppose an analyst sees:

```text
December Revenue ↓ 50%
```

EDA should first establish whether:

```text
December is complete
        OR
December contains only partial data
        OR
December has missing records
```

Without temporal context, a valid number can still lead to a wrong interpretation.

---

# 🔢 04 — Measures Exploration

Measures are the **numbers we want to understand**.

Typical examples:

```text
💰 Revenue
📦 Quantity
🧾 Orders
👥 Customers
💵 Price
```

### Common operations

```sql
SUM()
COUNT()
COUNT(DISTINCT ...)
AVG()
MIN()
MAX()
```

### Typical questions

| Question                  | Example            |
| ------------------------- | ------------------ |
| 💰 How much?              | Total Revenue      |
| 📦 How many units?        | Total Quantity     |
| 🧾 How many transactions? | Total Orders       |
| 👥 How many customers?    | Distinct Customers |
| 💵 What is the average?   | Average Price      |

### The important relationship

```text
             DIMENSION
                 +
              MEASURE
                 ↓
          ANALYTICAL QUESTION
```

Examples:

```text
Country   + Revenue
Category  + Quantity
Customer  + Orders
Product   + Sales
```

A measure by itself gives a number.

A measure combined with a dimension gives **context**.

---

# 📊 05 — Magnitude Analysis

Magnitude analysis moves from:

> **“How much do we have?”**

to:

> **“Where is that amount coming from?”**

### Example

Overall:

```text
Total Revenue = $50M
```

Magnitude analysis breaks it down:

```text
🌍 Country A   $20M
🌍 Country B   $15M
🌍 Country C   $10M
🌍 Country D    $5M
```

Now we can see the relative contribution.

### Common analysis

```text
Revenue   → by Country
Revenue   → by Category
Quantity  → by Product
Orders    → by Customer
```

### Typical SQL pattern

```sql
SELECT
    country,
    SUM(sales_amount) AS total_sales
FROM gold.fact_sales
GROUP BY country
ORDER BY total_sales DESC;
```

### Questions answered

* Which country contributes the most?
* Which category is largest?
* Which products drive sales?
* Which customers contribute significant revenue?

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

Magnitude analysis tells us the size of each group.

Ranking goes one step further:

> **Who is at the top and who is at the bottom?**

### 🥇 Top-N

```text
Top 5 Products by Revenue
Top 10 Customers by Sales
Top 5 Countries by Quantity
```

### 🔻 Bottom-N

```text
Bottom 5 Products by Revenue
Bottom 10 Customers by Orders
Lowest-performing Categories
```

### SQL tools

```sql
RANK()
DENSE_RANK()
ROW_NUMBER()
```

### Example

```text
Rank   Product       Revenue
─────────────────────────────
  1    Product A     $500K
  2    Product B     $420K
  3    Product C     $350K
```

### Why ranking is useful

Ranking helps identify:

* ⭐ leaders
* ⚠️ weak performers
* 🎯 areas requiring attention
* 💼 entities contributing most to the business

---

# 📈 Beyond Basic Exploration

The six scripts provide the core exploration workflow, but EDA can go further when a question requires deeper investigation.

### 📈 Trend Analysis

Understand how a measure changes with time.

```text
Revenue by Month
Orders by Year
Quantity by Quarter
```

---

### 📊 Distribution Analysis

Understand how values are spread.

For example:

```text
Are most customers low-value?

Are sales concentrated among a small number
of customers?

Are product prices evenly distributed?
```

---

### 🔗 Relationship Analysis

Investigate how attributes or measures relate.

```text
Does higher product price correspond
to lower quantity sold?

Do high-value customers purchase
more products?

Which categories are commonly purchased?
```

---

### ⚠️ Anomaly Investigation

Investigate values that appear unusual.

Examples:

```text
Unusually high sales
Unexpectedly low prices
Very large quantities
Unexpected date gaps
Sudden changes in performance
```

### Important distinction

Finding something unusual does **not automatically mean the data is wrong**.

It means:

> **“This result deserves investigation.”**

That is an important part of exploratory analysis.


---

# 💡 From Query Result to Insight

This is one of the most important concepts in EDA.

A **query result is not automatically an insight**.

Suppose the query returns:

```text
Category A → $20M
Category B → $12M
Category C → $5M
```

That is a **result**.

We can interpret it:

> Category A generates the highest revenue.

That is an **observation**.

But good EDA continues:

```text
Why is Category A higher?
          ↓
Does it contain more products?
          ↓
Does it have more customers?
          ↓
Is the average selling price higher?
          ↓
Did it always perform this way?
          ↓
Is the difference concentrated
in particular countries?
```

Now we are investigating the **reason behind the result**.

### 🧠 Think of it as:

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
💡 Insight
```

> **EDA is the process of turning data into understanding.**

---

# ⚖️ EDA vs Data Quality vs BI

These concepts often get mixed together, but they have different purposes.

| Activity        | Main Question                   | Example                                    |
| --------------- | ------------------------------- | ------------------------------------------ |
| 🧪 Data Quality | Is the data valid?              | Are there duplicate keys?                  |
| 🔍 EDA          | What does the data tell us?     | Which category generates the most revenue? |
| 📊 BI           | How do we monitor the business? | Monthly Revenue dashboard                  |

### 🧪 Data Quality

Focuses on predefined rules:

```text
Is the primary key unique?
Are required fields NULL?
Are foreign keys valid?
Are dates valid?
```

### 🔍 EDA

Focuses on investigation:

```text
Which customers generate the most revenue?
What patterns exist?
Which category dominates?
What changed over time?
```

### 📊 BI

Focuses on repeatable communication:

```text
Revenue KPI
Order KPI
Customer KPI
Sales by Country
Top Products
```

### The simplest way to remember:

```text
🧪 Data Quality
"Is the data valid?"

        ↓

🔍 EDA
"What is happening in the data?"

        ↓

📊 BI
"How do we monitor and communicate it?"
```

---

# 🚶 Practical EDA Process

When approaching a new analytical dataset, use this workflow.

### 1. 🗺️ Understand the model

Determine:

```text
What does each table represent?
What does one row represent?
What are the dimensions?
What are the measures?
How are tables related?
```

---

### 2. 🗄️ Inspect the structure

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

### 3. 🧩 Explore dimensions

Look at:

```text
Unique categories
Countries
Products
Customers
Segments
```

Pay attention to unexpected values.

---

### 4. 📅 Establish the time context

Find:

```text
Minimum date
Maximum date
Historical coverage
Possible gaps
```

---

### 5. 🔢 Calculate the major measures

Start with the overall picture:

```text
Total Revenue
Total Orders
Total Quantity
Total Customers
Average Price
```

---

### 6. 📊 Break the numbers down

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

### 7. 🏆 Rank important entities

Find:

```text
Top Products
Top Customers
Top Countries
Bottom Products
Bottom Customers
```

---

### 8. 🔬 Investigate interesting results

Whenever something stands out, ask:

```text
Why?
When?
Where?
Who contributed?
What changed?
Is the pattern consistent?
```

---

### 9. 💡 Form an insight

Do not simply copy the SQL output.

Explain what it means.

```text
Result:
Country A → $20M revenue

Interpretation:
Country A generates the largest revenue contribution.

Further question:
What products and customers are driving that performance?
```

---

### 10. 📊 Feed the findings downstream

The exploration can influence:

```text
                🔍 EDA
                  │
                  ▼
               💡 Insights
                  │
          ┌───────┴────────┐
          ▼                ▼
      📊 Dashboard     📈 Further
        Design          Analysis
          │
          ▼
       💼 Decisions
```

---

# 🧭 A Simple Question Framework

When you are unsure how to start EDA, move through these questions:

```text
┌────────────────────────────────────┐
│ 🗄️ WHAT DATA DO WE HAVE?           │
└──────────────────┬─────────────────┘
                   ↓
┌────────────────────────────────────┐
│ 🧩 WHAT DOES EACH TABLE REPRESENT? │
└──────────────────┬─────────────────┘
                   ↓
┌────────────────────────────────────┐
│ 📦 WHAT VALUES / CATEGORIES EXIST? │
└──────────────────┬─────────────────┘
                   ↓
┌────────────────────────────────────┐
│ 📅 WHAT TIME PERIOD IS AVAILABLE?  │
└──────────────────┬─────────────────┘
                   ↓
┌────────────────────────────────────┐
│ 🔢 WHAT ARE THE MAIN MEASURES?     │
└──────────────────┬─────────────────┘
                   ↓
┌────────────────────────────────────┐
│ 📊 HOW DO THEY DIFFER BY GROUP?    │
└──────────────────┬─────────────────┘
                   ↓
┌────────────────────────────────────┐
│ 🏆 WHO / WHAT PERFORMS BEST?       │
└──────────────────┬─────────────────┘
                   ↓
┌────────────────────────────────────┐
│ 🔬 WHAT IS INTERESTING / UNUSUAL?  │
└──────────────────┬─────────────────┘
                   ↓
┌────────────────────────────────────┐
│ 💡 WHAT DID WE LEARN?              │
└────────────────────────────────────┘
```

This prevents EDA from becoming random SQL experimentation.

---

# 📌 Quick Reference

| Need to understand...        | Start with...                          |
| ---------------------------- | -------------------------------------- |
| 🗄️ Database structure       | Metadata / catalog queries             |
| 🧩 Categories                | `DISTINCT`                             |
| 📅 Date boundaries           | `MIN()` / `MAX()`                      |
| 💰 Total revenue             | `SUM()`                                |
| 🧾 Number of orders          | `COUNT()`                              |
| 👥 Unique customers          | `COUNT(DISTINCT ...)`                  |
| 💵 Average price             | `AVG()`                                |
| 🌍 Performance by country    | `GROUP BY country`                     |
| 📦 Performance by category   | `GROUP BY category`                    |
| 🏆 Top performers            | `ORDER BY ... DESC`                    |
| 🥇 Ranking                   | `RANK()` / `DENSE_RANK()`              |
| 🔗 Combine business entities | `JOIN`                                 |
| 🧠 Complex analysis          | CTEs / subqueries                      |
| 📈 Trends                    | Date + aggregation                     |
| ⚠️ Unusual behavior          | Filtering + comparison + investigation |
