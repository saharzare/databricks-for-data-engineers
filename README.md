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
graph TB
    %% ================= Bronze Layer =================
    bronze[Bronze Layer]
    style bronze fill:#cd7f32,stroke:#000,stroke-width:2px

    %% ================= Silver Layer =================
    silver_erp_customer[ERP Customer]
    silver_erp_location[ERP Location]
    silver_layer_customer[Customer Layer]
    silver_layer_crm_production[CRM Production Layer]
    silver_layer_erp_category[ERP Category Layer]
    silver_sales[Sales Layer]

    style silver_erp_customer fill:#C0C0C0,stroke:#000,stroke-width:2px
    style silver_erp_location fill:#C0C0C0,stroke:#000,stroke-width:2px
    style silver_layer_customer fill:#C0C0C0,stroke:#000,stroke-width:2px
    style silver_layer_crm_production fill:#C0C0C0,stroke:#000,stroke-width:2px
    style silver_layer_erp_category fill:#C0C0C0,stroke:#000,stroke-width:2px
    style silver_sales fill:#C0C0C0,stroke:#000,stroke-width:2px

    %% ================= Gold Layer =================
    gold_dim_customer[Dim Customer]
    gold_dim_product[Dim Product]
    gold_fact_sales[Fact Sales]

    style gold_dim_customer fill:#FFD700,stroke:#000,stroke-width:2px
    style gold_dim_product fill:#FFD700,stroke:#000,stroke-width:2px
    style gold_fact_sales fill:#FFD700,stroke:#000,stroke-width:2px

    %% ================= Connections =================
    bronze --> silver_erp_customer
    bronze --> silver_erp_location
    bronze --> silver_layer_customer
    bronze --> silver_layer_crm_production
    bronze --> silver_layer_erp_category
    bronze --> silver_sales

    silver_erp_customer --> gold_dim_customer
    silver_erp_location --> gold_dim_customer

    silver_layer_crm_production --> gold_dim_product
    silver_layer_erp_category --> gold_dim_product

    gold_dim_customer --> gold_fact_sales
    gold_dim_product --> gold_fact_sales
    silver_sales --> gold_fact_sales
