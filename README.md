# Project DE: ingestion pipeline using an incremental loading strategy

## 📖 Project Overview
This project demonstrates how to build an efficient **batch ingestion pipeline using an incremental loading strategy** to process only new or updated records from a relational database.

Instead of performing expensive full-table loads, the pipeline captures data changes based on a timestamp column and incrementally loads the updates into a structured analytical database.

This approach improves **pipeline efficiency, scalability, and processing time**, which are essential principles in modern data engineering workflows.

## 🛠️ Tech Stack
* **Orchestration:** Apache Airflow
* **Data Transformation:** dbt (Data Build Tool)
* **Programming Language:** Python (Requests, Pandas/Polars)
* **Infrastructure/Containerization:** Docker & Docker Compose
* **Storage/Database:** PostgreSQL / MinIO (S3 API)
* **CI/CD:** GitHub Actions

## 📂 Directory Structure

Here is the breakdown of the project's directory structure:

```text
project_DE/
├── README.md                 # Project summary (this file)
├── docker-compose.yml        # Local stack (Postgres, Minio, Airflow, etc.)
├── .env.example              # Example env variables (DO NOT commit credentials)
├── .gitignore                # Ignore .env, __pycache__, data/tmp, etc.
├── data/                     
│   ├── raw/                  # Raw data (sample/synthetic)
│   ├── staging/              # Temporary ingestion results
│   └── seeds/                # Small CSVs for dbt seeds (optional)
├── src/                      
│   ├── ingestion/            
│   │   └── fetch_weather.py  # Script to pull data (API/CSV) -> data/raw
│   ├── transform/            
│   │   └── to_parquet.py     # Lightweight transform (non-dbt) / helper utils
│   └── utils/                
│       ├── logging_utils.py  # Structural logger (JSON) + timestamp
│       └── io_utils.py       # Read/write helpers, idempotency keys, etc.
├── dbt/                      # Main transformations & data quality
│   ├── models/               
│   │   ├── staging/          # Staging models (rename/clean)
│   │   └── marts/            # Star schema / aggregations
│   ├── tests/                # Generic + schema tests
│   ├── seeds/                # Seed data (if not in data/seeds)
│   └── dbt_project.yml       # dbt configuration file
├── dags/                     
│   └── dag_weather_etl.py    # Airflow orchestration: ingest -> load -> dbt -> alert
├── tests/                    
│   ├── unit/                 
│   │   └── test_io_utils.py  # Pytest for utility functions
│   └── integration/          
│       └── test_etl_smoke.py # Small end-to-end smoke tests
├── assets/                   
│   ├── demo.gif              # Loom GIF/short recording of ETL execution
│   └── architecture.png      # Architecture diagram (ETL flow + SLA/Alerts)
├── docs/                     
│   └── index.md              # Lightweight documentation (MkDocs/Markdown)
└── CI/                       
    └── github-actions.yml    # CI/CD workflow: lint + test + dbt build (optional)
