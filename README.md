📊 Data Pipeline Architecture (Databricks)

🔹 Overview

This project implements a multi-layer data pipeline (Bronze → Silver → Gold) in Databricks to process raw operational data and transform it into analytics-ready datasets.The pipeline is executed as a dependency-based Databricks Job (DAG), where each task runs only after its upstream dependencies have completed successfully.

🥉 Bronze Layer
Ingests raw data from ERP and CRM source systems
No business logic applied
Purpose: store raw, traceable, and auditable data
Job:
bronze

🥈 Silver Layer
Data cleansing and validation
Normalization and application of business rules
Domain-oriented transformations (Customer, Product, Location, Sales)
Jobs:
silver_erp_customer
silver_erp_location
silver_layer_customer
silver_layer_crm_production
silver_layer_erp_category
silver_sales

🥇 Gold Layer
Builds analytics-ready tables using a star schema
Optimized for BI tools and reporting
Dimension Tables:
gold_dim_customer
gold_dim_product
Fact Table:
gold_fact_sales
Fact Table:
gold_fact_sales

🔗 Execution Flow
The pipeline runs as a Directed Acyclic Graph (DAG)
Task dependencies are managed by Databricks Jobs
Downstream tasks execute only if upstream tasks succeed

🛠 Technologies
Databricks
Apache Spark
Delta Lake
GitHub (Version Control)

✅ Status
Latest run: Successful
All pipeline stages completed without errors
<img width="1913" height="871" alt="image" src="https://github.com/user-attachments/assets/9014dede-e48a-47a6-be4e-06091a4230c4" />
