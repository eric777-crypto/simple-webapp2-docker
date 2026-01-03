FROM python:3.6-slim

# OpenShift UID aléatoire
ENV HOME=/opt/app
WORKDIR /opt/app

# Dépendances système minimales
RUN apt-get update && apt-get install -y \
    gcc \
    libc-dev \
 && rm -rf /var/lib/apt/lists/*

# 🔑 Permissions OpenShift
RUN mkdir -p /opt/app \
 && chgrp -R 0 /opt/app \
 && chmod -R g=u /opt/app

# Outils Python compatibles MarkupSafe
RUN pip install --upgrade "pip<21" setuptools wheel

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 8080

# Non-root compatible
USER 1001

CMD ["flask", "run", "--host=0.0.0.0", "--port=8080"]
