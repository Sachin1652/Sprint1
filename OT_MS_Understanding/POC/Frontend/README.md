<h1 align="center">Frontend - POC </h1>

## Document Details

| Author | Created | Version | Last Updated By | Last Edited On | L0 Reviewer | L1 Reviewer | L2 Reviewer |
| -------------- | ---------- | ------- | --------------- | -------------- | ----------- | ----------- | ----------- |
| Sachin Rajput | 2026-04-22 | 1.0 | Sachin Rajput | 2026-04-22 | Anitha Annem | Shreya Jaiswal | Ashwani Singh |


---

## Table of Contents

- [Purpose](#1-purpose)
- [System Requirements](#2-system-requirements)
- [Dependencies](#3-dependencies)
  - [Build Time Dependency](#31-build-time-dependency)
  - [Run Time Dependency](#32-run-time-dependency)
  - [Other Dependency](#33-other-dependency)
- [Important Ports](#4-important-ports)
- [Architecture](#5-architecture)
- [Dataflow Diagram](#6-dataflow-diagram)
- [Step-by-step Installation](#7-step-by-step-installation)
  - [Update System Packages](#step-1-update-system-packages)
  - [Install Required Tools](#step-2-install-required-tools)
  - [Install Node.js](#step-3-install-nodejs-lts)
  - [Clone the Repository](#step-4-clone-the-repository)
  - [Install Node Dependencies](#step-5-install-node-dependencies)
  - [Production Build](#step-6-generate-production-build)
  - [Install Nginx](#step-7-install-nginx)
  - [Copy Build to Nginx Directory](#step-8-copy-build-files-to-nginx-directory)
  - [Configure Nginx](#step-9-configure-nginx)
  - [Test and Restart Nginx](#step-10-test-and-restart-nginx)
  - [Verify Application](#step-11-verify-application-in-browser)
- [Troubleshooting](#8-troubleshooting)
- [Contact](#9-contact)
- [References](#10-references)

---

## 1. Purpose

Frontend Web is the main UI of the OT-Microservices stack. It is a **ReactJS** based application that provides a web interface for employee management. The application is cross-platform and only requires a JavaScript runtime (Node.js) to run. It serves as a single point of access for all microservices — Attendance, Employee, Salary, and Notification APIs.

---

## 2. System Requirements

| Hardware Specifications | Minimum Recommendation |
|------------------------|----------------------|
| Processor | Dual-core |
| RAM | 4 GB |
| Disk | 20 GB |
| OS | Ubuntu 22.04 |

---

## 3. Dependencies

### 3.1 Build Time Dependency

| Name | Version | Description |
|------|---------|-------------|
| Node.js | 18.x (LTS) | JavaScript runtime required to build the React application |
| npm | 9.x | Node package manager used to install all project dependencies |
| make | latest | Used to run predefined build commands from Makefile |
| git | latest | Required to clone the repository |
| curl | latest | Required to download Node.js setup script |

### 3.2 Run Time Dependency

| Name | Version | Description |
|------|---------|-------------|
| Node.js | 18.x (LTS) | Required to serve the application |
| Nginx | 1.24.x | Web server used to serve static React build files and act as reverse proxy |

### 3.3 Other Dependency

| Name | Version | Description |
|------|---------|-------------|
| Employee API | latest | Provides employee data consumed by the frontend |
| Attendance API | latest | Provides attendance data consumed by the frontend |
| Salary API | latest | Provides salary data consumed by the frontend |
| Notification API | latest | Provides notification data consumed by the frontend |

---

## 4. Important Ports

| Inbound Traffic | Description |
|----------------|-------------|
| 3000 | React development server default port |
| 80 | Nginx HTTP port for serving production build |

| Outbound Traffic | Description |
|-----------------|-------------|
| 8080 | Employee API |
| 8081 | Attendance API |
| 8082 | Salary API |
| 8083 | Notification API |

---

## 5. Architecture

# frontend

---

## 6. Dataflow Diagram

# dataflow

---

## 7. Step-by-step Installation

### Step 1: Update System Packages

```bash
sudo apt update && sudo apt upgrade -y
```

> **[Add Screenshot Here]**

---

### Step 2: Install Required Tools

```bash
sudo apt install curl git make -y
```

> **[Add Screenshot Here]**

---

### Step 3: Install Node.js (LTS)

```bash
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
```

> **[Add Screenshot Here]**

```bash
sudo apt install -y nodejs
```

> **[Add Screenshot Here]**

Verify installation:

```bash
node --version
npm --version
```

> **[Add Screenshot Here]**

---

### Step 4: Clone the Repository

```bash
git clone https://github.com/OT-MICROSERVICES/frontend.git
```

> **[Add Screenshot Here]**

```bash
cd frontend
ls -la
```

> **[Add Screenshot Here]**

---

### Step 5: Install Node Dependencies

```bash
npm install
```

> **[Add Screenshot Here]**

---

### Step 6: Generate Production Build

```bash
npm run build
```

> **[Add Screenshot Here — should show "Compiled successfully"]**

```bash
ls -la build/
```

> **[Add Screenshot Here]**

---

### Step 7: Install Nginx

```bash
sudo apt install nginx -y
```

> **[Add Screenshot Here]**

```bash
nginx -v
```

> **[Add Screenshot Here]**

---

### Step 8: Copy Build Files to Nginx Directory

```bash
sudo cp -r build/* /var/www/html/
```

> **[Add Screenshot Here]**

---

### Step 9: Configure Nginx

```bash
sudo nano /etc/nginx/sites-available/default
```
Replace existing content with:

```nginx
server {
    listen 80;
    server_name _;

    root /var/www/html;
    index index.html;

    location / {
        try_files $uri /index.html;
    }
}
```

> **[Add Screenshot Here]**

---

### Step 10: Test and Restart Nginx

```bash
sudo nginx -t
```

> **[Add Screenshot Here — should show "syntax is ok" and "test is successful"]**

```bash
sudo systemctl restart nginx
sudo systemctl enable nginx
sudo systemctl status nginx
```

> **[Add Screenshot Here — should show "active (running)"]**

---

### Step 11: Verify Application in Browser

Open the browser and go to:

```
http://<your-server-ip>
```

> **[Add Screenshot Here — Frontend UI loaded in browser]**

---

## Logs

| Log Type | Location | Description |
|----------|----------|-------------|
| Nginx Access Logs | `/var/log/nginx/access.log` | Records all incoming HTTP requests to the server |
| Nginx Error Logs | `/var/log/nginx/error.log` | Records server errors, warnings, and failed requests |

---

## 8. Troubleshooting

### Issue 1: Build Fails Due to Memory / OpenSSL Error

If `npm run build` fails with a JavaScript heap out of memory error or OpenSSL-related error, run:

```bash
export NODE_OPTIONS="--max-old-space-size=4096 --openssl-legacy-provider"
npm run build
```

> **[Add Screenshot Here — successful build after applying fix]**

This sets the Node.js max memory to 4 GB and enables legacy OpenSSL support needed by older React versions.

---

### Issue 2: Nginx Page Not Loading

| Possible Cause | Solution |
|----------------|----------|
| Nginx is not running | Run `sudo systemctl status nginx` and restart if needed |
| Wrong files in `/var/www/html` | Re-run `sudo cp -r build/* /var/www/html/` |
| Port 80 is blocked | Check firewall: `sudo ufw allow 80` |

---

### Issue 4: White/Blank Page After Deployment

| Possible Cause | Solution |
|----------------|----------|
| Build files not copied correctly | Run `ls /var/www/html` and verify `index.html` exists |
| Nginx `try_files` missing | Ensure Nginx config has `try_files $uri /index.html` |
| Wrong `root` path in Nginx | Confirm root is set to `/var/www/html` |

---

### Issue 5: Node.js or npm Version Mismatch

```bash
node --version    # Should be v18.x
npm --version     # Should be v9.x
```
#### If version is wrong, reinstall using the nodesource setup script from Step 3


---

## 9. Contact

| Name | Email Address |
| ------------- | ------------- |
| Sachin Rajput | [sachin.rajput.snaatak@mygurukulam.co](mailto:sachin.rajput.snaatak@mygurukulam.co) |

---

## 10. References

| Links | Description |
|-------|-------------|
| https://github.com/OT-MICROSERVICES/frontend | Official Frontend Source Repository |
| https://nodejs.org/en/download | Node.js Official Download |
| https://nginx.org/en/docs/ | Nginx Official Documentation |
| https://github.com/OT-MICROSERVICES/documentation-template/wiki/Application-Template | Application Documentation Template |
