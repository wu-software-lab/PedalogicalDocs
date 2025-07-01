# Pedalogical Developer Environment Setup Guide

Welcome! This guide will walk you through setting up your local development environment for contributing to **Pedalogical**, an AI-enhanced testing and tutoring platform.

Repository: [https://github.com/wu-software-lab/AiTutor](https://github.com/wu-software-lab/AiTutor)

By the end of this guide, you will:

- Have cloned the repository
- Set up PostgreSQL and pgAdmin in Docker
- Installed .NET and other necessary tools
- Initialized and seeded the database
- Verified that you can run Pedalogical locally and log in

---

## Setup Steps

1. [Pre-requisites](./prerequisites.md)  
   Tools you need installed before starting, including Git, Docker, and .NET.

2. [Clone the Repository](./clone-repo.md)  
   How to fork and clone the Pedalogical GitHub repo.

3. [Set Up PostgreSQL + pgAdmin in Docker](./postgres_pgadmin_docker.md)  
   Instructions for creating a local Postgres container and admin GUI.

4. [Configure the App](./configure-app.md)  
   Setup of `appsettings.Development.json` for local development.

5. [Run Migrations & Seed the Database](./run-migrations.md)  
   Instructions for applying migrations and seeding the database.

6. [Run the Application](./run-app.md)  
   Build, run, and test the Pedalogical app locally.

---

## Final Check

Once you complete all steps, you should be able to:

- Navigate to `https://localhost:5001` (or specified port)
- Log in using seeded credentials
- Confirm the application runs as expected

---

Having trouble? Reach out to the team through Discord.
