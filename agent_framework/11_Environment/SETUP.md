# Project Setup & Environment Requirements

> **For the complete A-Z project reproduction guide** (infrastructure → code → deploy → verify), see `Runbook.md` in this folder.

This document outlines the standard procedure for setting up the **local development environment** for the project.

## 1. Prerequisites
List all the required software and specific versions needed to run the project.

*   **Runtime:** Node.js (e.g., v20+), Python (e.g., v3.11+), etc.
*   **Package Manager:** npm, yarn, pnpm, pip, or poetry.
*   **Database:** PostgreSQL (e.g., v15), Redis, MongoDB, etc.
*   **Docker:** Recommended for standardizing local development (Docker Engine / Docker Compose).

## 2. Environment Variables (.env)
Explain where developers can find the environment variable templates and how to configure them.

1.  Copy the template file:
    ```bash
    cp .env.example .env
    ```
2.  Fill in the specific secret values or database connection strings for local development.
3.  **NEVER** commit the `.env` file to version control.

## 3. Installation & Setup
Step-by-step commands to get the application up and running from scratch.

```bash
# 1. Clone the repository
git clone <repository_url>
cd <project_name>

# 2. Install dependencies
npm install  # or yarn install / pip install -r requirements.txt

# 3. Spin up infrastructure (if using Docker)
docker-compose up -d database cache

# 4. Run database migrations and seed data
npm run db:migrate
npm run db:seed
```

## 4. Running the Application
Commands used for day-to-day development.

```bash
# Start the development server (with hot-reload)
npm run dev

# Run tests
npm test

# Run code linters/formatters
npm run lint
```

## 5. Troubleshooting & Common Issues
*   **Issue:** Port 3000 is already in use.
    *   **Solution:** Kill the process running on port 3000 or change the `PORT` variable in the `.env` file.
*   **Issue:** Database connection failed.
    *   **Solution:** Ensure Docker is running and the credentials in `.env` match `.env.example`.
