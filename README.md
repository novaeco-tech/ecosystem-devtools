# Nova Ecosystem DevTools

This repository hosts shared developer tooling, Docker images, and scripts used across the Nova Ecosystem organization.

## 🛠️ Nova CLI

The **Nova CLI** (package: `nova-ecosystem-cli`) is our internal Python tool used to manage versioning, releases, and automation across our monorepos and microservices.

### Installation

Since this is an internal tool, we install it directly from the repository source. You do not need to configure a private registry.

**1. Install the latest version:**
```bash
# Note: The package is located in the 'nova-cli' subdirectory
pip install "git+https://github.com/nova-ecosystem/ecosystem-devtools.git@main#subdirectory=nova-cli"
````

**2. Update to the latest version:**
If a teammate pushes a fix, run this to update your local machine:

```bash
pip install --upgrade "git+https://github.com/nova-ecosystem/ecosystem-devtools.git@main#subdirectory=nova-cli"
```

### Usage

**1. Patching a Service**
Used when fixing bugs. Increments the patch version (e.g., `1.0.0` -\> `1.0.1`) for a specific service.

```bash
# Syntax: nova version patch <service_name>
nova version patch auth
nova version patch api
```

**2. Creating a Release**
Used when shipping new features.
Increments the Global version and aligns **all** services in the repository to the new version (e.g., `1.1.0`).

```bash
# Syntax: nova version release <minor|major>
nova version release minor
```

-----

## 🐳 Shared Docker Images

We maintain standard development images to ensure consistency across all engineers' machines.
These are automatically built and pushed to GHCR (GitHub Container Registry) whenever the `docker/` directory changes.

| Image | Tag | Description |
| :--- | :--- | :--- |
| `ghcr.io/nova-ecosystem/dev-python` | `latest` | Python 3.10, Flask, Pytest, and common utilities. |
| `ghcr.io/nova-ecosystem/dev-node` | `latest` | Node.js 18, npm, and Docusaurus support. |

**Usage in `devcontainer.json`:**

```json
"image": "ghcr.io/nova-ecosystem/dev-python:latest"
```

-----

## 👩‍💻 Contributing to DevTools

### Developing the CLI

If you want to add new commands to the `nova` tool:

1.  Clone this repository.
2.  Install the package in "editable" mode (changes are reflected immediately):
    ```bash
    cd nova-cli
    pip install -e .
    ```
3.  Add your new module in `src/nova_cli/commands/`.
4.  Register the command in `src/nova_cli/main.py`.

### Publishing Updates

  * **Docker Images:** Push changes to the `docker/` folder to trigger a rebuild and publish to GHCR.
  * **Nova CLI:** Simply push changes to the `nova-cli/` folder on the `main` branch. Everyone using the "Git Install" method will receive the updates the next time they run the upgrade command or rebuild their DevContainer.