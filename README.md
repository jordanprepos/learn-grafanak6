# 📊 Grafana + k6 Load Testing Lab

A streamlined environment for learning and executing load tests using **k6** and visualizing results in **Grafana** via **InfluxDB**.

## 🚀 Quick Start

### 1. Prerequisites

- **Docker Desktop**: Ensure it is installed and running.
- **k6 (Optional)**: If you want to run tests locally without Docker, install it via Homebrew: `brew install k6`.

### 2. Start the Infrastructure

Spin up the Grafana and InfluxDB containers:

```bash
docker compose up -d
```

### 3. Run Your First Test

You can run the load test script specifically designed for this lab:

**Using Docker (Recommended - No installation needed):**

```bash
docker compose run k6
```

**Using Local k6 (If installed):**

```bash
k6 run --out influxdb=http://localhost:8086/k6 test.js
```

### 4. Visualize the Data

1. Open your browser and go to: [**http://localhost:3000**](http://localhost:3000)
2. Login with credentials:
   - **Username**: `admin`
   - **Password**: `admin`
3. Click the **Explore** icon (compass) in the sidebar.
4. Select **InfluxDB** from the dropdown menu at the top.
5. Start querying metrics like `http_req_duration`!

---

## 📂 Project Structure

- `docker-compose.yml`: Defines the InfluxDB, Grafana, and k6 services.
- `test.js`: A sample k6 script that performs 10 VUs (Virtual Users) load testing against `test.k6.io`.
- `datasource.yaml`: Automatically configures InfluxDB as a data source in Grafana upon startup.
- `.gitignore`: Prevents OS pollution and local database files from being tracked by Git.

---

## 🛠 Useful Commands

| Action              | Command                                 |
| :------------------ | :-------------------------------------- |
| **Start Services**  | `docker compose up -d`                  |
| **Stop Services**   | `docker compose stop`                   |
| **Stop and Remove** | `docker compose down`                   |
| **Wipe All Data**   | `docker compose down -v`                |
| **Check Logs**      | `docker compose logs -f [service_name]` |

---

## ❓ Troubleshooting

- **Docker API Error**: Ensure the Docker Desktop app is open and the whale icon in your menu bar is steady.
- **Port Conflict**: If localhost:3000 is taken, ensure no other Grafana or web services are running (`lsof -i :3000`).
- **Data Not Showing**: Ensure you ran the k6 test _after_ the containers were up and running.
- **M1/M2 Mac Issues**: This project is optimized for Apple Silicon using the official `grafana/k6` image.

---

_Created by [jordanprepos](https://github.com/jordanprepos)_
