# 🧠 AWS Data Lakehouse using Glue, Delta Lake, and S3

## 📘 Overview
This project demonstrates how to build a **serverless, modern Data Lakehouse architecture** using **AWS Glue**, **Delta Lake**, and **Amazon S3**.  
It combines the **flexibility of data lakes** with the **consistency and reliability of data warehouses**, enabling scalable and ACID-compliant data pipelines.  

The system automatically ingests CSV files, performs ETL transformations, applies UPSERT logic via Delta Lake, and maintains schema consistency across all layers.

---

## 🏗️ Architecture

Raw Data (CSV)
↓
S3 (Raw Zone)
↓
Glue Job (PySpark ETL)
↓
Delta Lake (Curated Zone)
↓
Glue Crawler → Glue Catalog (Schema Detection & Update)
↓
Athena / Redshift / QuickSight (Analytics Layer)
↓
S3 Archived Zone (Historical Files)


---

## ⚙️ Components and Their Roles

### 🔹 Amazon S3 – Storage Layer
- Serves as the **foundation** of the Data Lakehouse.
- Structured into multiple zones:
  - `raw_zone/` → Incoming CSVs from source systems.
  - `lakehouse-dwh/` → Curated Delta tables.
  - `archived/` → Processed and historical files for lineage tracking.

### 🔹 AWS Glue Crawler – Schema Discovery
- Scans S3 data to **infer schemas automatically**.
- Keeps the **Glue Catalog** updated when new data or partitions are added.
- Enables **Athena**, **Redshift Spectrum**, and **QuickSight** to query data instantly without manual schema creation.

### 🔹 AWS Glue Catalog – Metadata & Governance
- Centralized metadata repository storing table definitions, schema info, and partition data.
- Ensures data **discoverability, governance, and consistency** across AWS analytics services.

### 🔹 AWS Glue Jobs – ETL Processing
- Uses **PySpark** to:
  - Read raw data from S3.
  - Apply transformations and aggregations.
  - Dynamically detect table types (e.g., `orders`, `order_items`, etc.).
  - Write transformed data into **Delta format** on S3.
  - Perform **MERGE (UPSERT)** operations for incremental updates.
- Automatically archives processed files for version control and auditability.

### 🔹 Delta Lake – Transactional Storage Layer
- Adds **ACID transactions** and **schema evolution** capabilities to S3.
- Enables **upserts, time travel,** and **data versioning**.
- Provides warehouse-like reliability without managing a dedicated database engine.

### 🔹 PySpark – Processing Engine
- Executes distributed data transformations.
- Handles schema inference, partitioning, and Delta MERGE operations efficiently at scale.

### 🔹 AWS Lambda (Future Enhancement)
- Can trigger Glue jobs automatically whenever new data arrives in S3.

### 🔹 AWS Step Functions (Future Enhancement)
- Can orchestrate multi-step ETL workflows and handle dependencies between Glue jobs.

---

## 🧩 Folder Structure

```

├── scripts/
│   └── glue_delta_etl.py       # Main ETL script (PySpark job)
├── data/
│   ├── raw_zone/
│   ├── lakehouse-dwh/
│   └── archived/
├── README.md
└── requirements.txt

```

---

## 🚀 Execution Flow

1. Upload new CSV files to the **raw_zone** in S3.
2. **Glue Crawler** detects the schema and updates the **Glue Catalog**.
3. **Glue Job** (PySpark script) processes and merges the data into **Delta Lake tables**.
4. Processed data is stored in **lakehouse-dwh/** for analytics.
5. Processed CSVs are automatically **archived**.
6. Data can be queried directly using **Athena**, **Redshift Spectrum**, or BI tools like **QuickSight**.

---

## ✅ Key Features

- Serverless ETL using **AWS Glue**
- ACID transactions with **Delta Lake**
- Automated schema detection using **Glue Crawler**
- Incremental **upserts** and **schema evolution**
- Data lineage tracking and archival
- Query-ready integration with **Athena** and **Redshift**
- Cost-efficient, fully managed architecture

---

## 🧪 Next Steps

- Add **Lambda triggers** for real-time job execution when new files arrive.
- Integrate **Step Functions** for workflow orchestration.
- Implement **data quality validation** using Great Expectations or Deequ.
- Build **Athena/QuickSight dashboards** on top of curated data.

---

## 🏁 Conclusion

This project demonstrates how a **fully serverless, reliable, and cost-efficient Data Lakehouse** can be built on AWS using native services.  
It eliminates infrastructure overhead while providing **data consistency, automation, and analytics readiness** — the foundation of any modern data platform.

---

## 📚 Technologies Used
- AWS Glue Jobs  
- AWS Glue Crawler  
- AWS Glue Data Catalog  
- Amazon S3  
- Delta Lake  
- PySpark  
- AWS Lambda (future)  
- AWS Step Functions (future)
```

---

