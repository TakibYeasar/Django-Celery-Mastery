FROM python:3.12-alpine

# Set the working directory in the container
WORKDIR /usr/src/app

# Prevent Python from writing .pyc files and ensure output is unbuffered
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# Install system dependencies
RUN apk update && apk add --no-cache \
    gcc \
    musl-dev \
    libffi-dev \
    postgresql-dev \
    curl \
    make \
    build-base \
    && pip install --upgrade pip

# Install Poetry
RUN curl -sSL https://install.python-poetry.org | python3 -

# Add Poetry to PATH
ENV PATH="/root/.local/bin:$PATH"

# Copy the project's Poetry files from the root (parent) directory
COPY ../pyproject.toml ../poetry.lock* /usr/src/app/

# Install dependencies with Poetry
RUN poetry install --no-dev --no-interaction --no-ansi

# Copy the rest of the application code
COPY . /usr/src/app

# Ensure entrypoint script is executable
RUN chmod +x /usr/src/app/entrypoint.sh

# Set the entrypoint script
ENTRYPOINT ["/usr/src/app/entrypoint.sh"]
