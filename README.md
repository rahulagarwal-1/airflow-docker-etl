# Airflow Docker ETL — Weather to S3

A personal project built to learn Apache Airflow orchestration and Docker containerisation. Uses real-time weather data as the data source to keep it practical.

## What it does

Fetches real-time weather data from the Open-Meteo API on a schedule, saves it as a timestamped CSV, and uploads it to S3 under a date-partitioned path (`weather/YYYY/MM/DD/`). Credentials secured via Airflow Connections — no hardcoded secrets.

## Why I built it

I wanted hands-on experience with:
- Running Airflow locally inside Docker
- Writing and scheduling a DAG
- Connecting to an external API and landing data in S3
- Managing cloud credentials securely without hardcoding

## Pipeline flow

Open-Meteo API  →  Airflow DAG  →  Local CSV  →  AWS S3 (date-partitioned)

## Tech stack

| Tool | Purpose |
|------|---------|
| Apache Airflow 2.5 | Orchestration and scheduling |
| Docker Compose | Containerisation |
| Open-Meteo API | Weather data source |
| AWS S3 + Boto3 | Cloud storage |
| Python 3.10 | Pipeline logic |

## How to run

```bash
# Clone the repo
git clone https://github.com/rahulagarwal-1/airflow-docker-etl.git
cd airflow-docker-etl

# Start Airflow
docker-compose up -d

# Open Airflow UI
http://localhost:8080
```

Once running, go to Admin → Connections in the Airflow UI and add your AWS credentials there. No secrets are hardcoded in the code.

## Project structure

├── dags/
│   └── weather_to_s3_timestamped.py
├── docker-compose.yaml
├── requirements.txt
└── .gitignore

## Learnings

- How Airflow DAGs are structured and scheduled
- CeleryExecutor setup inside Docker Compose
- S3 date-based partitioning for raw data storage
- Securing credentials using Airflow Connections UI
