FROM python:3.9-slim AS build

RUN apt-get update
RUN python -m venv /opt/venv
ENV PATH="/opt/venv/bin:$PATH"

COPY deployment/requirements.txt .
RUN pip install -r requirements.txt

FROM python:3.9-slim

RUN apt-get update && \
  apt-get install -y --no-install-recommends \
    openjdk-17-jre-headless && \
  apt-get autoremove -yqq --purge && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/*

ENV JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64

COPY --from=build /opt/venv /opt/venv
ENV PATH="/opt/venv/bin:$PATH"

COPY . /data_pipeline
WORKDIR /data_pipeline
