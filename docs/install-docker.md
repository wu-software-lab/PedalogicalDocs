# Installing Docker

This guide walks you through installing Docker on both **macOS** (using Homebrew) and **Windows**.

---

## Installing Docker on macOS (via Homebrew)

### Prerequisites

- macOS 11+ (Intel or Apple Silicon)
- [Homebrew](https://brew.sh/) installed

### Steps

1. **Install Docker Desktop**:

   ```bash
   brew install --cask docker-desktop
   ```

2. **Start Docker Desktop**:

   - Open `Docker` from your Applications folder.
   - Wait for it to say "Docker is running" in the menu bar.

3. **Test Installation**:

   ```bash
   docker --version
   ```

   You should see something like:  
   `Docker version 24.0.6, build ed223bc`

---

## Installing Docker on Windows

### Prerequisites

- Windows 10 64-bit: Pro, Enterprise, or Education (Build 15063 or later)
- Or Windows 11 (any edition)
- [WSL 2](https://learn.microsoft.com/en-us/windows/wsl/install) (for Windows Home)

### Steps

1. **Download Docker Desktop**:

   Go to [https://www.docker.com/products/docker-desktop/](https://www.docker.com/products/docker-desktop/) and download the Windows installer.

2. **Run the Installer**:

   - Follow the setup instructions.
   - Enable WSL 2 if prompted.

3. **Start Docker Desktop**:

   - Launch Docker from the Start Menu.
   - Wait for the whale icon to indicate it's running.

4. **Test Installation**:

   Open PowerShell or Command Prompt:

   ```bash
   docker --version
   ```

   Example output:  
   `Docker version 24.0.6, build ed223bc`

---

## Notes

- Docker Desktop includes Docker CLI, Docker Compose, and the Docker daemon.
- You can manage Docker containers directly or with GUI tools like [Docker Desktop Dashboard](https://docs.docker.com/desktop/).

---

## You’re Ready

Now you can start running containers, build images, and explore Dockerized development environments!
