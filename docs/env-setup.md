# Environment Variables Setup

This guide explains how to set up environment variables for development using a `.env` file, which contains sensitive configuration like database credentials and API keys.

---

## Why Use `.env`?

- Keeps sensitive values (like API keys) out of source control
- Works cross-platform (Windows and macOS)
- Compatible with tools like `DotNetEnv` in .NET

---

## Step 1: Copy the Example File

From the root of the repository, copy the provided template:

```bash
cp .env.example .env
```

Then, open `.env` and fill in your actual credentials and configuration values.

---

## Step 2: Configure for Your Setup

Depending on your development environment, your PostgreSQL connection will differ.

### macOS: Using Docker

If you're running PostgreSQL in Docker (recommended):

```env
PG_HOST=localhost
PG_PORT=5433
PG_DB=pedalogical
PG_USER=pedalogical
PG_PASS=devpass
```

### macOS: Native PostgreSQL

If you're running a local Postgres installation directly (e.g., via Homebrew):

```env
PG_HOST=localhost
PG_PORT=5432
PG_DB=pedalogical
PG_USER=your-local-user
PG_PASS=your-local-password
```

---

### Windows: Using Docker

If you're using Docker on Windows:

```env
PG_HOST=localhost
PG_PORT=5433
PG_DB=pedalogical
PG_USER=pedalogical
PG_PASS=devpass
```

### Windows: Native PostgreSQL

If you're using a direct install of PostgreSQL:

```env
PG_HOST=localhost
PG_PORT=5432
PG_DB=pedalogical
PG_USER=your-local-user
PG_PASS=your-local-password
```

---

## Step 3: Load the `.env` File in .NET

Install the [DotNetEnv](https://github.com/tonerdo/dotenv) package in your .NET project:

```bash
dotnet add package dotenv.net
```

Then in `Program.cs` or at startup:

```csharp
DotNetEnv.Env.Load();
```

You can now access values like:

```csharp
var connString = Environment.GetEnvironmentVariable("PG_CONNECTION_STRING");
```

Or build it manually using individual environment variables.

---

## Step 4: Keep `.env` Secure

Make sure `.env` is in your `.gitignore`:

```bash
# .gitignore
.env
```

Only share `.env.example`, which contains placeholders and no sensitive data.

---

## You're Ready

With your `.env` configured and secrets loaded at runtime, you're now using a flexible and secure setup that works across macOS, Windows, Docker, and local PostgreSQL.
