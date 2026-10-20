# E-Commerce Sales & Customer Analytics

**An end-to-end data analytics project using Python, MySQL, SQL, and Power BI to analyze sales performance, customer behavior, product performance, and payment effectiveness.**

## Project Overview

This project analyzes 50,000 e-commerce orders to understand revenue trends, customer purchasing behavior, product performance, city-level sales, and payment outcomes.

The project follows an end-to-end analytics workflow, from processing raw JSON data using Python and Pandas to storing normalized data in MySQL, performing business analysis using SQL, creating SQL views, and building interactive Power BI dashboards.

The objective is to transform raw transactional data into actionable business insights that help management understand business performance and make data-driven decisions.

## Business Problem

An e-commerce company has experienced growth in its customer base and transaction volume, but management lacks a clear understanding of what is driving its revenue and customer growth.

The leadership team wants to understand which customers and products are most valuable, which cities and categories are performing well, how customer purchasing behavior varies, and whether payment issues are affecting transactions.

The objective is to analyze transactional data and provide management with a clear view of sales performance, customer value, product performance, market performance, and payment effectiveness.

## Project Objectives

- Analyze total revenue, average order value, and monthly revenue trends.
- Identify high-value customers and analyze purchasing frequency.
- Evaluate product and category performance by revenue and quantity sold.
- Compare sales performance across cities.
- Analyze payment method preferences and payment success and failure patterns.
- Build interactive dashboards that support business analysis and decision-making.

## Tools & Technologies Used

1. Python - Extracting and transforming nested JSON data 
2. Pandas - Data manipulation and DataFrame creation 
3. MySQL - Relational data storage and database management 
4. SQL - Data analysis, joins, aggregations, CTEs, subqueries, and window functions 
5. SQL Views - Preparing reusable analytical datasets and Power BI source views 
6. Power BI - Data modeling, interactive reports, and dashboard development 
7. DAX - Creating KPIs and analytical measures 

## Dataset Overview

The project uses a synthetic e-commerce dataset containing 50,000 orders in JSON format.

**Source file:** [E-Commerce Dataset (JSON)](Data/ecommerce_50000_orders.json)

The dataset contains order details, customer information, payment information, and product-level transaction data.

### Database Tables

The nested JSON data was processed and normalized into five relational tables:

| Table | Description |
|---|---|
| `orders` | Order identifiers, dates, and customer references |
| `customers` | Customer identifiers, names, and cities |
| `payments` | Payment methods and payment statuses |
| `products` | Product identifiers, names, and categories |
| `order_items` | Product-level order details, including quantity, price, and item amount |

The `order_items` table contains 125,451 rows because an order can contain multiple products.

## Project Workflow

1. **Data Extraction:** Loaded the raw JSON dataset using Python.
2. **Data Transformation:** Used Pandas to extract nested JSON fields and organize the data into separate DataFrames.
3. **Database Development:** Loaded the normalized DataFrames into MySQL.
4. **SQL Business Analysis:** Answered business questions using joins, aggregations, subqueries, CTEs, and window functions.
5. **SQL View Development:** Created analytical views for sales, customer, product, and payment analysis.
6. **Power BI Integration:** Connected Power BI to MySQL and used dedicated SQL views as source tables for the analytical data model.
7. **Data Modeling:** Designed a star schema with a fact view, dimension views, and a date dimension.
8. **DAX Development:** Created reusable measures for revenue, orders, customers, average order value, and other business KPIs.
9. **Dashboard Development:** Built three interactive Power BI report pages.
10. **Business Insights:** Used the analysis to identify performance patterns and potential business improvement opportunities.

## SQL Analysis

The project addresses 15 business questions across five analytical areas.

### 1. Revenue & Sales Analysis

- What is the total revenue the business generates?
- What is the Average Order Value (AOV), and how does it change over time?
- What is the revenue generated each month?
- Which months had the highest revenue growth and decline?
  
### 2. Customer Analysis

- What is the Customer Lifetime Value (CLV) for each customer?
- Who are the Top 10 customers by total spending?
- List of the customers who have placed repeated orders.
- What percentage of total revenue do the Top 10% of customers generate?

### 3. Product & Category Performance 

- Which product categories generate the highest revenue, and what percentage of total revenue does each category contribute?
- Which products generate the highest revenue?
- Which products have the highest quantity sold?
- What are the Top 3 revenue-generating products within each category?

### 4. Market / City Performance

- Which cities generate the highest revenue, and how does revenue per customer compare across cities?

### 5. Payment Performance

- Which payment methods are most frequently used, and what is the payment success rate for each method?
- Which payment method has the highest Average Order Value?

## SQL Views and Power BI Integration

SQL views were created to organize analytical logic and provide structured data for reporting.

### Analytical SQL Views

The following views support business analysis:

- `vw_sales_analysis` — sales performance analysis.
- `vw_customer_analysis` — customer spending and purchasing behavior.
- `vw_product_analysis` — product and category performance.
- `vw_payment_analysis` — payment method and transaction status analysis.

### Power BI Source Views

Dedicated SQL views were created to support a star-schema model in Power BI.

| View | Purpose |
|---|---|
| `vw_fact_sales` | Contains order-item transaction data, including dates, customer and product identifiers, payment information, quantities, prices, and item amounts |
| `vw_dim_customer` | Provides customer attributes, including customer name and city |
| `vw_dim_product` | Provides product attributes, including product name and category |
| `vw_dim_payment` | Provides distinct payment methods |

These views were connected to Power BI and used as source tables for data modeling, DAX calculations, slicers, and report visuals.

Using SQL views helped separate data preparation and analytical logic from report development while providing a consistent structure for business intelligence reporting.

## Power BI Data Model

The Power BI model follows a **star schema** to support analytical reporting and consistent filtering.

### Model Components

- **Fact view:** `vw_fact_sales`
- **Customer dimension:** `vw_dim_customer`
- **Product dimension:** `vw_dim_product`
- **Payment dimension:** `vw_dim_payment`
- **Date dimension:** `Dim_Date`, created in Power BI

### Relationships

The model uses one-to-many relationships from the dimension tables to the fact view:

- `Dim_Date[Date]` → `vw_fact_sales[order_date]`
- `vw_dim_customer[customer_id]` → `vw_fact_sales[customer_id]`
- `vw_dim_product[product_id]` → `vw_fact_sales[product_id]`
- `vw_dim_payment[payment_method]` → `vw_fact_sales[payment_method]`

Single-direction filtering from dimensions to the fact view supports predictable filtering and reusable DAX measures.

## DAX Measures and KPIs

DAX measures were created to calculate key business performance indicators.

Examples include:

- Total Revenue
- Total Orders
- Total Customers
- Average Order Value
- Average Customer Revenue
- Average Orders per Customer
- Total Products Sold
- Average Revenue per Product
- Successful Orders
- Payment Success Rate
- Payment Count
- Order Lines

These measures support KPI cards, customer and product comparisons, time-based analysis, and payment performance reporting.

## Power BI Dashboard

The report is organized into three pages.

### 1. KPI Summary

Provides an executive-level view of business performance.

**KPIs**
- Total Revenue
- Total Orders
- Total Customers
- Average Order Value

**Visualizations**
- Monthly Revenue Trend
- Revenue by City
- Top 5 Customers by Revenue
- Revenue by Product Category

### 2. Customer & Product Analysis

Focuses on customer value and product performance.

**KPIs**
- Average Customer Revenue
- Average Orders per Customer
- Total Products Sold
- Average Revenue per Product

**Visualizations**
- Top 3,5, and 10 Products by Revenue
- Top 3,5, and 10 Products by Quantity Sold
- Category Revenue by City
- Top 3 Quantity Sold % by City

### 3. Payment Analysis

Examines payment behavior and transaction outcomes.

**KPIs**
- Total Orders
- Successful Orders
- Payment Success Rate

**Visualizations**
- Payment Success vs. Failure by Payment Method
- Average Order Value vs. Total Orders by Payment Method
- City-level analysis of the most-used payment method

The report includes interactive filters and navigation to help users explore performance across business dimensions.

## Key Business Insights & Recommendations

Detailed SQL analysis, query outputs, Power BI dashboard screenshots, key business insights, and actionable recommendations are documented in the project case study PDF.

📄 **[View the E-Commerce Analytics Case Study](PASTE_YOUR_PDF_LINK_HERE)**

## Skills Demonstrated

- JSON data processing using Python and Pandas
- Data transformation and normalization
- Relational database development using MySQL
- SQL joins, aggregations, subqueries, and CTEs
- Window functions and ranking analysis
- SQL view development
- Star-schema data modeling
- DAX measures and KPI development
- Power BI dashboard development
- Data visualization and business storytelling

## Project Outcome

This project demonstrates an end-to-end analytics workflow that converts raw e-commerce data into structured datasets, reusable SQL views, a star-schema data model, and interactive Power BI dashboards.

It combines data preparation, database management, SQL analysis, data modeling, and business intelligence to support sales, customer, product, city, and payment performance analysis.

**Anugya Singhal**
Power BI Developer | Data Analyst

**Technologies:** Power BI, SQL, MySQL, Python, Pandas, DAX, and Excel
