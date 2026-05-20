# Apache Airflow Scraper — Project Documentation
Dealwallet  
Version 1.0 | February 2026  

---

##  Project Summary

| Field        | Details |
|-------------|--------|
| Project Name | Apache Airflow Multi-Site Product Scraper |
| Purpose | Scrape product data from e-commerce websites and store in Supabase |
| Schedule | Runs automatically at 9 AM & 9 PM daily |
| Status | Production Ready |
| Tech Stack | Apache Airflow, Playwright, BeautifulSoup, Docker, Supabase |

---

##  1. Project Overview

This project is an automated ETL (Extract, Transform, Load) pipeline built using Apache Airflow.

It:
- Scrapes product data from multiple e-commerce websites
- Cleans and transforms the data
- Stores it in a Supabase PostgreSQL database

---

##  Pipeline Flow

ikea_products        ──┐
newu_products        ──┼──► transform_data ──► load_to_supabase
muscleblaze_products ──┘

---

##  Technology Stack

- Apache Airflow  
- Playwright  
- BeautifulSoup  
- Docker  
- Supabase (PostgreSQL)  
- Redis  
- Python 3.12  

---

##  Scraped Websites

- IKEA India  
- NewU  
- MuscleBlaze  

---

##  How It Works

### Step 1 — Scraping
- Runs twice daily
- Extracts product data
- Saves JSON files

### Step 2 — Transform
- Merge and clean data
- Generate UUID
- Normalize structure

### Step 3 — Load
- Insert into Supabase using UPSERT

---

##  Docker Services

- airflow-webserver  
- airflow-scheduler  
- airflow-worker  
- postgres  
- redis  
- flower  

---

##  Setup

```bash
git clone https://github.com/dealwallet1/apache-airflow-scrape.git
cd apache-airflow-scrape
pip install uv
uv sync
```

Start:

```bash
docker-compose run --rm airflow-init
docker-compose up -d
```

---

##  Known Issues

- AJIO blocked (CDN issue)  
- Nike blocked (bot detection)  
- Temp file errors fixed using run_id  

---

##  Future Improvements

- Add more websites  
- Alerts (Slack/Email)  
- AWS deployment  
- Dashboard  

---

Dealwallet Internal Project 
