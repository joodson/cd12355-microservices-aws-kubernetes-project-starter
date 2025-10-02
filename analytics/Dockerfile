# Use Python slim image
FROM python:3.10-slim

# Install system dependencies for psycopg2
RUN apt-get update -y && apt-get install -y --no-install-recommends \
    build-essential libpq-dev && rm -rf /var/lib/apt/lists/*

# Set work directory
WORKDIR /app

# Install Python dependencies
COPY analytics/requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy application code
COPY analytics/ ./

# Run as non-root (good practice)
RUN useradd -m app && chown -R app:app /app
USER app

EXPOSE 5153
CMD ["python", "app.py"]
