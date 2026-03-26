# Base image
FROM python:3.12-slim AS base

# Builder stage
FROM base AS builder

RUN apt-get update \
    && apt-get install -y --no-install-recommends g++ \
    && rm -rf /var/lib/apt/lists/*

# Install dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Final stage
FROM base

ENV PYTHONUNBUFFERED=1
ENV ENABLE_PROFILER=1

WORKDIR /email_service

# Copy installed packages
COPY --from=builder /usr/local/lib/python3.12/ /usr/local/lib/python3.12/

# Copy app
COPY . .

EXPOSE 8080

ENTRYPOINT ["python", "email_server.py"]