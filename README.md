# pyspark-etl-pipelines-azure

# End-to-End Azure Data Engineering: Incremental Medallion Pipeline

This repository demonstrates a production grade data engineering pipeline built on the Azure Ecosystem. It features automated incremental loading, Delta Lake storage, and data governance via Unity Catalog.

## 🏗️ Architecture
The pipeline follows a Medallion Architecture to ensure data quality and lineage:
1. **Source:** CSV and JSON files landed in ADLS Gen2.
2. **Bronze to Silver:** Incremental ingestion using PySpark, converting raw files to **Delta** format.
3. **Silver to Gold:** Business logic transformations and aggregations.
4. **Orchestration:** **Azure Data Factory** triggers notebooks on a scheduled basis.

## 🛠️ Tech Stack
* **Orchestration:** Azure Data Factory (ADF)
* **Compute:** Azure Databricks
* **Language:** PySpark (Spark SQL & Dataframe API)
* **Storage:** ADLS Gen2, Delta Lake
* **Governance:** Hive Metastore

## 🚀 Key Implementation Details
### 🔄 Incremental Loading logic
Instead of full refreshes, I implemented an incremental pattern to optimize cost and performance:
* **Bronze-to-Silver:** Used Spark to read only new files from ADLS Gen2 and upsert into Delta tables.
* **Silver-to-Gold:** Applied complex transformations (joins, window functions) and stored the final truth in the Gold layer.

### 📅 ADF Orchestration & Triggers
I designed a parent pipeline in ADF that:
1. **Validates** source file existence.
2. **Executes** the Ingestion Notebook.
3. **Executes** the Transformation Notebook upon success.
4. **Trigger:** Set to run on a Daily schedule to ensure data freshness.

## 📊 Data Visualization
The `/02-Databricks-Notebooks/Analysis` folder contains SQL queries and Databricks visualizations used to derive business insights from the Gold layer.
