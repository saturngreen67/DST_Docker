FROM python:3.12

ENV DEBIAN_FRONTEND=noninteractive

WORKDIR /app

# Install system dependencies (no software-properties-common)
RUN apt-get update -y && apt-get install -y --no-install-recommends \
    apt-transport-https \
    ca-certificates \
    gnupg \
    build-essential \
    curl \
    libgdal-dev \
    gdal-bin \
    libgeos-dev \
    libproj-dev \
    && rm -rf /var/lib/apt/lists/*

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY DST_Specific4.py .
COPY data/ data/

EXPOSE 8080
HEALTHCHECK CMD curl --fail http://localhost:8501/_stcore/health

ENTRYPOINT ["streamlit", "run", "DST_Specific4.py", "--server.port=8501", "--server.address=0.0.0.0"]
