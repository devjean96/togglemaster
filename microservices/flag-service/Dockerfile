# syntax=docker/dockerfile:1

FROM python:3.11-slim

ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1 \
    PORT=8082

WORKDIR /app

# Install dependencies before copying the application to improve build cache hits.
COPY requirements.txt .
RUN pip install --no-cache-dir --upgrade pip \
    && pip install --no-cache-dir -r requirements.txt \
    && adduser --disabled-password --gecos "" app

COPY . .

USER app

EXPOSE 8082

CMD ["sh", "-c", "gunicorn --bind 0.0.0.0:${PORT:-8082} --workers ${GUNICORN_WORKERS:-2} --threads ${GUNICORN_THREADS:-4} app:app"]
