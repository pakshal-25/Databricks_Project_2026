🚀 Bike Lakehouse 2026
End-to-End Data Engineering Project on Databricks
📌 Project Overview

This project implements a complete Medallion Architecture (Bronze → Silver → Gold) using Databricks, PySpark, and Delta Lake.

The pipeline ingests raw CRM and ERP CSV data, transforms and standardizes it in the Silver layer, and builds business-ready dimension and fact tables in the Gold layer using a Star Schema design.

The objective of this project was to practice real-world data engineering concepts including ingestion, cleaning, transformation, dimensional modeling, and orchestration.

🏗 Architecture

The project follows the Medallion Architecture pattern:

Raw CSV Files
      ↓
Bronze Layer (Raw Delta Tables)
      ↓
Silver Layer (Cleaned & Standardized Data)
      ↓
Gold Layer (Dimension & Fact Tables)
🥉 Bronze Layer – Raw Data Ingestion
What I Implemented:

Read CRM and ERP CSV files using PySpark

Used schema inference

Loaded data into Delta tables

Used overwrite mode for idempotent ingestion

Structured ingestion using configuration lists

Bronze Tables Created:

bronze.crm_cust_info

bronze.crm_prd_info

bronze.crm_sales_details

bronze.erp_cust_az12

bronze.erp_loc_a101

bronze.erp_px_cat_g1v2

This layer stores raw source data without heavy transformations.

🥈 Silver Layer – Data Cleaning & Transformation

In the Silver layer, I cleaned and standardized the data to make it analytics-ready.

Transformations Implemented:

Trimmed whitespace from all string columns

Standardized gender values (M/F → Male/Female)

Normalized country codes (US/USA → United States)

Removed prefixes from customer IDs

Converted numeric date fields (YYYYMMDD) to proper DateType

Handled null values and invalid values

Renamed technical column names to business-friendly names

Standardized product category and product line values

Each Silver table was implemented in a dedicated notebook to maintain modular design.

🥇 Gold Layer – Dimensional Modeling

In the Gold layer, I built analytics-ready tables using Star Schema principles.

📦 Dimension Tables
dim_products

Generated surrogate key using ROW_NUMBER()

Joined CRM product data with ERP category data

Selected business-friendly attributes

Built as a Delta table

dim_customers

Generated surrogate customer key

Standardized demographic attributes

Cleaned country and gender fields

📊 Fact Table
fact_sales

Built by joining Silver sales data with:

dim_products

dim_customers

Replaced natural keys with surrogate keys

Selected business metrics:

sales_amount

quantity

price

order_date

ship_date

due_date

This enables dimensional analysis and structured reporting.

🔄 Orchestration

Created an orchestration notebook that executes Silver layer notebooks sequentially using:

dbutils.notebook.run()

This simulates a pipeline workflow execution model.

⚙️ Technologies Used

Databricks

Apache Spark

PySpark

Spark SQL

Delta Lake

GitHub Integration

Medallion Architecture

Star Schema Modeling

📂 Project Structure
Bronze.ipynb
silver_crm_cust_info.ipynb
silver_crm_prd_info.ipynb
silver_crm_sales_details.ipynb
silver_erp_cust_az12.ipynb
silver_erp_loc_a101.ipynb
silver_erp_px_cat_g1v2.ipynb
gold_dim_products.ipynb
gold_dim_customers.ipynb
gold_fact_sales.ipynb
Orchestration_Silver_Notebooks.ipynb
🎯 What This Project Demonstrates

End-to-end ETL pipeline development

Medallion architecture implementation

Data cleansing and standardization

Dimensional modeling

Surrogate key generation

Fact and dimension design

Modular notebook architecture

Git-based version control in Databricks

👤 Author

Pakshal Sheth
Data Engineering Project – 2026

If you want next, I can:

Make this more resume-impact oriented

Create a short 4-line summary for LinkedIn

Or upgrade this README to look slightly more senior-level without exaggerating

Tell me which direction you want.
