
# Attendance API

| Author | Created On | Version | Last Updated By | Last Edited On |
|--------|------------|---------|-----------------|----------------|
| Sachin Rajput | 21-04-2026 | V1.0 | Sachin | 21-04-2026 |

---

## Table of Contents
1. [Purpose](#1-purpose)
2. [Pre-requisites](#2-pre-requisites)
   - [System Requirements](#21-system-requirements)
   - [Build Time Dependencies](#22-build-time-dependencies)
   - [Runtime Dependencies](#23-runtime-dependencies)
3. [Important Ports](#3-important-ports)
4. [Architecture](#4-architecture)
5. [Step by step Setup](#5-step-by-step-setup)
   - [Step 1: Update System](#step-1-update-system)
   - [Step 2: Install Python](#step-2-install-python-311)
   - [Step 3: Install Poetry](#step-3-install-poetry)
   - [Step 4: Install PostgreSQL](#step-4-install-postgresql)
     - [Create Database & User](#create-database--user)
   - [Step 5: Install Redis](#step-5-install-redis-optional)
   - [Step 6: Install Liquibase](#step-6-install-liquibase)
   - [Step 7: Clone Repository](#step-7-clone-repository)
   - [Step 8: Configure Application](#step-8-configure-application)
   - [Step 9: Install Dependencies](#step-9-install-dependencies)
   - [Step 10: Run Database Migrations](#step-9-install-dependencies)
   - [Step 10: Run Database Migrations](#step-10-run-database-migrations)
   - [Step 11: Start the Application](#step-11-start-the-application)
   - [Step 12: Verify](#step-12-verify)
6. [Troubleshooting](#6-troubleshooting)
7. [Contact](#7-contact)
8. [References](#8-references)

## 1. Purpose

The Attendance API is a Python-based microservice that is part of the OT-Microservices stack. It is responsible for handling all attendance-related transactions and data management within the organization. This microservice follows a RESTful architecture and provides endpoints for creating, reading, updating, and deleting attendance records.

The need for a dedicated Attendance microservice arises from the requirement to:

- Decouple attendance management from other HR functions
- Enable independent scaling of the attendance module
- Provide a single source of truth for all attendance data
- Support cross-platform deployment with minimal runtime dependencies

---

## 2. Pre-requisites

Before diving into the Attendance API deployment, ensure the following requirements are fulfilled.

### 2.1 System Requirements

| Hardware Specification | Minimum Recommendation |
|------------------------|------------------------|
| Processor | Dual-core (2 GHz+) |
| RAM | 4 GB |
| Disk | 20 GB free space |
| OS | Ubuntu 22.04 LTS |

### 2.2 Build Time Dependencies

| Name | Version | Description |
|------|---------|-------------|
| Python | 3.11+ | Core runtime for the application |
| Poetry | 1.6+ | Python package and dependency manager |
| Make | 4.3+ | Build automation tool |
| Git | 2.x | Version control to clone the repository |

### 2.3 Runtime Dependencies

| Name | Version | Description |
|------|---------|-------------|
| PostgreSQL | 14+ | Primary database for storing attendance records (Mandatory) |
| Redis | 6.x+ | Cache layer for improved response time (Optional) |
| Liquibase | 4.x+ | Database schema migration tool |

---
## 3. Important Ports

| Port | Description |
|------|-------------|
| 8080 | Attendance API (Swagger UI) |
| 5432 | PostgreSQL |
| 6379 | Redis (optional) |

---
## 4. Architecture

The Attendance API follows a layered microservice architecture. Incoming HTTP requests are handled by the REST API layer (Flask/Flasgger), processed through the business logic layer, and persisted in PostgreSQL. Redis is optionally used as a caching layer to improve read performance.

<!-- Add Architecture Diagram Screenshot here -->
>  **Screenshot:** Architecture Diagram

---

## 5. Step by step Setup

### Step 1: Update System

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y git make curl wget software-properties-common
```
# 1
---

### Step 2: Install Python 3.11

```bash
sudo add-apt-repository ppa:deadsnakes/ppa -y
sudo apt update
sudo apt install -y python3.11 python3.11-venv python3.11-dev

# Verify
python3.11 --version
```

---

### Step 3: Install Poetry

```bash
curl -sSL https://install.python-poetry.org | python3 -

# Add to PATH
export PATH="$HOME/.local/bin:$PATH"
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc

# Verify
poetry --version
```
# 2
---

### Step 4: Install PostgreSQL

```bash
sudo apt install -y postgresql postgresql-contrib
sudo systemctl start postgresql
sudo systemctl enable postgresql

# Verify
sudo systemctl status postgresql
```
# 3

#### Create Database & User

```bash
sudo -i -u postgres psql
```

```sql
CREATE USER attendanceuser WITH PASSWORD 'password';
CREATE DATABASE attendance;
CREATE DATABASE attendancedb OWNER attendanceuser;
GRANT ALL PRIVILEGES ON DATABASE attendancedb TO attendanceuser;

# Verify
\l

#Exit
\q
```




---

### Step 5: Install Redis (Optional)

```bash
sudo apt install -y redis-server
sudo systemctl start redis-server
sudo systemctl enable redis-server

# Test
redis-cli ping
# Expected: PONG
```

---

### Step 6: Install Liquibase

```bash
wget https://github.com/liquibase/liquibase/releases/download/v4.25.0/liquibase-4.25.0.tar.gz
sudo mkdir -p /opt/liquibase
sudo tar -xzf liquibase-4.25.0.tar.gz -C /opt/liquibase

echo 'export PATH="/opt/liquibase:$PATH"' >> ~/.bashrc
source ~/.bashrc

# Verify
liquibase --version
```

---

### Step 7: Clone Repository

```bash
git clone https://github.com/OT-MICROSERVICES/attendance-api.git
cd attendance-api
```
# 4
---

### Step 8: Configure Application

Edit `config.yaml` with your database details:

```yaml
server:
  port: 8080

postgres:
  host: "localhost"
  port: 5432
  user: "attendanceuser"
  password: "password"
  database: "attendancedb"

redis:
  host: "localhost"
  port: 6379
  password: ""

```

---

### Step 9: Install Dependencies

```bash
poetry add pyyaml@latest
```
# 5
---

### Step 10: Run Database Migrations

Edit `liquibase.properties`:

```properties
url=jdbc:postgresql://localhost:5432/attendancedb
username=attendanceuser
password=password
driver=org.postgresql.Driver
changeLogFile=migration/db.changelog-master.xml
```


Then run:

```bash
make run-migrations
```
# 6
---

### Step 11: Start the Application

```bash
poetry run gunicorn app:app --log-config log.conf -b 0.0.0.0:8080
```
# 7

---

### Step 12: Verify

```bash
# Health check
curl http://localhost:8080/api/v1/attendance/health/detail
```
# 8

Swagger UI:
```
http://<server-ip>:8080/apidocs
```
# 9
---

## 6. Troubleshooting

| Issue | Fix |
|-------|-----|
| PostgreSQL connection refused | `sudo systemctl start postgresql` |
| Poetry not found | `export PATH="$HOME/.local/bin:$PATH"` |
| Port 8080 already in use | `sudo lsof -i :8080` then `sudo kill -9 <PID>` |
| Liquibase migration fails | Check DB credentials in `liquibase.properties` |

---

## 7. Contact

| Name | Email Address |
| ------------- | ------------- |
| Sachin Rajput | [sachin.rajput.snaatak@mygurukulam.co](mailto:sachin.rajput.snaatak@mygurukulam.co) |

Samajh gaya 👍 — tum chahte ho niche wale references ko **same table format** me convert karna (jaise upar wala hai). Ye raha clean format 👇

---

## 8. References

| Resource Name             | Link                                                                                                     |
| ------------------------- | -------------------------------------------------------------------------------------------------------- |
| Attendance API Repository | [https://github.com/OT-MICROSERVICES/attendance-api](https://github.com/OT-MICROSERVICES/attendance-api) |
| Poetry Documentation      | [https://python-poetry.org/docs/](https://python-poetry.org/docs/)                                       |
| PostgreSQL 14 Docs        | [https://www.postgresql.org/docs/14/](https://www.postgresql.org/docs/14/)                               |
| Liquibase Docs            | [https://docs.liquibase.com/](https://docs.liquibase.com/)                                               |

---
