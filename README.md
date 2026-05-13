# Astro Airflow Pipeline
This project is an ETL pipeline built using Apache Airflow (Astro CLI). It extracts data from a CSV file and a REST API, processes and validates the data, and loads it into a PostgreSQL database.

---
# Overview
The pipeline processes data from:

* Local CSV file (`retail_sales.csv`)
* REST API (DummyJSON products endpoint)

It performs a full ETL workflow:
Extraction → Transformation → Validation → Loading into PostgreSQL using incremental logic.

---
# Pipeline Flow
CSV File + REST API → Extract → Transform → Validate → Load into PostgreSQL → Logging

---

# Features
* Extract data from CSV and REST API
* Retry mechanism for API requests
* Data validation before loading
* Incremental loading using watermark strategy
* PostgreSQL upsert to prevent duplicates
* Airflow DAG orchestration
* Basic logging for monitoring pipeline execution

---

# Tech Stack
* Apache Airflow
* Astro CLI
* Python
* PostgreSQL
* Docker
* Requests library

---

# Project Structure 

```
astro-airflow-pipelines/
├── dags/
│   └── retail_etl_dag.py
├── include/
│   ├── data/
│   │   └── retail_sales.csv
│   ├── extract.py
│   ├── transform.py
│   ├── validate.py
│   └── load_postgre.py
├── tests/
├── .astro/
├── Dockerfile
├── requirements.txt
└── README.md
```
---

# How to Run
1. Set up the environment using Astro CLI
2. Start Airflow locally
3. Open Airflow UI in the browser
4. Trigger the DAG manually or via CLI

---

# Database
The pipeline loads data into:
* Product dimension table
* Sales fact table

---
# Incremental Loading
* Uses watermark-based tracking
* Processes only new data each run
* Prevents duplicate inserts
* Supports safe re-runs

---

# Logging
Tracks:
* Extraction status
* Transformation results
* Load operations
* Errors and failures

