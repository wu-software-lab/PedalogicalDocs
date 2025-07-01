# Step 4: Configure the App

## 1. Locate or Create the Development Config

In the root project folder, ensure you have a file named:

```text
appsettings.Development.json
```

If it doesn’t exist, create one based on the existing `appsettings.json` or copy this template:

```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Host=pedalogical-db;Port=5432;Database=pedalogical;Username=pedalogical;Password=devpass"
  },
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft": "Warning",
      "Microsoft.Hosting.Lifetime": "Information"
    }
  }
}
```

This tells the app how to connect to your Dockerized Postgres instance.

---

Move on to [Step 5: Run Migrations & Seed the Database](./run-migrations.md).
