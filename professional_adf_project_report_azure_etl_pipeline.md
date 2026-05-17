# 🚀 End-to-End Azure ETL Pipeline using Azure Data Factory

# 1. Project Overview

This project demonstrates the implementation of an end-to-end Azure Data Engineering ETL pipeline using Azure Data Factory (ADF), Azure Blob Storage, and Azure SQL Database.

The primary objective of the project was to ingest raw CSV files from Azure Blob Storage, process and orchestrate the data using Azure Data Factory pipelines, and load the structured data into Azure SQL Database for reporting and analytical purposes.

The project was designed as a beginner-to-intermediate level Azure Data Engineering implementation focused on understanding:

- Cloud-based ETL architecture
- Azure resource setup
- Data ingestion workflows
- Pipeline orchestration
- Source-to-sink data movement
- Schema mapping
- SQL integration
- Error handling and debugging
- Data warehouse concepts
- Real-world ETL troubleshooting scenarios

The implementation also emphasized industry-standard naming conventions, modular pipeline development, debugging practices, and interview-oriented conceptual understanding.

---

# 2. Objective

The objective of this project was to build a scalable cloud-based ETL pipeline capable of:

- Uploading raw business data files into Azure Blob Storage
- Connecting Azure Data Factory with Blob Storage and Azure SQL Database
- Creating reusable datasets and linked services
- Loading dimension and fact tables into a relational warehouse
- Orchestrating multiple ETL pipelines using a Master Pipeline
- Handling schema mismatches and duplicate data issues
- Understanding Azure Data Engineering architecture practically

The project also aimed to provide practical exposure to:

- ETL workflow implementation
- Data warehouse design
- Pipeline dependency management
- Incremental loading concepts
- SQL troubleshooting
- Azure networking and firewall configuration

---

# 3. Project Architecture

```text
Local CSV Files
        ↓
Azure Blob Storage (raw-data container)
        ↓
Azure Data Factory Linked Services
        ↓
ADF Datasets
        ↓
ADF Pipelines
        ↓
Copy Activities
        ↓
Azure SQL Database
        ↓
Fact & Dimension Tables
```

---

# 4. ETL Workflow

The ETL process followed the traditional Extract → Transform → Load workflow.

## Extract
ADF extracted raw CSV files from Azure Blob Storage.

Source files included:

- customers.csv
- products.csv
- orders_jan2024.csv
- orders_feb2024.csv
- orders_mar2024.csv
- returns.csv

## Transform
During pipeline execution:

- Schema mapping was performed
- Datatype compatibility was validated
- Source-to-destination column mapping was configured
- Data validation checks were applied

## Load
The transformed data was loaded into Azure SQL Database tables:

- dim_Customers
- dim_Products
- fact_Orders
- fact_Returns

---

# 5. Technologies Used

| Technology | Purpose |
|---|---|
| Azure Blob Storage | Raw data storage layer |
| Azure SQL Database | Destination warehouse |
| Azure SQL Server | Database hosting and authentication |
| Azure Data Factory (ADF) | ETL orchestration and pipeline automation |
| Azure Query Editor | SQL query execution |
| CSV Files | Source datasets |
| SQL | Table creation and debugging |

---

# 6. Azure Resources Setup

## 6.1 Resource Group Creation

A dedicated Azure Resource Group was created to organize all cloud resources associated with the project.

### Resource Group Name

```text
rg-riseshopeasy-project
```

### Region

```text
Central India
```

### Purpose of Resource Group

The Resource Group acted as a logical container for:

- Azure Blob Storage
- Azure SQL Server
- Azure SQL Database
- Azure Data Factory

### Key Learning

Resource Groups simplify:

- resource organization
- permission management
- deployment tracking
- billing management

---

# 7. Storage Layer Configuration

## 7.1 Azure Storage Account

A Storage Account was created to store raw CSV files used as the source layer for ETL processing.

### Storage Account Name

```text
rsshopeasyproject
```

### Configuration

| Setting | Value |
|---|---|
| Region | Central India |
| Performance | Standard |
| Redundancy | LRS |
| Primary Service | Blob Storage |

### Key Concepts Learned

- Blob Storage acts as cloud-based file storage.
- Storage Account names must be globally unique.
- LRS (Locally Redundant Storage) provides low-cost replication.
- Blob Storage is commonly used as a raw-data landing zone in Data Engineering.

---

## 7.2 Blob Container Creation

A Blob Container named:

```text
raw-data
```

was created to store all source CSV files.

### Uploaded Files

- customers.csv
- products.csv
- orders_jan2024.csv
- orders_feb2024.csv
- orders_mar2024.csv
- returns.csv

### Access Level

```text
Private (No anonymous access)
```

### Important Concepts

- Containers help organize data into layers.
- Raw data should remain unchanged for auditing and reprocessing.
- Blob Storage is scalable and cloud-native.

---

# 8. Azure SQL Setup

## 8.1 Azure SQL Server

An Azure SQL Server was created to host relational databases.

### SQL Server Name

```text
sql-riseshopeasy
```

### Authentication

- SQL Authentication
- Admin Username and Password configured

### Important Configuration

- Public endpoint enabled
- Firewall rules configured
- Azure services access enabled
- Current client IP allowed

### Key Learning

Azure SQL Server acts as a logical host for databases and manages:

- authentication
- firewall access
- security
- connectivity

---

## 8.2 Azure SQL Database

An Azure SQL Database was created as the destination warehouse.

### Database Name

```text
db-riseshopeasy-project
```

### Compute Configuration

| Setting | Value |
|---|---|
| Service Tier | General Purpose |
| Compute Tier | Serverless |
| Environment | Development |

### Reason for Choosing Serverless

Serverless compute was selected because:

- it automatically pauses during inactivity
- it reduces cost for learning projects
- it is suitable for development workloads

---

# 9. Data Warehouse Design

The project followed a simplified Star Schema design.

## 9.1 Dimension Tables

### dim_Customers

Stores descriptive customer information.

### dim_Products

Stores product-related business information.

---

## 9.2 Fact Tables

### fact_Orders

Stores transactional order records.

### fact_Returns

Stores product return transactions.

---

## 9.3 SQL Table Creation Scripts

```sql
CREATE TABLE dim_Customers (
    CustomerID VARCHAR(20) PRIMARY KEY,
    CustomerName VARCHAR(100),
    City VARCHAR(50),
    State VARCHAR(50),
    Country VARCHAR(50)
);

CREATE TABLE dim_Products (
    ProductID VARCHAR(20) PRIMARY KEY,
    ProductName VARCHAR(100),
    Category VARCHAR(50),
    Price DECIMAL(10,2)
);

CREATE TABLE fact_Orders (
    OrderID INT PRIMARY KEY,
    CustomerID VARCHAR(20),
    ProductID VARCHAR(20),
    Quantity INT,
    OrderDate DATE,
    OrderStatus VARCHAR(50),
    Discount DECIMAL(10,2),
    TotalAmount DECIMAL(10,2)
);

CREATE TABLE fact_Returns (
    ReturnID INT PRIMARY KEY,
    OrderID INT,
    ReturnDate DATE,
    ReturnReason VARCHAR(100)
);
```

---

# 10. Azure Data Factory Setup

## 10.1 Azure Data Factory Creation

An Azure Data Factory instance was created to orchestrate the ETL workflow.

### Factory Name

```text
adf-riseshopeasy-project
```

### Version

```text
ADF V2
```

### Region

```text
Central India
```

### Purpose of ADF

Azure Data Factory was used for:

- ETL orchestration
- pipeline automation
- data movement
- workflow management
- pipeline execution monitoring

---

# 11. Linked Services Configuration

Linked Services were created to establish reusable connections between ADF and external systems.

## 11.1 Blob Storage Linked Service

### Name

```text
ls_blobstorage
```

### Purpose

Connect ADF with Azure Blob Storage.

---

## 11.2 Azure SQL Linked Service

### Name

```text
ls_sqldatabase
```

### Purpose

Connect ADF with Azure SQL Database.

### SQL Server Format

```text
sql-riseshopeasy.database.windows.net
```

---

## Key Concepts Learned

### Linked Service

A Linked Service acts like a connection configuration or connection string.

It stores:

- server details
- authentication information
- database connection configuration
- storage access credentials

### Difference Between Linked Service and Dataset

| Linked Service | Dataset |
|---|---|
| Connection configuration | Actual data reference |
| Stores authentication | Stores file/table metadata |
| Reusable connection | Specific data structure |

---

# 12. Dataset Creation

Datasets were created to represent source files and destination SQL tables.

---

## 12.1 Blob Source Datasets

| Dataset Name | Purpose |
|---|---|
| DS_Blob_Customers | customers.csv |
| DS_Blob_Products | products.csv |
| DS_Blob_OrdersJan | January orders |
| DS_Blob_OrdersFeb | February orders |
| DS_Blob_OrdersMar | March orders |
| DS_Blob_Returns | returns.csv |

### Dataset Type

```text
DelimitedText
```

### Important Learning

CSV files are treated as DelimitedText because they use delimiters such as commas to separate columns.

---

## 12.2 SQL Sink Datasets

| Dataset Name | SQL Table |
|---|---|
| DS_SQL_dimCustomers | dim_Customers |
| DS_SQL_dimProducts | dim_Products |
| DS_SQL_factOrders | fact_Orders |
| DS_SQL_factReturns | fact_Returns |

---

# 13. Pipeline Development

Multiple pipelines were created for modular ETL processing.

---

## 13.1 PL_CopyDimensions

Purpose:

- Load customer data
- Load product data

### Activities

- Copy_Customers
- Copy_Products

### Pipeline Logic

```text
Copy_Customers → Copy_Products
```

---

## 13.2 PL_CopyOrders

Purpose:

- Load order transaction data

### Activities

- Copy_OrdersJan
- Copy_OrdersFeb
- Copy_OrdersMar

---

## 13.3 PL_CopyReturns

Purpose:

- Load returns data into fact_Returns

### Activity

- Copy_Returns

---

# 14. Copy Activities & Mapping

Copy Activities were used to move data from Blob Storage into Azure SQL tables.

---

## Source Configuration

Blob datasets were configured as source datasets.

---

## Sink Configuration

SQL datasets were configured as sink datasets.

### Write Behavior

```text
Insert
```

---

## Mapping Configuration

Source columns were manually mapped to destination columns.

### Example

| Source Column | Destination Column |
|---|---|
| CustomerID | CustomerID |
| FirstName | CustomerName |
| UnitPrice | Price |
| Amount | TotalAmount |

---

## Key Learning

ADF does not automatically understand semantically similar column names.

Manual mapping becomes necessary when:

- column names differ
- datatypes mismatch
- schema variations exist

---

# 15. Master Pipeline Orchestration

A Master Pipeline was created to orchestrate the complete ETL workflow.

## Pipeline Name

```text
PL_MasterPipeline
```

## Activities

| Execute Pipeline Activity | Target Pipeline |
|---|---|
| Run_CopyDimensions | PL_CopyDimensions |
| Run_CopyOrders | PL_CopyOrders |
| Run_CopyReturns | PL_CopyReturns |

---

## Pipeline Flow

```text
PL_CopyDimensions
        ↓
PL_CopyOrders
        ↓
PL_CopyReturns
```

---

## Key Learning

Master Pipelines help:

- automate workflow execution
- manage dependencies
- simplify orchestration
- centralize monitoring
- improve scalability

---

# 16. SQL Integration

SQL Query Editor was used for:

- table creation
- data validation
- troubleshooting
- truncating tables
- verifying ETL loads

---

## Data Validation Queries

```sql
SELECT * FROM dim_Customers;
SELECT * FROM dim_Products;
SELECT * FROM fact_Orders;
SELECT * FROM fact_Returns;
```

---

## Record Count Verification

```sql
SELECT COUNT(*) AS CustomerCount FROM dim_Customers;
SELECT COUNT(*) AS ProductCount FROM dim_Products;
SELECT COUNT(*) AS OrderCount FROM fact_Orders;
SELECT COUNT(*) AS ReturnCount FROM fact_Returns;
```

---

## Table Reload Queries

```sql
TRUNCATE TABLE fact_Returns;
TRUNCATE TABLE fact_Orders;
TRUNCATE TABLE dim_Products;
TRUNCATE TABLE dim_Customers;
```

---

# 17. Error Handling & Troubleshooting

Several real-world ETL issues were encountered and resolved during implementation.

---

## 17.1 Type Conversion Failure

### Error

```text
CustomerID values like C001 could not convert from String to INT.
```

### Root Cause

The SQL table schema defined CustomerID as INT, while source CSV values contained alphanumeric strings.

### Resolution

CustomerID datatype was changed from:

```text
INT → VARCHAR
```

### Key Learning

Schema validation and datatype compatibility are critical during ETL processing.

---

## 17.2 Primary Key Violation

### Error

```text
Duplicate key value (C001) already existed in dim_Customers.
```

### Root Cause

Pipelines were rerun without clearing existing data.

### Resolution

Tables were truncated before rerunning pipelines.

```sql
TRUNCATE TABLE dim_Customers;
```

### Key Learning

During ETL development, TRUNCATE + RELOAD workflows are commonly used for testing and debugging.

---

## 17.3 Mapping Source Empty Error

### Root Cause

Destination columns were left unmapped in ADF Mapping tab.

### Resolution

Source columns were manually mapped to destination columns.

Example:

```text
Amount → TotalAmount
```

---

## 17.4 SQL Firewall Connectivity Issue

### Error

SQL Query Editor could not connect.

### Root Cause

Client IP was not added to Azure SQL firewall rules.

### Resolution

Current client IP was added to firewall configuration.

---

## 17.5 Publish All Issue

### Problem

ADF authoring changes disappeared.

### Root Cause

Changes were not published to live ADF service.

### Resolution

Used:

```text
Publish All
```

### Key Learning

ADF changes remain only in authoring mode until published.

---

# 18. Key ETL Concepts Learned

The project provided practical understanding of:

- ETL workflow architecture
- Source and sink configuration
- Linked Services
- Datasets
- Copy Activities
- Schema mapping
- Pipeline orchestration
- Master Pipeline execution
- Blob Storage architecture
- SQL integration
- Data warehousing concepts
- Star Schema design
- Incremental loading understanding
- Debugging workflows
- Cloud-based ETL implementation

---

# 19. Interview & Viva Preparation Notes

## What is Azure Data Factory?

Azure Data Factory is a cloud-native ETL and orchestration service used to build, automate, monitor, and manage data pipelines.

---

## Difference Between Source and Sink

| Source | Sink |
|---|---|
| Data origin | Destination location |
| Blob Storage | Azure SQL Database |

---

## Why Use Blob Storage?

Blob Storage acts as a scalable and cost-effective raw data landing zone for ETL pipelines.

---

## Why Use Master Pipeline?

Master Pipelines automate sequential workflow execution and simplify orchestration.

---

## What is Incremental Loading?

Incremental loading is an ETL strategy where only newly arrived or modified data is processed instead of reloading all historical records.

---

## Why Import Schema?

Import Schema allows ADF to automatically understand source structure, column names, and datatypes.

---

## What is a Dataset?

A Dataset represents the structure and location of data used inside pipelines.

---

## What is a Linked Service?

A Linked Service stores reusable connection information for external systems.

---

## Why Validate Pipelines?

Validation identifies configuration issues before runtime execution.

---

# 20. Key Learnings

This project significantly improved understanding of:

- Azure cloud architecture
- Azure Data Factory development
- ETL orchestration
- SQL integration
- Pipeline execution
- Data validation
- Debugging techniques
- Data warehouse modeling
- Real-world troubleshooting
- Schema management
- Data movement workflows

The project also helped build confidence in explaining:

- ETL lifecycle
- pipeline architecture
- Azure services integration
- error resolution workflows
- orchestration concepts
- SQL-based debugging

---

# 21. Final Outcome

The project successfully implemented a fully functional end-to-end Azure ETL pipeline capable of:

- storing raw data in Blob Storage
- orchestrating ETL workflows using ADF
- loading structured warehouse tables
- automating pipeline execution
- handling ETL errors
- validating warehouse data

Final warehouse tables included:

- dim_Customers
- dim_Products
- fact_Orders
- fact_Returns

The complete ETL workflow was successfully orchestrated using:

```text
PL_MasterPipeline
```

---

# 22. Future Enhancements

The project can be extended further using advanced Azure Data Engineering concepts such as:

- Mapping Data Flows
- Derived Columns
- Conditional Split
- Lookup Activities
- Surrogate Keys
- Incremental Loading Pipelines
- Triggers and Scheduling
- Parameterized Pipelines
- Metadata-Driven ETL
- Azure Data Lake Integration
- Power BI Reporting Layer
- CI/CD Integration with Git
- Dynamic File Processing
- Data Quality Validation Framework
- Slowly Changing Dimensions (SCD)

---

# 📌 Conclusion

This project provided hands-on practical exposure to building cloud-based ETL workflows using Azure technologies.

The implementation helped bridge the gap between theoretical ETL concepts and real-world Azure Data Engineering practices.

The project also strengthened understanding of:

- Azure Data Factory architecture
- cloud storage integration
- SQL warehouse loading
- ETL orchestration
- schema mapping
- debugging workflows
- data engineering best practices

The overall solution demonstrates a beginner-to-intermediate level Azure Data Engineering implementation suitable for:

- internship portfolios
- GitHub documentation
- project submissions
- resume discussions
- technical interviews
- viva presentations

