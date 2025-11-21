# Start from a stable, slim Python base
FROM python:3.11-slim-bullseye

# Set environment variables to optimize Python
ENV PYTHONUNBUFFERED=1 \
    PYTHONDONTWRITEBYTECODE=1 \
    PIP_NO_CACHE_DIR=off \
    PIP_DISABLE_PIP_VERSION_CHECK=on

# Install common system dependencies and dev tools
RUN apt-get update && apt-get install -y --no-install-recommends \
    git \
    curl \
    bash \
    zsh \
    # Add any other common, system-level tools your team needs
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Install common Python development tools
RUN pip install --no-cache-dir \
    black \
    flake8 \
    pytest \
    mypy

# Create a non-root user for security
RUN useradd -m -s /bin/bash appuser
USER appuser

# Set a default working directory
WORKDIR /workspace