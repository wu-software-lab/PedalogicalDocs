# Setting Up PostgreSQL for Pedalogical in Docker

This guide walks you through setting up a PostgreSQL database using Docker for use with the **Pedalogical** .NET application.

---

## Overview

The Pedalogical app uses PostgreSQL as its development database. By using Docker, we can:

- Isolate our database from local installations
- Ensure a consistent environment for all developers
- Easily tear down or rebuild the database without affecting the rest of your system

This guide assumes you're using **macOS with Homebrew** or **Windows with Docker Desktop**.

---

## Step 1: Create a Docker Network (Optional but Recommended)

```bash
docker network create pedalogical-network
```

**What this does:**  
Creates a private network so containers (like the database and potentially other services) can talk to each other by name (e.g., `pedalogical-db`). This simplifies networking between services.

---

## Step 2: Run PostgreSQL Container

### On macOS (Homebrew + Docker)

```bash
docker run -d \
  --name pedalogical-db \
  --network pedalogical-network \
  -e POSTGRES_USER=pedalogical \
  -e POSTGRES_PASSWORD=devpass \
  -e POSTGRES_DB=pedalogical \
  -v ~/Projects/Pedalogical/docker/dbdata:/var/lib/postgresql/data \
  -p 5433:5432 \
  postgres:16
```

### On Windows (Docker Desktop PowerShell)

```powershell
docker run -d `
  --name pedalogical-db `
  --network pedalogical-network `
  -e POSTGRES_USER=pedalogical `
  -e POSTGRES_PASSWORD=devpass `
  -e POSTGRES_DB=pedalogical `
  -v ${env:USERPROFILE}\Projects\Pedalogical\docker\dbdata:/var/lib/postgresql/data `
  -p 5433:5432 `
  postgres:16
```

**What this does:**

- Names the container `pedalogical-db`
- Sets up database credentials and creates the `pedalogical` database automatically
- Mounts a local folder to persist data across restarts
- Maps port `5433` on your machine to `5432` inside the container to avoid conflicts
- Attaches the container to the `pedalogical-network`

---

## Step 3: Connect from the Pedalogical .NET App

In your `appsettings.Development.json`, update your connection string:

```json
"ConnectionStrings": {
  "DefaultConnection": "Host=pedalogical-db;Port=5432;Database=pedalogical;Username=pedalogical;Password=devpass"
}
```

**Why this works:**

- `pedalogical-db` is the container name, resolved via the Docker network
- `.NET` will connect to the internal container port `5432`, not the host port

---

## Step 4: Optional — Run pgAdmin for GUI Access

### macOS

```bash
docker run -d \
  --name pedalogical-pgadmin \
  --network pedalogical-network \
  -e PGADMIN_DEFAULT_EMAIL=admin@pedalogical.local \
  -e PGADMIN_DEFAULT_PASSWORD=admin \
  -v ~/Projects/Pedalogical/docker/pgadmin:/var/lib/pgadmin \
  -p 5050:80 \
  dpage/pgadmin4
```

### Windows (PowerShell)

```powershell
docker run -d `
  --name pedalogical-pgadmin `
  --network pedalogical-network `
  -e PGADMIN_DEFAULT_EMAIL=admin@pedalogical.local `
  -e PGADMIN_DEFAULT_PASSWORD=admin `
  -v ${env:USERPROFILE}\Projects\Pedalogical\docker\pgadmin:/var/lib/pgadmin `
  -p 5050:80 `
  dpage/pgadmin4
```

**What this does:**

- Starts the pgAdmin GUI tool for managing Postgres visually
- Accessible at [http://localhost:5050](http://localhost:5050)

### Add Server in pgAdmin

- Host: `pedalogical-db`
- Port: `5432`
- Username: `pedalogical`
- Password: `devpass`

---

## Step 5: Verify Everything is Working

You can check that the container is running:

```bash
docker ps
```

You can log into the container's database directly:

```bash
docker exec -it pedalogical-db psql -U pedalogical -d pedalogical
```

---

## Cleanup Commands

To stop and remove the containers:

```bash
docker stop pedalogical-pgadmin pedalogical-db
docker rm pedalogical-pgadmin pedalogical-db
```

To clear volumes (be careful — this deletes data):

```bash
docker volume prune
```

---

## You're Ready

You now have a Postgres database running in Docker for the Pedalogical project, with pgAdmin GUI access and .NET integration via Docker networking.
