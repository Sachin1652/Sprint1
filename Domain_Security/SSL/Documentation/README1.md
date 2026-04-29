# SSL (Secure Sockets Layer) Documentation

<img width="800" height="300" alt="image" src="https://github.com/user-attachments/assets/e021e5f7-215a-4877-b2c7-b97be3994e9a" />

---

## Author Details

| Author           | Created    | Version | Last updated by  | Last Edited On | L0 Reviewer       | L1 Reviewer | L2 Reviewer       |
|------------------|------------|---------|------------------|----------------|-------------------|-------------|-------------------|
| Bhawna Dangarh   | 2026-04-20 | 1.0     | Bhawna Dangarh   | 2026-04-25     | Tina Bhatnagar    | Aman Raj    | Abhishek Dubey    |

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [Why SSL is Required](#2-why-ssl-is-required)
3. [What is SSL](#3-what-is-ssl)
4. [How SSL Works](#4-how-ssl-works)
5. [How to Get an SSL Certificate](#5-how-to-get-an-ssl-certificate)
6. [Types of SSL Certificates](#6-types-of-ssl-certificates)
7. [SSL Providers](#7-ssl-providers)
8. [Detailed Comparison of SSL Providers](#8-detailed-comparison-of-ssl-providers)
9. [Recommendation](#9-recommendation)
10. [Contact Information](#10-contact-information)
11. [References](#11-references)

---

## 1. Introduction

This document explains the importance of SSL and how it helps secure communication over the internet.

SSL (Secure Sockets Layer) is a security protocol that establishes an encrypted connection between a user's browser and a web server. This ensures that any data exchanged remains private and protected from unauthorized access.

Websites using SSL can be easily identified by:

- **HTTPS** in the URL
- A **lock icon** in the browser

---

## 2. Why SSL is Required

SSL plays a critical role in ensuring data security and building user trust. It helps to:

- Protect sensitive information such as passwords and personal data
- Prevent hacking, data theft, and unauthorized access
- Build trust and credibility with users
- Meet security requirements for login and payment systems
- Improve website ranking on search engines

---

## 3. What is SSL

SSL is a digital certificate that serves two main purposes:

- It verifies the identity of a website
- It encrypts the data exchanged between the browser and the server

This ensures that users are communicating with the correct server and that their data remains secure.

---

## 4. How SSL Works

SSL works through a process known as the **SSL handshake**, which establishes a secure connection between the browser and the server.

The process includes the following steps:

- A user attempts to access a website
- The browser requests the server's SSL certificate
- The certificate is verified by a trusted Certificate Authority (CA)
- A secure, encrypted connection is established
- Data is transmitted safely between the browser and the server

---

## 5. How to Get an SSL Certificate

To obtain an SSL certificate, follow these steps:

### Step 1: Choose an SSL Provider
Select a trusted Certificate Authority (CA) such as Let's Encrypt or DigiCert.

### Step 2: Generate CSR
Create a Certificate Signing Request (CSR) on your server.
This includes details like your domain name and organization.

### Step 3: Verify Domain Ownership
Complete the verification process using methods such as:

- Email verification
- Uploading a verification file to the server

### Step 4: Install the Certificate
Install the issued SSL certificate on your web server to enable secure communication.

---

## 6. Types of SSL Certificates

### 1. Domain Validation (DV)
- Verifies only domain ownership
- Provides basic security
- Usually free or low cost

### 2. Organization Validation (OV)
- Verifies business identity
- Offers a moderate level of security

### 3. Extended Validation (EV)
- Requires full business verification
- Provides the highest level of trust and security

---

## 7. SSL Providers

Some commonly used SSL providers include:

| Provider       | Cost  | Best Use |
|---------------|------|----------|
| Let's Encrypt | Free | Small or personal websites |
| DigiCert      | Paid | Enterprise-level applications |
| GlobalSign    | Paid | Business websites |

---

## 8. Detailed Comparison of SSL Providers

| Feature | Let's Encrypt | DigiCert | GlobalSign |
|--------|---------------|----------|------------|
| Cost | Free | High | Medium |
| Certificate Types | DV | DV, OV, EV | DV, OV, EV |
| Validity Period | 90 Days | 1 Year | 1 Year |
| Automation Support | Fully automated | Limited | Limited |

---

## 9. Recommendation

| Use Case | Recommended Provider |
|----------|---------------------|
| Small or test websites | Let's Encrypt |
| Business websites | GlobalSign |
| Enterprise or financial systems | DigiCert |

---

## 10. Contact Information

| Name | Email Id |
|------|----------|
| Bhawna Dangarh | bhawna.dangarh.snaatak@mygurukulam.co |

---

## 11. References

| Reference | Description |
|-----------|-------------|
| https://www.cloudflare.com/learning/ssl/what-is-ssl/ | Overview of SSL concepts |
| https://letsencrypt.org/docs/ | Official documentation for Let's Encrypt |

---
