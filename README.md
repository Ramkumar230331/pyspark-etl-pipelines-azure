# pyspark-etl-pipelines-azure

🏎️ Project Overview: F1 Insights Engine
This project is an End-to-End Azure Data Engineering Pipeline designed to ingest, process, and analyze Formula 1 world championship data. By integrating a API with the Medallion Architecture, the pipeline transforms raw race statistics into a "Gold" layer of high-performance analytics.

The goal was to move beyond static data processing and implement a production ready workflow that handles data velocity and volume.

🎯 Objective

To build a scalable, automated system that:

1. Ingests real-time or historical race data from an external API.

2. Optimizes storage and compute costs using Incremental Loading.

3. Ensures data reliability through governance and ADF validation logic.

4. Delivers business ready insights (e.g., Driver Dominance, Constructor Trends) via Delta Lake.

🛠️ Data Source: Ergast Motor Racing API

The pipeline sources its data from the Ergast API, a comprehensive database for Formula 1 statistics.

Format: JSON/CSV landing in ADLS Gen2 (Bronze Layer).


## 📊 Data Visualization
Below screenshot acquired from executing the SQL queries and from Databricks visualizations used to derive business insights from the Gold layer.
**Dominant Drivers**
<img width="1161" height="477" alt="Dominant Drivers" src="https://github.com/user-attachments/assets/6d141b21-0f7a-4c41-8f47-88e1acef7311" />
**Dominant Teams**
<img width="1171" height="449" alt="Dominant Teams" src="https://github.com/user-attachments/assets/bab832c6-7c74-46b2-b9fb-943f8f01b2f2" />


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
   Below screenshot shows the pipeline created for Ingestion, Transformation purpose
<img width="2658" height="1266" alt="image" src="https://github.com/user-attachments/assets/d0e74e26-3bd0-478c-9823-392c355d81d2" />
<img width="2658" height="1266" alt="image" src="https://github.com/user-attachments/assets/de2f05df-8858-4d4e-ac24-fdf533531f4a" />
<img width="2658" height="1266" alt="image" src="https://github.com/user-attachments/assets/2253d759-2f23-439a-9213-1f4acf9709ca" />


