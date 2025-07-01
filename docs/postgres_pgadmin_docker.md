# Step 3: Set Up PostgreSQL + pgAdmin in Docker

This step sets up a PostgreSQL database and pgAdmin in Docker, specifically configured for Pedalogical development.

---

## Create a Docker Network

```bash
docker network create pedalogical-network
```

Creates a private network so your database and tools (like pgAdmin) can communicate using container names.

---

## Run PostgreSQL Container

### macOS

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

### Windows (PowerShell)

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

---

## (Optional) Run pgAdmin

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

---

## Access pgAdmin

- Navigate to: [http://localhost:5050](http://localhost:5050)
- Login with:
  - Email: `admin@pedalogical.local`
  - Password: `admin`

Add a new server:

- Name: `Pedalogical DB`
- Host: `pedalogical-db`
- Port: `5432`
- Username: `pedalogical`
- Password: `devpass`

---

Proceed to [Step 4: Configure the App](./configure-app.md).
