---
title: "Step 3: Set Up PostgreSQL + pgAdmin in Docker"
format: gfm
---

# Step 3: Set Up PostgreSQL + pgAdmin in Docker

This step sets up a PostgreSQL database and pgAdmin using Docker, specifically configured for Pedalogical development.

> 📁 All Docker-related config and volume paths reference the `Docker/` directory inside the project repository.

## Create a Docker Network

```bash
docker network create pedalogical-network
```

This creates a private network that allows Docker containers (PostgreSQL, pgAdmin, and others) to communicate with each other by name.

## Run PostgreSQL Container

Navigate to the root of your **Pedalogical** repository, then run:

### macOS

```bash
docker run -d \
  --name pedalogical-db \
  --network pedalogical-network \
  -e POSTGRES_USER=pedalogical \
  -e POSTGRES_PASSWORD=devpass \
  -e POSTGRES_DB=pedalogical \
  -v $(pwd)/Docker/dbdata:/var/lib/postgresql/data \
  -p 5433:5432 \
  postgres:17
```

### Windows (PowerShell)

```powershell
docker run -d `
  --name pedalogical-db `
  --network pedalogical-network `
  -e POSTGRES_USER=pedalogical `
  -e POSTGRES_PASSWORD=devpass `
  -e POSTGRES_DB=pedalogical `
  -v ${PWD}\Docker\dbdata:/var/lib/postgresql/data `
  -p 5433:5432 `
  postgres:17
```

This runs the official Postgres container with:

- A persistent volume at `./docker/dbdata`
- Custom credentials and a default database
- Port `5433` exposed to avoid conflicts with local Postgres

## (Optional) Run pgAdmin Container

### macOS

```bash
docker run -d \
  --name pedalogical-pgadmin \
  --network pedalogical-network \
  -e PGADMIN_DEFAULT_EMAIL=admin@pedalogical.local \
  -e PGADMIN_DEFAULT_PASSWORD=admin \
  -v $(pwd)/Docker/pgadmin:/var/lib/pgadmin \
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
  -v ${PWD}\Docker\pgadmin:/var/lib/pgadmin `
  -p 5050:80 `
  dpage/pgadmin4
```

This will launch the pgAdmin web UI for managing the Postgres instance.

## Access pgAdmin

Open [http://localhost:5050](http://localhost:5050) and log in with:

- **Email**: `admin@pedalogical.local`
- **Password**: `admin`

Then, add a new server in pgAdmin:

- **Name**: `Pedalogical DB`
- **Host**: `pedalogical-db`
- **Port**: `5432`
- **Username**: `pedalogical`
- **Password**: `devpass`

## Next Step

Continue to [Step 4: Configure the App](./configure-app.md) to set up your connection string and local app settings.
