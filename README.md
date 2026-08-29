# Pattern Detect Analyzer - Docker Deployment

This repository provides the Docker Compose configuration for deploying the **Pattern Detect Analyzer** web application.

## What is Pattern Detect Analyzer?

Pattern Detect Analyzer is a web-based tool for analyzing PDF documents and automatically classifying them based on the software design pattern description format they follow. The application identifies documents that align with known formats such as Alexandrian, Coplien, GoF (Gang of Four), and others, based on structured text analysis.

It consists of the following components:

- A **React frontend** for uploading and interacting with PDFs.
- A **Spring Boot backend** that manages the core logic and PDF processing.
- A **Python microservice** responsible for extracting and analyzing text from PDFs.
- A **PostgreSQL database** used to store extracted data and metadata.

## Source Repositories

| Component | Repository |
|-----------|------------|
| Frontend | [pattern-detection-frontend](https://github.com/kostasfotos/pattern-detection-frontend) |
| Backend | [pattern-detect-backend](https://github.com/kostasfotos/pattern-detect-backend) |
| Python server | [pattern-detect-backend-pythonserver](https://github.com/kostasfotos/pattern-detect-backend-pythonserver) |

This deploy repo pulls pre-built images from Docker Hub. To build from source instead, use the `docker-compose.yml` in the backend repository.

## Repository Contents

- `docker-compose.yml` — Defines and orchestrates all required containers.
- `.env.example` — Template for environment variable configuration.
- `.gitignore` — Prevents `.env` and other sensitive files from being committed.

## Prerequisites

- [Docker](https://www.docker.com/products/docker-desktop)
- [Docker Compose](https://docs.docker.com/compose/)

## How to Deploy and Run the Application

Follow the steps below to run the application locally using Docker.

### Step 1: Clone the Repository

```bash
git clone https://github.com/kostasfotos/pattern-detect-analyzer-deploy.git
cd pattern-detect-analyzer-deploy
```

### Step 2: Create the `.env` file

Copy the example file and edit the values (at minimum, set a real database password):

```bash
cp .env.example .env
```

On Windows (PowerShell):

```powershell
Copy-Item .env.example .env
```

### Step 3: Start the Application with Docker

Make sure Docker Desktop is running, then pull the latest images and start the services:

```bash
docker compose pull
docker compose up -d
```

### Step 4: Open the Application

- **Web UI:** [http://localhost:3000](http://localhost:3000)
- **Backend API:** [http://localhost:8080](http://localhost:8080)

The frontend proxies API requests to the backend through nginx (`/api/` → Spring Boot).

### Step 5: Stop the Application

```bash
docker compose down
```

To also remove the database volume:

```bash
docker compose down -v
```

## Configuration

| Variable | Description | Default |
|----------|-------------|---------|
| `POSTGRES_DB` | PostgreSQL database name | `pattern_detect_db` |
| `POSTGRES_USER` | PostgreSQL username | — |
| `POSTGRES_PASSWORD` | PostgreSQL password | — |
| `SPRING_JPA_HIBERNATE_DDL_AUTO` | Hibernate schema mode | `update` |
| `UPLOAD_PARALLELISM` | Shared upload concurrency for Spring + Python (`auto` or `2`–`12`) | `auto` |
| `UPLOAD_RESOURCE_PROFILE` | Resource profile for auto-tuning (`auto`, `laptop`, etc.) | `auto` |
| `HOST_RAM_GB` | Optional RAM override for concurrency tuning | — |
| `APP_CORS_ALLOWED_ORIGIN` | Allowed CORS origins for the backend | `http://localhost:3000,http://localhost:5173` |

## Legacy Deployment

The pre-refactor deployment is preserved under the `v0.1.0-legacy` git tag:

```bash
git checkout v0.1.0-legacy
```

That version uses older images and a simpler environment configuration.
