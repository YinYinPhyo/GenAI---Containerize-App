# GenAI---Containerize-App

# Generative AI Application Development Environment Setup

This repository contains the necessary steps to set up and run a Generative AI (GenAI) application. The setup includes configuring a local database and connecting to a local or remote LLM (Large Language Model) service.

---

## Prerequisites
- Complete the "Containerize a Generative AI Application" guide.
- Install Docker and Docker Compose.

---

## Overview
This guide covers:
1. Adding a local Neo4j database using containers.
2. Configuring a local or remote LLM service (e.g., Ollama or OpenAI).
3. Running your GenAI application using Docker Compose.

---

## Setup Instructions

### 1. Add a Local Database
To set up a Neo4j database service:

1. Rename the `env.example` file to `.env`.
   ```bash
   mv env.example .env
   ```
2. Update the compose.yaml file to include the Neo4j database service:
    ```yaml
    services:
        database:
            image: neo4j:5.11
            ports:
            - "7474:7474"
            - "7687:7687"
            environment:
            - NEO4J_AUTH=${NEO4J_USERNAME}/${NEO4J_PASSWORD}
            healthcheck:
            test: ["CMD-SHELL", "wget --no-verbose --tries=1 --spider localhost:7474 || exit 1"]
            interval: 5s
            timeout: 3s
            retries: 5
    ```
3. Start the database service:
    ```bash
    docker compose up --build
    ```
### 2. Add a local or remote LLM service
For this application, you can use Ollama or OpenAI as the LLM service. I use Ollama in this documentation. I’m using macOS environment, so I’ll run Ollama outside of a container.
You can download or manually install Ollama via this link
https://ollama.com/download/mac

### 3. Run the GenAI Application
Start all services:
```bash
docker compose up --build
```

Open a browser and access the application at http://localhost:8000.

Upload a PDF and ask a question about the content.