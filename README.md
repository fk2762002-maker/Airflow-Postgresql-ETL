Astro Airflow Pipelines

A production-grade ETL pipeline built with Apache Airflow (via Astro CLI) that extracts data from both a CSV file and a REST API, applies transformation and validation logic, and loads processed data into PostgreSQL using an incremental, idempotent architecture.

 Overview

This project implements a fully orchestrated ETL pipeline using Apache Airflow (Astro CLI).

It extracts data from:

 Local CSV file (retail_sales.csv)
 REST API (https://dummyjson.com/products)

Then applies:

Data cleaning & transformation
Data validation checks
Incremental loading into PostgreSQL

The pipeline is designed for reliability, scalability, and observability, with retry logic, structured logging, and watermark-based incremental processing.

 Architecture
CSV Source            REST API Source
   │                       │
   └─────── Extract Layer ─┘
             │
             ▼
        Transform Layer
             │
             ▼
        Validation Layer
             │
             ▼
     Incremental Loader
      (PostgreSQL Upsert)
             │
             ▼
     Logging & Monitoring
 Key Features
 Dual data sources (CSV + REST API)
 Retry mechanism with exponential backoff for API calls
 Data validation layer before loading
 Incremental loading (watermark-based) to avoid duplicates
 PostgreSQL upserts (ON CONFLICT)
 Modular Airflow DAG design
 Structured logging for observability
 Astro CLI + Docker ready deployment
 Tech Stack
Layer	Technology
Orchestration	Apache Airflow
Runtime	Astro CLI
Language	Python
API Client	requests + urllib3 Retry
Database	PostgreSQL
Container	Docker
Logging	Python logging
 Project Structure
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
 Getting Started
1_ Clone Repository
git clone https://github.com/your-username/astro-airflow-pipelines.git
cd astro-airflow-pipelines
2️_ Setup Environment Variables

Create .env file:

POSTGRES_HOST=localhost
POSTGRES_PORT=5432
POSTGRES_DB=airflow
POSTGRES_USER=airflow
POSTGRES_PASSWORD=airflow
3️_ Start Airflow (Astro CLI)
astro dev start

Airflow UI:

http://localhost:8080
4️_ Trigger DAG
astro dev run dags trigger retail_etl_dag
 Database Design
 dim_products

Stores product master data.

Column	Type
product_id	INT
title	TEXT
category	TEXT
price	FLOAT
quantity	INT
 fact_sales

Stores transactional sales data.

Column	Type
sale_id	INT
product_id	INT
customer_id	INT
quantity	INT
price	FLOAT
date	DATE
 Incremental Loading Strategy
Uses watermark mechanism
Tracks last processed record
Loads only new data
Ensures idempotency (safe re-runs)
Uses UPSERT (ON CONFLICT) in PostgreSQL
 Observability

Each DAG run tracks:

Rows extracted
Rows loaded
Watermark state
Errors & retries

All logs are available in:

Airflow UI logs
Docker container logs
 Why This Project Matters

This pipeline demonstrates:

Real-world ETL architecture
Production-level Airflow usage
API + batch data integration
Incremental data engineering design
Scalable backend pipeline thinking
 Author
Built as a Data Engineering portfolio project using Apache Airflow + Astro CLI.
