# End-to-End Azure ETL Pipeline using Azure Data Factory

## Project Overview

This project demonstrates an end-to-end Azure Data Engineering ETL pipeline using Azure Data Factory, Azure Blob Storage, and Azure SQL Database.

The goal of this project is to ingest raw CSV files from Azure Blob Storage, process them through Azure Data Factory pipelines, and load the structured data into Azure SQL Database tables for analytical use.

## Architecture

```text
CSV Files
   ↓
Azure Blob Storage
   ↓
Azure Data Factory
   ↓
ADF Linked Services
   ↓
ADF Datasets
   ↓
ADF Pipelines
   ↓
Copy Activities
   ↓
Azure SQL Database
   ↓
Fact and Dimension Tables

Technologies Used
Azure Data Factory
Azure Blob Storage
Azure SQL Database
Azure SQL Server
SQL
CSV Files
ETL Pipelines
Dataset Files

The project uses e-commerce-style CSV files:

customers.csv
products.csv
orders_jan2024.csv
orders_feb2024.csv
orders_mar2024.csv
returns.csv

Azure Resources Created
Resource Group: rg-riseshopeasy-project
Storage Account: rsshopeasyproject
Blob Container: raw-data
SQL Server: sql-riseshopeasy
SQL Database: db-riseshopeasy-project
Azure Data Factory: adf-riseshopeasy-project
SQL Tables

Dimension tables:

dim_Customers
dim_Products

Fact tables:

fact_Orders
fact_Returns

ADF Pipelines
PL_CopyDimensions

Loads customer and product data into SQL dimension tables.

Copy_Customers → Copy_Products
PL_CopyOrders

Loads monthly order files into fact_Orders.

Copy_OrdersJan → Copy_OrdersFeb → Copy_OrdersMar
PL_CopyReturns

Loads return records into fact_Returns.

PL_MasterPipeline

Orchestrates the complete ETL workflow.

PL_CopyDimensions → PL_CopyOrders → PL_CopyReturns
Key Features
Cloud-based ETL pipeline
Blob Storage as raw data layer
Azure SQL as structured warehouse
Source and sink datasets
Copy Activity-based ingestion
Master pipeline orchestration
Schema mapping
SQL validation
Error troubleshooting
Errors Solved
Type Conversion Failure

CustomerID values such as C001 were initially failing because the SQL column was defined as INT.

Solution:

Changed the datatype to VARCHAR.

Primary Key Violation

Duplicate records appeared during repeated pipeline testing.

Solution:

Used TRUNCATE TABLE before reloading data during development.

Mapping Source Empty

Some destination columns had no matching source columns.

Solution:

Manually corrected source-to-destination column mapping in ADF.

Final Outcome

The final ETL workflow successfully loads raw CSV data from Azure Blob Storage into Azure SQL Database through Azure Data Factory pipelines.

Key Learnings
Azure Data Factory orchestration
Linked Services vs Datasets
Source and Sink configuration
Copy Activity mapping
SQL table design
ETL debugging
Data warehouse basics
Master pipeline orchestration
