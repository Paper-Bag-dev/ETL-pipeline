# ETL Crypto ETL System — Submission Overview

This project implements a complete ETL + API backend for the ETL assignment. This project is deployed on render due to credit limitations in other cloud services providers. Its running for 0 cost via a workflow cron job in .github/workflows/cron.yml and backend hosted and deployed on render.com with postgres instance from aiven cloud. You can visit https://ETL-backend-latest.onrender.com/ to check the get endpoints labelled below. To run it please follow the instructions below after cloning this repo and use the Makefile to run it locally.

## ✅ Completed Requirements
**P0 — FOUNDATION LAYER**  
**P1 — GROWTH LAYER**  
**P2.3 — Rate Limiting + Backoff**  
**P2.4 — Observability Layer**  
**P2.5 — DevOps Enhancements**  

## 🔧 Tech Stack
- FastAPI — API layer  
- PostgreSQL — storage  
- SQLAlchemy — ORM  
- Docker — runtime  
- APScheduler — ETL scheduler  
- httpx — retry + exponential backoff  
- Prometheus metrics — ETL observability  

---

## 📦 Docker Image (Final Submission)

Public Docker Hub image:  
👉 **https://hub.docker.com/r/aetherlover/ETL-backend**

Pull it:

```
docker pull aetherlover/ETL-backend:latest
```


---

# 🚀 Run Locally

## 0. Clone this repository:
```
git clone https://github.com/Paper-Bag-dev/ETL-backend-vikalp-sharma.git
cd ETL-backend-vikalp-sharma
```

## 1. Create `.env`

(Replace values)


Important variables:

- `DATABASE_URL`
- `COINGECKO_API_KEY`
- `CRON_SECRET`
- `ETL_FETCH_INTERVAL=2`
- `CSV_PATH=./data/coins.csv`
- `APP_ENV=local`

---

## 2. Start the entire system

The repo already includes **Makefile + docker-compose**, so simply run:

```
make up
```
or 
```
make down
make test
```


API will be available at:

👉 **http://localhost:8000**

---

## 3. Trigger ETL Manually

```
curl -X POST http://localhost:8000/internal/run-etl
-H "x-api-key: <CRON_SECRET>"
```


# 📁 Endpoints

```
GET /health
GET /data
GET /stats
GET /metrics
```


This project completes all core and some advanced requirements in P2, including observability, CI, Docker image publishing, and a clean deployment-ready architecture.

# Fixed:
1. CSV_PATH not included in docker-compose file causing csv missing error.
2. APP_ENV: production hardcoded string removed. Now it's sourced properly from .env file.
3. DATABASE_URL: harcoded string removed. Now it's also sourced properly from .env file.
4. Minor oversights where I hardcoded database url for testing.

# Added:
1. .dockerignore file with .env included.
2. ETL_FETCH_INTERVAL env variable to control interval of fetching the data via .env. Defauls to 2 minutes (to mainly prevent coingecko from throttling and blocking requests).
