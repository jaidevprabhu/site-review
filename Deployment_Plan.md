# 🧭 Deployment Plan: Modular Stock Insights Chatbot

## Overview
This document outlines the deployment strategy for a modular, containerized application hosted on a single EC2 instance. The application consists of four independently developed Docker containers, each responsible for a distinct phase of the system.

---

## 🧱 Container Modules

| Module         | Description                                      | Language | Dependencies |
|----------------|--------------------------------------------------|----------|--------------|
| Analyzer       | Selects top 20–25 S&P 500 stocks + 3 sectors     | Python   | pandas, TA-lib |
| Scraper        | Scrapes Yahoo Finance data for selected tickers  | Python   | requests, BeautifulSoup |
| RAG Engine     | Embeds, stores, and retrieves data for chatbot   | Python   | OpenAI API, Chroma |
| UI Frontend    | Streamlit-based chatbot interface                | Python   | Streamlit, Plotly |

---

## 🧪 Development Workflow

1. **Local Development**
   - Each module is developed and tested independently on local machines.
   - Dockerfiles are maintained per module for reproducibility.

2. **Version Control**
   - All code is stored in a GitHub repository with separate folders per module.
   - Branching strategy: `main`, `dev`, `feature/*`

3. **CI/CD Pipeline**
   - GitHub Actions configured to:
     - Build Docker images
     - Run tests
     - Push images to Docker Hub or EC2 via SSH
     - Restart containers on EC2

4. **Deployment Target**
   - EC2 instance (Ubuntu 22.04) with Docker and Docker Compose installed
   - Containers orchestrated via `docker-compose.yml`
   - Optional: Nginx reverse proxy for routing

---

## 🔐 Configuration & Secrets

- Environment variables stored in `.env` files
- Optional: Use AWS Secrets Manager for API keys and credentials

---

## 📈 Monitoring & Logging

- Each container logs to stdout/stderr
- Logs aggregated via Docker logging driver or external service (e.g., Loki, CloudWatch)

---

## 🔄 Update Strategy

- Code changes pushed to GitHub trigger CI/CD pipeline
- Containers rebuilt and redeployed automatically
- Rollback supported via previous image tags

---

## 🧩 Future Enhancements

- Migrate to ECS or EKS for managed container orchestration
- Add autoscaling and load balancing
- Implement user authentication and role-based access

---

## ✅ Status

- Analyzer module complete and tested
- RAG Engine functional with OpenAI embeddings and GPT-4o-mini
- UI operational via Streamlit; aesthetic improvements planned
- Scraper module in progress

