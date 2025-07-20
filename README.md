# CSI-Week-7-Assignments

# Azure Data Factory Project – Daily Truncate-Load Pipelines

This project showcases a beginner-friendly Azure Data Factory (ADF) solution to automate daily data ingestion from CSV files stored in a Data Lake into Azure SQL Database. The design includes individual pipelines for each file and a master pipeline to execute them in parallel.

## 📁 Files Processed

1. **CUST_MSTR_YYYYMMDD.csv** → `CUST_MSTR` table  
2. **master_child_export-YYYYMMDD.csv** → `MASTER_CHILD` table  
3. **H_ECOM_ORDER.csv** → `H_ECOM_ORDER` table

## 🚀 Pipelines

### 🔹 `PL_CUST_MSTR`
- Extracts data from `CUST_MSTR_YYYYMMDD.csv`
- Dynamically adds `ingestion_date` from filename
- Truncates the `CUST_MSTR` table and loads new data

### 🔹 `PL_MASTER_CHILD`
- Processes `master_child_export-YYYYMMDD.csv`
- Extracts date from filename to populate `ingestion_date`
- Performs truncate-load on `MASTER_CHILD` table

### 🔹 `PL_H_ECOM_ORDER`
- Loads data from `H_ECOM_ORDER.csv`
- Adds current date as `ingestion_date`
- Truncates the `H_ECOM_ORDER` table before loading

### 🔹 `PL_MAIN_MASTER`
- **Master pipeline** that triggers all three pipelines (`PL_CUST_MSTR`, `PL_MASTER_CHILD`, `PL_H_ECOM_ORDER`) **in parallel**
- Ensures complete daily ingestion in one go

## 🛠️ Tools Used
- Azure Data Factory (ADF)
- Mapping Data Flows
- Azure SQL Database
- Azure Data Lake Storage Gen2

## 📌 Notes
- Each pipeline follows a **truncate-load strategy** (old data is wiped before new insert).
- Pipelines are designed for **daily runs** and use dynamic file name/date extraction.
- Master pipeline enables automation and parallel execution of all sub-pipelines.

---

✅ Successfully tested. All pipelines executed correctly, and data was loaded into corresponding SQL tables with accurate `ingestion_date` values.
