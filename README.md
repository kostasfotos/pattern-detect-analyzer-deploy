# Pattern Detect Analyzer - Docker Deployment

This repository provides the Docker Compose configuration for deploying the **Pattern Detect Analyzer** web application.

## What is Pattern Detect Analyzer?

Pattern Detect Analyzer is a web-based tool for analyzing PDF documents and automatically classifying them based on the software design pattern description format they follow.
The application identifies documents that align with known formats such as Alexandrian, Coplien, GoF (Gang of Four), and others, based on structured text analysis.

It consists of the following components:
- A **React frontend** for uploading and interacting with PDFs.
- A **Spring Boot backend** that manages the core logic and PDF processing.
- A **Python microservice** responsible for extracting and analyzing text from PDFs.
- A **PostgreSQL database** used to store extracted data and metadata.

## Repository Contents

This repository contains a single file:

- `docker-compose.yml`: Defines and orchestrates all required containers.
- `.env.example`: Template for environment variable configuration.
- `.gitignore`: Prevents `.env` and other sensitive files from being committed.

## Prerequisites

- [Docker](https://www.docker.com/products/docker-desktop)
- [Docker Compose](https://docs.docker.com/compose/)

## How to Deploy and Run the Application

Follow the steps below to run the application locally using Docker.

### Step 1: Clone the Repository

Open your terminal and run:

	```bash
	git clone https://github.com/kostasfotos/pattern-detect-analyzer-deploy.git
	cd pattern-detect-analyzer-deploy
	

### Step 2: Create the .env file

You can create the .env file using the included example file.

### Step 3: Start the Application with Docker

Make sure Docker Desktop is running, then start the services:

	```bash
	docker-compose up -d
	
