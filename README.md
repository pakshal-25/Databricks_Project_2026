# 🚀 Bike Lakehouse 2026  
## End-to-End Data Engineering Project on Databricks

---

## 📌 Overview

This project implements a Medallion Architecture (Bronze → Silver → Gold) using **Databricks, PySpark, and Delta Lake**.

The pipeline ingests raw CRM and ERP CSV files, transforms and standardizes the data in the Silver layer, and builds analytics-ready dimension and fact tables in the Gold layer using Star Schema principles.

This project demonstrates practical data engineering concepts including ingestion, transformation, dimensional modeling, and orchestration.

---

## 🏗 Architecture

Raw CSV Files  
→ Bronze Layer (Raw Delta Tables)  
→ Silver Layer (Cleaned & Standardized Tables)  
→ Gold Layer (Dimension & Fact Tables)

---

## 🥉 Bronze Layer – Raw Ingestion

### What Was Implemented

- Read CSV files using PySpark  
- Used schema inference  
- Loaded raw data into Delta tables  
- Used overwrite mode for repeatable ingestion  
- Structured ingestion using a configuration list  

### Bronze Tables

- `bronze.crm_cust_info`  
- `bronze.crm_prd_info`  
- `bronze.crm_sales_details`  
- `bronze.erp_cust_az12`  
- `bronze.erp_loc_a101`  
- `bronze.erp_px_cat_g1v2`  

This layer preserves raw source data with minimal transformation.

---

## 🥈 Silver Layer – Data Cleaning & Standardization

### Transformations Implemented

- Trimmed whitespace from string columns  
- Standardized gender values (M/F → Male/Female)  
- Normalized country codes (US/USA → United States)  
- Removed prefixes from customer IDs  
- Converted numeric date fields (YYYYMMDD) to DateType  
- Handled null and invalid values  
- Renamed technical columns to business-friendly names  
- Standardized product categories and product lines  

Each Silver table was implemented in a dedicated notebook to maintain modular structure.

---

## 🥇 Gold Layer – Dimensional Modeling

### 📦 Dimension Tables

#### `dim_products`

- Generated surrogate key using `ROW_NUMBER()`  
- Joined CRM product data with ERP category data  
- Selected business-ready attributes  

#### `dim_customers`

- Generated surrogate `customer_key`  
- Standardized demographic attributes  
- Cleaned country and gender values  

---

### 📊 Fact Table

#### `fact_sales`

- Built by joining Silver sales data with:
  - `dim_products`
  - `dim_customers`  
- Replaced natural keys with surrogate keys  
- Selected business metrics:
  - `sales_amount`
  - `quantity`
  - `price`
  - `order_date`
  - `ship_date`
  - `due_date`

This structure enables dimensional analysis and reporting.

---

## 🔄 Orchestration

Created a master notebook that executes Silver layer notebooks sequentially using:

```python
dbutils.notebook.run()
