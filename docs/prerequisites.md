# Step 1: Pre-requisites

Before setting up the Pedalogical environment, make sure you have the following tools installed on your system.

## Required Tools

### 1. Git
Used for cloning and managing the project repository.

- **macOS**: Git is included with Xcode Command Line Tools
  ```bash
  xcode-select --install
  ```
- **Windows**: Download from [https://git-scm.com](https://git-scm.com)

---

### 2. Docker Desktop
Used to run PostgreSQL and pgAdmin containers.

- **macOS**:
  ```bash
  brew install --cask docker
  ```
- **Windows**: Download and install from [https://www.docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop)

---

### 3. .NET SDK (Version 8+)
Required to build and run the Pedalogical .NET application.

- Download and install from [https://dotnet.microsoft.com/en-us/download](https://dotnet.microsoft.com/en-us/download)

Verify installation:
```bash
dotnet --version
```

---

Once all tools are installed, proceed to [Step 2: Clone the Repository](./clone-repo.md).
