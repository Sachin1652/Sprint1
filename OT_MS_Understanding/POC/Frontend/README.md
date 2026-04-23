<h1 align="center">Frontend API </h1>

<p align="center">
  <img 
    src="https://raw.githubusercontent.com/OT-MICROSERVICES/frontend/0515d20bc9a18ab0df520e9b6aad04a2794ef448/static/frontend-logo.svg" 
    width="350"
  />
</p>

## Document Details

| Author | Created | Version | Last Edited On | L0 Reviewer | L1 Reviewer | L2 Reviewer |
| -------------- | ---------- | ------- | -------------- | ----------- | ----------- | ----------- |
| Sachin Rajput | 2026-04-22 | 1.0 | 2026-04-22 | Anitha Annem | Shreya Jaiswal | Ashwani Singh |


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
| Node.js | 18.20.8 (LTS) | JavaScript runtime required to build the React application |
| npm | 10.8.2 | Node package manager used to install all project dependencies |
| make | latest | Used to run predefined build commands from Makefile |
| git | latest | Required to clone the repository |
| curl | latest | Required to download Node.js setup script |

### 3.2 Run Time Dependency

| Name | Version | Description |
|------|---------|-------------|
| Node.js | 18.20.8 (LTS) | Required to serve the application |
| Nginx | 1.24.0 | Web server used to serve static React build files and act as reverse proxy |

### 3.3 Other Dependency

| Name | POC Link | Description |
|------|---------|-------------|
| Employee API | [Employee](https://github.com/Snaatak-Cloud-Cartel/Documentations/blob/0632547adb40c2b027178f1ad23c7e82a87f1e6b/OT_MS_Understanding/POC/Employee/README.md)  | Provides employee data consumed by the frontend |
| Attendance API | [Attendance](https://github.com/Snaatak-Cloud-Cartel/Documentations/blob/f52749d8323cc6a179e65af14cc5ae13f2c4801a/OT_MS_Understanding/POC/Attendance/README.md) | Provides attendance data consumed by the frontend |
| Salary API | [Salary]() | Provides salary data consumed by the frontend |
| Notification API | [Notification]() | Provides notification data consumed by the frontend |

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

<img width="2912" height="1156" alt="frontend" src="https://github.com/user-attachments/assets/a19bfe10-620f-45ce-a700-141bb4cc7232" />

---

## 6. Dataflow Diagram

<img width="1536" height="1024" alt="Dataflow" src="https://github.com/user-attachments/assets/257941c9-728a-4eb9-ba65-4f7ef312969f" />

---

## 7. Step-by-step Installation

### Step 1: Update System Packages

```bash
sudo apt update && sudo apt upgrade -y
```
<img width="1919" height="957" alt="image" src="https://github.com/user-attachments/assets/2a96b28f-a204-4de2-86dd-5795ab8bebd4" />


---

### Step 2: Install Required Tools

```bash
sudo apt install curl git make -y
```
<img width="1919" height="951" alt="image" src="https://github.com/user-attachments/assets/310ca451-fc93-4593-9093-b09a8b2b0001" />

---

### Step 3: Install Node.js (LTS)

```bash
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
```
<img width="1919" height="753" alt="image" src="https://github.com/user-attachments/assets/88c5d7f4-971d-48e7-8dd8-fb868d52f88c" />
<img width="1919" height="330" alt="image" src="https://github.com/user-attachments/assets/e238cfaa-bd06-48d5-877a-fea5cb9efd9b" />



```bash
sudo apt install -y nodejs
```
<img width="1919" height="949" alt="image" src="https://github.com/user-attachments/assets/70aadc6b-298d-4d21-bd88-1d2324bcd2bc" />


Verify installation:

```bash
node --version
npm --version
```
<img width="1919" height="94" alt="image" src="https://github.com/user-attachments/assets/4fd805fb-d3f7-4d06-a64d-ff8cd714bba9" />

---

### Step 4: Clone the Repository

```bash
git clone https://github.com/OT-MICROSERVICES/frontend.git
```
<img width="1919" height="183" alt="image" src="https://github.com/user-attachments/assets/6133f09d-6e1d-4772-abfd-85a63aa660a4" />


```bash
cd frontend
ls -la
```
<img width="1919" height="334" alt="image" src="https://github.com/user-attachments/assets/7eefe481-29c6-4918-8092-68f32b2cc381" />


---

### Step 5: Install Node Dependencies

```bash
make install
```

<img width="1919" height="466" alt="image" src="https://github.com/user-attachments/assets/75900a56-bdd5-48e2-a12d-2f287aa60e38" />


---

### Step 6: Generate Production Build

```bash
npm run build
```

<img width="1919" height="488" alt="image" src="https://github.com/user-attachments/assets/23e37ba3-8af1-4f47-a7a6-7beca98e8a59" />
<img width="1919" height="528" alt="image" src="https://github.com/user-attachments/assets/9bcbf12a-ac4a-4ff2-bc69-4e65da983e45" />


```bash
ls -la build/
```
<img width="1919" height="203" alt="image" src="https://github.com/user-attachments/assets/bf01a900-aafd-40e4-a226-45c2de371505" />


---

### Step 7: Install Nginx

```bash
sudo apt install nginx -y
```

<img width="1919" height="928" alt="image" src="https://github.com/user-attachments/assets/bd753717-c081-44a5-9f19-12528c1440dc" />


```bash
nginx -v
```
<img width="1919" height="48" alt="image" src="https://github.com/user-attachments/assets/1933ec36-9fed-4b31-93db-8bf5b17cc7ef" />


---

### Step 8: Copy Build Files to Nginx Directory

```bash
sudo cp -r build/* /var/www/html/
```
<img width="1919" height="68" alt="image" src="https://github.com/user-attachments/assets/4b0481a8-0b62-4a8b-a4a4-ade34c02543d" />


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
---

### Step 10: Test and Restart Nginx

```bash
sudo nginx -t
```
<img width="1919" height="91" alt="image" src="https://github.com/user-attachments/assets/46cfa3f7-6a6e-4c75-9473-5e8b406a725d" />


```bash
sudo systemctl restart nginx
sudo systemctl enable nginx
sudo systemctl status nginx
```
<img width="1919" height="403" alt="image" src="https://github.com/user-attachments/assets/0f9352f6-bab6-42b1-bfa3-2f04ee118d92" />


---

### Step 11: Verify Application in Browser

Open the browser and go to:

```
http://<your-server-ip>
```
<img width="1919" height="1011" alt="Screenshot from 2026-04-21 20-27-37" src="https://github.com/user-attachments/assets/8b864bd2-bc43-4d3e-a013-4c8a3b4cbdae" />


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
node --version    # Should be v18.20.8
npm --version     # Should be v10.8.2
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
