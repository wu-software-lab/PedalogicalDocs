# Step 5: Run Migrations & Seed the Database

Now that Postgres is running and your app is configured, you need to apply the database schema and seed initial data.

## 1. Open a Terminal

Navigate to the project root:

```bash
cd AiTutor
```

## 2. Apply Migrations

```bash
dotnet ef database update --project AiTutor
```

This will:
- Create the database schema in the container
- Apply any pending migrations
- Seed the database with initial data (including a test user)

**Troubleshooting tip**: If you get an error like `No project was found`, try adding the `--startup-project AiTutor` flag.

---

Once the database is seeded, continue to [Step 6: Run the Application](./run-app.md).
