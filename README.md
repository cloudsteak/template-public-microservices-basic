# Template Repository

## Table of Contents

- [Overview](#overview)
- [Initialize your Python Project](#initialize-your-python-project)
    - [Prerequisites](#prerequisites)
    - [Initialize the Project](#initialize-the-project)
    - [Common UV Commands](#common-uv-commands)
- [Workflows](#workflows)

## Overview

## Initialize your Python Project

This project uses [UV](https://docs.astral.sh/uv/) - a fast Python package installer and resolver with **Python 3.12**.

### Prerequisites

Install UV:

```bash
# macOS - Homebrew (recommended)
brew install uv

# macOS/Linux - Official installer
curl -LsSf https://astral.sh/uv/install.sh | sh

# Windows
powershell -c "irm https://astral.sh/uv/install.ps1 | iex"

# Or via pip
pip install uv
```

### Initialize the Project

```bash
# Initialize a new Python project with UV
uv init

# Create a virtual environment with Python 3.12
uv venv --python 3.12

# Install/sync dependencies (UV automatically uses the virtual environment)
uv sync

# Note: You don't need to manually activate the venv!
# UV commands automatically detect and use the .venv directory

# If you still want to manually activate:
# macOS/Linux: source .venv/bin/activate
# Windows: .venv\Scripts\activate
```

### Common UV Commands

```bash
# Add a new dependency
uv add <package-name>

# Add a development dependency
uv add --dev <package-name>

# Update dependencies
uv lock --upgrade

# Run a command in the virtual environment
uv run <command>

# Install all dependencies
uv sync
```

## Workflows

Available workflows in this repository:

### 1. New Release - Manual

- **File:** [.github/workflows/create-release.yml](.github/workflows/create-release.yml)
- **Trigger:** Manual (workflow_dispatch)
- **Description:** Creates a new release with semantic versioning
- **Options:**
  - **patch** - Bug fixes and minor changes (e.g., 1.0.0 → 1.0.1)
  - **minor** - New features, backward compatible (e.g., 1.0.0 → 1.1.0)
  - **major** - Breaking changes (e.g., 1.0.0 → 2.0.0)
- **Uses:** `cloudsteak/cm-workflows/.github/workflows/new-release.yml@1.3.0`

### 2. Production Build & Push - Manual

- **File:** [.github/workflows/prod-build.yml](.github/workflows/prod-build.yml)
- **Trigger:** Manual (workflow_dispatch)
- **Description:** Manually triggers a production build and pushes the Docker image
- **Image Name:** Uses the repository name as the image name
- **Uses:** `cloudsteak/cm-workflows/.github/workflows/production-build-push.yml@1.3.0`

### 3. Staging Build & Push - Automatic

- **File:** [.github/workflows/staging-build.yml](.github/workflows/staging-build.yml)
- **Trigger:** Automatic on push to `main` branch
- **Monitored Files:**
  - `Dockerfile`
  - `pyproject.toml`
  - `poetry.lock`
  - `.github/workflows/staging-build.yml`
- **Description:** Automatically builds and pushes staging Docker images when monitored files are updated
- **Image Name:** Uses the repository name as the image name
- **Uses:** `cloudsteak/cm-workflows/.github/workflows/staging-build-push.yml@1.3.0`
