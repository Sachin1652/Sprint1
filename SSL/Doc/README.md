
![image](https://github.com/user-attachments/assets/142cd82e-98f1-4861-b8e5-1e06c47ec7f0)


#  Secure Your Domain with HTTPS 
This proof-of-concept (POC) demonstrates how to secure your domain with HTTPS using a free SSL certificate.

## Document Details

| Author | Created | Version | Last Edited On | L0 Reviewer | L1 Reviewer | L2 Reviewer |
| --- | --- | --- | --- | --- | --- | --- |
| Your Name | 2026-04-23 | 1.0 | 2026-04-23 | Anitha Annem | Shreya Jaiswal | Ashwani Singh |



# Table of Contents

- [Prerequisites](#prerequisites)
- [Certbot Overview](#certbot-overview)
- [What Certbot Does](#what-certbot-does)
- [Steps to Set Up SSL](#steps-to-set-up-ssl)
- [POC Success Criteria](#poc-success-criteria)
- [Contact Information](#contact-information)
- [Reference](#reference)


# Goal

Secure your domain with HTTPS using a **free SSL certificate** 

# Before setting up refer this link 

[SSL Documentation](https://github.com/Cloud-NInja-snaatak/Documentation/blob/aniruddh_SCRUM-121/domain_security/ssl/ssl_document/README.md)



# Prerequisites

Before you begin, ensure you have the following:

| Requirement                             | Description                                      |
| --------------------------------------- | ------------------------------------------------ |
| **Registered Domain Name**              | A valid domain name (e.g., `example.com`)        |
| **Public Web Server**                   | Ubuntu/Debian-based server (preferred)           |
| **DNS A Record**                        | Points your domain (e.g., `example.com`) to your server's IP address |
| **Root (or sudo) Access**               | Full administrative privileges on the server     |
| **Nginx or Apache Installed**           | Either Nginx or Apache web server installed      |


# Certbot Overview

**Certbot** is a free, open-source tool that helps you obtain and renew **SSL/TLS certificates** from **Let's Encrypt**, a certificate authority that provides free certificates for securing websites with HTTPS.

# What Certbot Does

- Automatically obtains certificates from Let's Encrypt.
- Installs the certificate on your web server (e.g., Apache or Nginx).
- Automatically renews certificates before they expire.  
  > Let's Encrypt certificates are valid for 90 days.
- Supports domain validation via:
  - HTTP challenge
  - DNS challenge



# Steps to Set Up SSL (Detailed)

## 1. Install Certbot and the Nginx Plugin

```bash
sudo apt update
sudo apt install certbot python3-certbot-nginx -y
```

### 2. Allow HTTPS Through Firewall

```bash
sudo ufw allow 'Nginx Full'
```
### 3. Configure Nginx (Optional Manual Step)
Create a basic config for your domain if not already done:
```bash
server {
    listen 80;
    server_name cloudninja.com www.cloudninja.com;

    root /var/www/html;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```
Save it to /etc/nginx/sites-available/cloudninja.com

Enable the site:

```bash
sudo ln -s /etc/nginx/sites-available/cloudninja.com /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl reload nginx
```

### 4. Obtain SSL Certificate

Run the Certbot command with your domain name:

```bash
sudo certbot --nginx -d cloudninja.com -d www.cloudninja.com
```

Certbot will:

- Edit your Nginx config to redirect HTTP to HTTPS
- Obtain and install the certificate
- Set up automatic renewal


### 5. Verify SSL Installation

Open your domain in a browser:
👉 https://cloudninja.com — You should see the secure padlock icon.

### 5. Test Auto-Renewal

Certbot auto-renews certificates every 60 days. You can simulate a renewal with:

```bash
sudo certbot renew --dry-run
```

You should see a padlock icon and your custom HTML page.

![image](https://github.com/user-attachments/assets/0f308d5d-ec7d-455d-a9bb-346a84b27d2e)



# POC Success Criteria

| Criteria                         | Expected Result                         |
| --------------------------------- | --------------------------------------- |
| **HTTPS Loads Without Warning**   |  Padlock icon visible                 |
| **Certificate Issued by Let's Encrypt** |  Valid issuer and expiry             |
| **Auto-renewal Configured**       |  cron or systemd task verified       |


# Contact Information

| Name       | Email Address                |
|------------|------------------------------|
| Sachin Rajput | [sachin.rajput.snaatak@mygurukulam.co](mailto:sachin.rajput.snaatak@mygurukulam.co) |

# Reference

| Link                                                                 | Description                    |
|----------------------------------------------------------------------|--------------------------------|
| https://www.ssllabs.com/ssltest/       | Used as format reference       |


