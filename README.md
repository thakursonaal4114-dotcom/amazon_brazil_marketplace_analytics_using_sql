# Amazon Brazil Marketplace Analytics 📊

### Customer Insights, Revenue Intelligence & Operational Performance Using SQL

> **SQL is not just about writing queries — it is about converting business questions into measurable decisions.**

This project analyzes an Amazon Brazil marketplace business scenario using the **Brazilian E-Commerce Public Dataset by Olist**.

The objective was to use SQL to answer real business questions around:

* Revenue & product performance
* Customer purchasing behavior
* Seller performance
* Payment preferences
* Customer satisfaction
* Delivery performance
* Marketplace optimization
* Demand trends

The analysis contains **14 business problems**, solved using relational SQL techniques including **JOINs, subqueries, window functions, CTE-style logic, aggregations, filtering, GROUP BY, HAVING, and date functions**.

---

## 🎯 Business Objective

The project was designed around a simple business question:

**How can transactional data be converted into decisions that improve revenue, customer retention, seller performance, logistics, and marketplace efficiency?**

The analysis covers:

1. Seller order volume by state
2. Cumulative revenue by product category
3. Payment method usage and average order value
4. Highest-spending customer
5. Average review score by product category
6. Customer ordering behavior by state
7. Sellers registered but never fulfilling orders
8. Top 5 product categories by revenue
9. Median delivery time
10. Products that have never been ordered
11. Sellers performing above the marketplace average
12. Brazilian states with the highest review scores
13. Customers who never submitted a review
14. Month with the highest order volume

These questions directly follow the business problem framework documented in the project presentation.

---

# 🗂️ Dataset at a Glance

The analysis uses the Brazilian E-Commerce Public Dataset by Olist, containing transactional information across customers, orders, products, sellers, payments, reviews and delivery dates.

### Verified dataset scale

| Metric           |  Real Value |
| ---------------- | ----------: |
| Orders           |  **99,441** |
| Customers        |  **99,441** |
| Sellers          |   **3,095** |
| Products         |  **32,951** |
| Order Items      | **112,650** |
| Payments         | **103,886** |
| Reviews          |  **99,224** |
| Delivered Orders |  **96,478** |

The dataset covers Brazilian e-commerce transactions from **2016–2018**.

---

# 🧠 SQL Skills Demonstrated

### Relational Data Analysis

* INNER JOIN
* LEFT JOIN
* Multi-table JOINs
* Foreign-key based table relationships

### Aggregation

* COUNT()
* COUNT(DISTINCT)
* SUM()
* AVG()
* GROUP BY
* HAVING
* ORDER BY

### Advanced SQL

* Subqueries
* CTEs
* Window functions
* Running totals
* Ranking
* Date calculations
* Date formatting
* NULL handling

### Business Analytics

* Revenue analysis
* Customer value analysis
* Seller benchmarking
* Payment behavior
* Product performance
* Customer satisfaction
* Delivery performance
* Demand forecasting

---

# 💼 Business Problems → SQL Solutions → Business Value

## 1. Seller Order Volume by State

### Business Problem

Which seller states are generating the highest order volume?

### SQL Approach

Joined `sellers` with `order_items`, counted distinct orders, grouped sellers by state and ranked states by order volume.

### SQL Skills

`INNER JOIN` + `COUNT(DISTINCT)` + `GROUP BY` + `ORDER BY`

### Business Value

This converts seller-location data into a **regional demand map**, supporting:

* Fulfillment-center planning
* Logistics infrastructure
* Regional resource allocation
* Expansion decisions

This was specifically designed to identify high-demand seller regions and support data-driven expansion.

---

# 2. Cumulative Revenue by Product Category

### Business Problem

How does revenue accumulate over time across product categories?

### SQL Approach

Joined products → order items → orders and used a **window function** to calculate running revenue by category over time.

### SQL Skills

`JOIN` + `SUM()` + `PARTITION BY` + `ORDER BY` + Window Function

### Business Value

The analysis helps management identify:

* Fast-growing categories
* Revenue accumulation trends
* Seasonal demand
* Categories requiring marketing investment

The project specifically uses cumulative revenue to support promotion planning, inventory optimization and revenue forecasting.

---

# 3. Payment Method & Average Order Value

### Business Problem

Which payment method do customers use most, and what is the average order value for each method?

### Real Dataset Result

| Payment Method | Transactions |
| -------------- | -----------: |
| Credit Card    |   **76,795** |
| Boleto         |   **19,784** |
| Voucher        |    **5,775** |
| Debit Card     |    **1,529** |
| Not Defined    |        **3** |

Credit cards represented approximately **74%** of payment records, making them the dominant payment channel.

### SQL Skills

`JOIN` + `COUNT(DISTINCT)` + `AVG()` + `GROUP BY`

### Business Value

The result provides evidence for:

* Payment-partner negotiations
* Checkout optimization
* Payment-specific promotions
* Understanding customer spending behavior

The project specifically identifies the dominant payment method and calculates average order value by payment type.

---

# 4. Highest-Spending Customer

### Business Problem

Who generates the highest customer value across all orders?

### SQL Approach

`customers → orders → order_payments`

Then:

```text
GROUP BY customer
        ↓
SUM(payment_value)
        ↓
ORDER BY total_spend DESC
        ↓
LIMIT 1
```

### SQL Skills

Multi-table `JOIN` + `SUM()` + `GROUP BY` + `ORDER BY` + `LIMIT`

### Business Value

This transforms thousands of transactions into a **customer-value ranking**, enabling:

* VIP customer identification
* Loyalty-program design
* Retention strategies
* Personalized engagement
* Revenue maximization

The PDF explicitly frames this analysis around customer lifetime value and premium customer segmentation.

---

# 5. Average Review Score by Product Category

### Business Problem

Which product categories provide the strongest and weakest customer experience?

### SQL Approach

Joined:

```text
products
   ↓
order_items
   ↓
orders
   ↓
order_reviews
```

Then calculated average review score by category.

### SQL Skills

Multi-table `JOIN` + `AVG()` + filtering + `GROUP BY`

### Business Value

The result can identify:

* Best-rated categories
* Low-performing categories
* Product-quality issues
* Customer dissatisfaction areas

This creates a direct link between SQL analysis and product-quality improvement.

---

# 6. Customer Orders by State

### Business Problem

How frequently are customers ordering, and where are the highest-activity regions?

### SQL Approach

Joined customers and orders, filtered inactive orders, counted distinct orders and grouped the result by customer and state.

### SQL Skills

`JOIN` + filtering + `COUNT(DISTINCT)` + `GROUP BY`

### Business Value

The analysis supports:

* Regional marketing
* Customer segmentation
* Loyalty programs
* Retention planning

The project identifies state-level ordering behavior as a basis for targeted marketing campaigns.

---

# 7. Dormant Sellers

### Business Problem

Which sellers registered on the marketplace but never fulfilled an order?

### SQL Approach

Used a **LEFT JOIN** between sellers and order items and searched for unmatched records using `IS NULL`.

```text
All Sellers
     ↓
LEFT JOIN
     ↓
Order Items
     ↓
WHERE order_item IS NULL
```

### SQL Skill Demonstrated

**LEFT JOIN + NULL detection**

This is an important analytical pattern because it identifies records that exist in one business entity but have no corresponding activity in another.

### Business Value

The output can support:

* Seller re-engagement
* Account cleanup
* Seller activation
* Marketplace efficiency

---

# 8. Top 5 Revenue-Generating Categories

### Business Problem

Which product categories contribute the most revenue?

### SQL Approach

Joined products with order items and orders, summed item prices, grouped by category and ranked the results.

### Verified Revenue Insight

The dataset-level analysis identifies the strongest revenue categories as:

1. **Health & Beauty**
2. **Watches & Gifts**
3. **Bed Bath Table**
4. **Sports & Leisure**
5. **Computers & Accessories**

Total product revenue was approximately **R$13.59 million**, with approximately **R$2.25 million** in freight revenue. Combined item + freight revenue was approximately **R$15.84 million**.

### Business Value

This enables management to:

* Prioritize high-revenue categories
* Allocate promotional budgets
* Improve inventory planning
* Prepare sales events
* Optimize merchandising

---

# 9. Median Delivery Time

### Business Problem

What is the typical delivery time between order placement and actual customer delivery?

### SQL Approach

Calculated delivery duration using date differences and used a subquery/indexing approach to determine the **median**, rather than relying only on the average.

### SQL Skills

`DATEDIFF()` + CTE/subquery logic + window functions + statistical reasoning

### Business Value

Median delivery time provides a more robust representation of the typical customer experience than a simple average when delivery times contain extreme values.

The project connects this metric directly to logistics efficiency, customer waiting time and service-quality improvement.

Independent analysis of the same Olist dataset also reports a median delivery time of approximately **10 days**, supporting the scale of the result.

---

# 10. Products With Zero Order History

### Business Problem

Which products exist in the catalog but have never been purchased?

### SQL Approach

Used:

```text
products
   ↓
LEFT JOIN
   ↓
order_items
   ↓
WHERE order_items.product_id IS NULL
```

### SQL Skill Demonstrated

**LEFT JOIN + NULL filtering**

### Business Value

This identifies:

* Dead catalog listings
* Low-visibility products
* Inventory optimization opportunities
* Products requiring promotion
* Listings that may need removal

The project specifically uses this analysis for catalog cleanup and product discoverability.

---

# 11. Sellers Performing Above the Average

### Business Problem

Which sellers have fulfilled more orders than the marketplace-wide average seller?

### SQL Approach

First calculated total orders per seller.

Then used a **subquery** to calculate the average seller order volume.

Finally filtered sellers whose order count exceeded that benchmark.

```text
Orders per Seller
       ↓
Global Average
       ↓
WHERE Seller Orders > Average
```

### SQL Skills

`CTE` + aggregation + subquery + benchmarking

### Business Value

This turns raw seller transactions into a **performance benchmark**, supporting:

* Top-seller identification
* Seller badges
* Performance recognition
* Seller benchmarking
* Marketplace growth

---

# 12. Brazilian States With Highest Review Scores

### Business Problem

Which Brazilian states provide the strongest customer satisfaction for delivered orders?

### SQL Approach

Joined customers, orders and reviews, filtered for delivered orders and calculated average review score by state.

### SQL Skills

Multi-table `JOIN` + conditional filtering + `AVG()` + `GROUP BY` + ranking

### Business Value

The result allows management to compare regional service quality and identify locations where logistics or seller performance needs improvement.

---

# 13. Customers Who Never Leave Reviews

### Business Problem

Which customers have purchased but never provided feedback?

### SQL Approach

Used a **LEFT JOIN** between active orders and reviews, then identified customers where the review record was `NULL`.

### SQL Skill Demonstrated

`LEFT JOIN` + `IS NULL`

### Business Value

The result identifies a direct target population for:

* Review-reminder campaigns
* Feedback collection
* Customer engagement
* Product feedback generation

---

# 14. Peak Order Month

### Business Problem

When does marketplace demand reach its highest level?

### SQL Approach

Extracted year-month from order timestamps, counted distinct orders and ranked months by volume.

### Real Dataset Insight

One analysis of the same Olist dataset reports **August 2018 as the highest-order month with 10,843 orders**.

The dataset also shows a major Black Friday spike: **1,176 orders were placed on November 24, 2017** alone.

### Business Value

Peak-demand analysis supports:

* Warehouse capacity planning
* Workforce allocation
* Inventory preparation
* Seasonal marketing
* Demand forecasting

---

# 📈 Key Business Results

The SQL analysis turns a large transactional dataset into measurable business intelligence.

### Marketplace Scale

**99,441** orders
**3,095** sellers
**32,951** products
**103,886** payment records
**99,224** review records

### Revenue

**~R$13.59M** product revenue
**~R$2.25M** freight revenue
**~R$15.84M** product + freight revenue

### Operations

**96,478** delivered orders

### Payments

**76,795** credit-card payment records
**19,784** boleto records
Credit cards account for approximately **74%** of payment records.

### Demand

**10,843 orders** in August 2018
**1,176 orders** on Black Friday, November 24, 2017

### Customer Experience

Delivery performance is strongly connected to customer satisfaction. Dataset-level analysis reports average review scores of approximately:

* **4.29** for on-time deliveries
* **2.57** for late deliveries
* **1.76** for not-delivered orders

This demonstrates how SQL can connect operational performance with customer experience.

---

# 🔍 What This Project Demonstrates

This project demonstrates that I can move beyond writing isolated SQL queries and use SQL as a **business analysis tool**.

### Instead of:

> "Write a JOIN."

I asked:

> **"What business decision can this JOIN support?"**

### Instead of:

> "Use a window function."

I applied it to:

> **Measure cumulative revenue growth across product categories.**

### Instead of:

> "Use a subquery."

I applied it to:

> **Benchmark sellers against the average marketplace seller.**

### Instead of:

> "Use a LEFT JOIN."

I applied it to:

> **Find dormant sellers, unpurchased products and customers who never reviewed their orders.**

This is the central purpose of the project: **connecting SQL techniques with measurable business outcomes.**

---

# 💡 Strategic Recommendations

Based on the analysis, the project recommends:

### Revenue Optimization

* Prioritize investment in top-performing product categories.
* Align promotions with category revenue trends.
* Focus inventory on high-demand categories.

### Customer Growth & Retention

* Develop premium loyalty programs for high-value customers.
* Target customers who purchase but never leave reviews.
* Increase post-purchase engagement.

### Logistics & Service Excellence

* Expand fulfillment capacity in high-demand regions.
* Investigate lower-rated states and delivery performance.
* Use delivery KPIs to improve customer experience.

### Marketplace Optimization

* Review or remove products with zero sales history.
* Re-engage dormant sellers.
* Prepare inventory and workforce capacity before peak-demand periods.

These strategic actions are consistent with the recommendations documented in the project presentation.

---

# 🛠️ Tech Stack

**Database:** MySQL
**Language:** SQL
**Analysis:** SQL Business Analytics
**Dataset:** Brazilian E-Commerce Public Dataset by Olist

### Core SQL Concepts

```text
JOINs
GROUP BY
HAVING
Aggregations
Subqueries
CTEs
Window Functions
COUNT(DISTINCT)
Date Functions
NULL Handling
Ranking
Business Benchmarking
```

---

# 📂 Project Structure

```text
Amazon-Brazil-SQL-Analytics/
│
├── README.md
│
├── SQL/
│   ├── Q01_Seller_State_Orders.sql
│   ├── Q02_Cumulative_Category_Revenue.sql
│   ├── Q03_Payment_Method_AOV.sql
│   ├── Q04_Highest_Spending_Customer.sql
│   ├── Q05_Category_Review_Score.sql
│   ├── Q06_Customer_Orders_By_State.sql
│   ├── Q07_Dormant_Sellers.sql
│   ├── Q08_Top_5_Revenue_Categories.sql
│   ├── Q09_Median_Delivery_Time.sql
│   ├── Q10_Unordered_Products.sql
│   ├── Q11_Above_Average_Sellers.sql
│   ├── Q12_State_Review_Performance.sql
│   ├── Q13_Non_Reviewing_Customers.sql
│   └── Q14_Peak_Order_Month.sql
│
└── Documentation/
    └── Amazon_Analysis.pdf
```

---

# 🚀 Conclusion

This project demonstrates how SQL can be used to solve **real business problems across an e-commerce marketplace**.

Starting with approximately **100,000 orders and multiple interconnected relational tables**, I used SQL to investigate revenue, customers, sellers, payments, products, reviews and logistics.

The final analysis moved from:

**Raw Transactions → SQL Logic → Business Metrics → Business Insights → Strategic Actions**

The key achievement was not simply writing SQL queries.

It was using SQL to answer:

> **What is happening in the business, why does it matter, and what should the business do next?**

---

## 👩‍💻 Author

**Sonaal Thakur**

**Data Analytics | SQL | Business Intelligence**

### Core Strengths Demonstrated

* SQL Business Analytics
* Relational Data Analysis
* Advanced JOINs
* Subqueries
* Window Functions
* Customer Analytics
* Revenue Analytics
* Seller Performance Analysis
* Operational Analytics
* Data-Driven Decision Making
