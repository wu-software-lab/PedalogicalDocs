# Installing PostgreSQL and pgAdmin in Docker Containers

This guide walks you through setting up PostgreSQL and pgAdmin using Docker containers, with separate instructions for macOS and Windows.

---

## Installing on macOS (using Homebrew and Docker Desktop)

### Prerequisites

- macOS 11 or higher
- Docker Desktop installed via Homebrew:
  ```bash
  brew install --cask docker-desktop
  ```
- Start Docker Desktop and ensure it's running

### Steps

1. **Create a Docker network** (optional but recommended):
   ```bash
   docker network create pg-network
   ```

2. **Run PostgreSQL container**:
   ```bash
   docker run -d \
     --name postgres-container \
     --network pg-network \
     -e POSTGRES_USER=admin \
     -e POSTGRES_PASSWORD=secret \
     -e POSTGRES_DB=mydb \
     -v ~/docker/postgres/data:/var/lib/postgresql/data \
     -p 5433:5432 \
     postgres:16
   ```

3. **Run pgAdmin container**:
   ```bash
   docker run -d \
     --name pgadmin-container \
     --network pg-network \
     -e PGADMIN_DEFAULT_EMAIL=admin@admin.com \
     -e PGADMIN_DEFAULT_PASSWORD=admin \
     -v ~/docker/pgadmin:/var/lib/pgadmin \
     -p 5050:80 \
     dpage/pgadmin4
   ```

4. **Access pgAdmin**:
   - Open a browser and go to `http://localhost:5050`
   - Login with:
     - Email: `admin@admin.com`
     - Password: `admin`

5. **Add PostgreSQL server in pgAdmin**:
   - Host: `postgres-container`
   - Port: `5432`
   - Username: `admin`
   - Password: `secret`

---

## Installing on Windows

### Prerequisites

- Windows 10 or 11 with Docker Desktop installed
- WSL 2 enabled for Windows Home edition
- Docker Desktop running

### Steps

1. **Create a Docker network** (optional but recommended):
   ```powershell
   docker network create pg-network
   ```

2. **Run PostgreSQL container**:
   ```powershell
   docker run -d `
     --name postgres-container `
     --network pg-network `
     -e POSTGRES_USER=admin `
     -e POSTGRES_PASSWORD=secret `
     -e POSTGRES_DB=mydb `
     -v %USERPROFILE%\docker\postgres\data:/var/lib/postgresql/data `
     -p 5433:5432 `
     postgres:16
   ```

3. **Run pgAdmin container**:
   ```powershell
   docker run -d `
     --name pgadmin-container `
     --network pg-network `
     -e PGADMIN_DEFAULT_EMAIL=admin@admin.com `
     -e PGADMIN_DEFAULT_PASSWORD=admin `
     -v %USERPROFILE%\docker\pgadmin:/var/lib/pgadmin `
     -p 5050:80 `
     dpage/pgadmin4
   ```

4. **Access pgAdmin**:
   - Open your browser and go to `http://localhost:5050`
   - Login with:
     - Email: `admin@admin.com`
     - Password: `admin`

5. **Add PostgreSQL server in pgAdmin**:
   - Host: `postgres-container`
   - Port: `5432`
   - Username: `admin`
   - Password: `secret`

---

## Notes

- Adjust the port mapping (`-p`) if port 5432 is in use.
- Docker volumes used above ensure your data persists across restarts.
- Use `docker logs` and `docker exec` for debugging if needed.

---

## Cleanup Commands

To stop and remove the containers:

```bash
docker stop pgadmin-container postgres-container
docker rm pgadmin-container postgres-container
```

To remove volumes:

```bash
docker volume prune
```

---

## You're Ready

Your Dockerized PostgreSQL and pgAdmin environment is now running and accessible locally.
