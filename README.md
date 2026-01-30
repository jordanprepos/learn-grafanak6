# Learning Grafana and k6

This project is set up to help you learn Grafana, specifically in the context of load testing with k6.

## What is Grafana?

Grafana is an open-source platform for monitoring and observability. It allows you to query, visualize, alert on, and understand your metrics no matter where they are stored.

## What is k6?

k6 is a modern, developer-centric open-source load testing tool.

## Plan

1. Set up Grafana and a data source (InfluxDB) using Docker.
2. Write a basic k6 test.
3. Visualize k6 results in Grafana.

## How to Run

### 1. Start the Environment

Ensure Docker Desktop is running, then start the containers:

```bash
docker compose up -d
```

### 2. Run the k6 Test

Run the test and send results to the InfluxDB container:

```bash
# If you have k6 installed locally:
k6 run --out influxdb=http://localhost:8086/k6 test.js

# If you prefer using Docker:
docker run --rm -i -v $(pwd):/io grafana/k6 run --out influxdb=http://host.docker.internal:8086/k6 /io/test.js
```

### 3. View Results

- Open **Grafana**: [http://localhost:3000](http://localhost:3000)
- The **InfluxDB** datasource is already pre-configured!
- Create a new dashboard and select `InfluxDB` as the source.
-
<img width="2048" height="1280" alt="image" src="https://github.com/user-attachments/assets/358a54f8-bc72-4623-a829-b3883f16b4f4" />

## Troubleshooting

- **Docker API error**: Make sure Docker Desktop is open and the whale icon is steady.
- **Port 3000/8086 busy**: Check if another service is using these ports with `lsof -i :3000`.
