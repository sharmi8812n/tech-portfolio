# 📊 Grafana – Monitoring & Visualization Platform

## Overview

**Grafana** is an open-source analytics and monitoring solution used to visualize time-series data. It supports a wide variety of data sources including Prometheus, InfluxDB, Elasticsearch, MySQL, PostgreSQL, and more.

Grafana is widely used for building dashboards that help monitor infrastructure, applications, and DevOps workflows in real-time.

---

## 🚀 Features

- 📈 **Interactive Dashboards**  
- 🔌 **Multiple Data Sources** (Prometheus, InfluxDB, MySQL, PostgreSQL, etc.)  
- 🔒 **User Access Control and Authentication**  
- 🛠 **Alerting System** with Notifications (Slack, Email, Teams)  
- 📦 **Plugins and Custom Panels**  
- 🧩 **Templating and Variables** for dynamic dashboards  
- ☁️ **Cloud or Self-hosted Deployments**

---

## 🏗️ Installation

## Docker (Recommended for quick start)
docker run -d -p 3000:3000 --name=grafana grafana/grafana
Visit: http://localhost:3000
Default login: admin / admin (you’ll be prompted to change it)



### Server Settings
/etc/grafana/grafana.ini

Key sections to configure:
```ini
[server]
http_port = 3000
domain = yourdomain.com
root_url = %(protocol)s://%(domain)s/


## 1. Access Grafana

Open your browser: http://localhost:3000
Login with default credentials and set a new password.

## 2. Add Data Source
Navigate to Configuration → Data Sources
Select a backend like Prometheus, InfluxDB, or MySQL
Enter connection details and save

## 3. Create Dashboard

Go to Create → Dashboard
Add a new Panel
Choose metrics and apply filters
Save your dashboard

## 4. Set Up Alerts

Configure alert rules within panels
Set thresholds and notification channels

## Docker Commands
# Run Grafana in Docker
docker run -d \
  -p 3000:3000 \
  --name=grafana \
  -e "GF_SECURITY_ADMIN_PASSWORD=secret" \
  grafana/grafana

# Stop container
docker stop grafana

# Start container
docker start grafana

Use Alerting → Contact points to integrate Slack, Email, Webhooks, etc.

<img width="814" height="325" alt="image" src="https://github.com/user-attachments/assets/c1cfb275-9d64-41a8-ada9-36e14d1213b3" />
