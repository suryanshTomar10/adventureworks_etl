# adventureworks_etl
End-to-End Azure ETL Project – AdventureWorks

📌 Project Overview

This project demonstrates a production-grade ETL pipeline built using Microsoft Azure services and SQL Server.

The solution extracts transactional sales data from SQL Server, applies business transformations, and loads curated data into Azure Databricks Hive tables under Unity Catalog for analytics and reporting.


---

🏗️ Architecture Overview

SQL Server (AdventureWorks)
        ↓
Azure Data Factory (Orchestration)
        ↓
Azure Data Lake Storage Gen2
        ↓
Azure Databricks (Transformation & Load)
        ↓
Unity Catalog Managed Delta Tables
        ↓
SQL Logging + Email Alerts


---

🗄️ Source System

SQL Server (On-Prem)

AdventureWorksLT2025 Database

Tables Used:

SalesOrderHeader

SalesOrderDetail

Customer

Product




---

🔄 Azure Data Factory – Pipeline Orchestration

The master pipeline performs:

✔️ SQL → ADLS copy
✔️ Mapping Data Flow transformation
✔️ Databricks notebook execution
✔️ Logging into SQL Server
✔️ Success/Failure email trigger


---

📷 Master Pipeline
<img width="1920" height="1080" alt="copy_transform_notebook" src="https://github.com/user-attachments/assets/4b1ead1f-e0f0-48d3-b660-c7f58ff8ecdd" />
<img width="1920" height="1080" alt="log_pipeline_run" src="https://github.com/user-attachments/assets/9181c591-7ef7-4c4c-ac80-7ded7d64642d" />


---

📊 Data Transformation – Mapping Data Flow

Transformations Implemented

✔️ Data cleaning (null handling, filtering)
✔️ Product-wise total sales calculation
✔️ Order-level revenue aggregation
✔️ Customer-level revenue summary
✔️ Margin classification (High / Medium / Low)
✔️ Salesperson ranking using window functions
✔️ Enrichment joins between Product, Customer & Sales tables


---

📷 Data Flow Design

<img width="1920" height="1080" alt="mapping_dataflow" src="https://github.com/user-attachments/assets/8113c4ef-cc7a-40c1-9254-8cfe575c4461" />


---

💾 Azure Data Lake Storage (ADLS Gen2)

Two-layer data architecture:

/source_folder   → Raw extracted data
/target_folder   → Transformed Parquet files

✔️ Optimized storage using Parquet
✔️ Structured folder organization
✔️ Secure service principal authentication


---

⚡️ Azure Databricks – Ingestion Layer

Databricks notebook reads transformed Parquet files from ADLS and loads them into Unity Catalog managed Delta tables.


---

📷 Databricks Notebook
<img width="1920" height="1080" alt="adb_notebook" src="https://github.com/user-attachments/assets/d13344d4-5cdd-4fa6-b5eb-66c0e21e3886" />



Spark session configuration

Schema creation

Delta table creation

Data load & validation



---

🗃️ Unity Catalog – Final Hive Tables

Catalog: adb_adventureworks_etl
Schema: adventureworks_transformed

Tables Created:

customer_orders

order_total

order_details_ext

product_performance

high_margin_products

medium_margin_products

low_margin_products

sales_person_ranked

---

📷 Unity Catalog Tables

<img width="1920" height="1080" alt="adb_hive_tables" src="https://github.com/user-attachments/assets/89fcc2e9-d58a-4103-a4ea-d495d121ea58" />


---

📈 Production Logging Framework

Custom logging implemented in SQL Server:

Pipeline_Run

Pipeline_Log

Activity_Details


Logs capture:

Pipeline Name

Run ID

Trigger Type

Start Time

End Time

Execution Duration

Status (Success / Failed)



---

📷 SQL Logging Tables
<img width="1920" height="1080" alt="sqlServer_logged_pipeline_data" src="https://github.com/user-attachments/assets/71b56f54-6a78-4460-901e-83e9f9fce899" />


---

📧 Email Alert System – Logic App Integration
Logic App is triggered via ADF Web Activity.

Email includes:

Pipeline Name

Run ID

Data Factory Name

Execution Status



---

📷 Logic App Configuration

<img width="1920" height="1080" alt="logic_app" src="https://github.com/user-attachments/assets/f4f74660-f567-4784-9728-9bc59ee4c8c1" />


---

🔐 Security Implementation

✔️ Service Principal authentication
✔️ No hardcoded credentials
✔️ Secure Linked Services
✔️ Parameterized datasets
✔️ Unity Catalog governance


---

🛠️ Technologies Used

Azure Data Factory

Azure Data Lake Storage Gen2

Azure Databricks

Unity Catalog

PySpark

SQL Server

Logic Apps

Delta Lake

Parquet



---

🎯 Key Data Engineering Concepts Demonstrated

End-to-end ETL orchestration

Layered data architecture

Business rule transformation

Window functions & ranking

Aggregations & joins

Production logging design

Error handling framework

Event-driven email notifications

Secure cloud authentication



👨‍💻 Author

Suryansh Tomar
