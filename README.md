
# EC2 Nginx Status Demo

This project demonstrates hosting a website on AWS EC2 using Nginx.

## Features
- EC2 Ubuntu server
- Nginx web server
- HTTP status testing

## Endpoints
- /dashboard → 200
- /login → 302
- /missingpage → 404
- /server-error → 500
- /api → 502

# 🚀 EC2 Nginx HTTP Status Code Demo

This project demonstrates how to:

- Connect to an AWS EC2 instance using SSH
- Host a simple website using Nginx
- Understand Nginx architecture
- Learn sites-available vs sites-enabled
- Test HTTP status codes using curl, browser, and Postman

---

# 🧠 Architecture Overview

## 🌐 How User → Server Works

![Architecture](https://upload.wikimedia.org/wikipedia/commons/3/3f/Client-server-model.svg)

Flow:

User (Browser)
    ↓
Internet
    ↓
EC2 Instance (Ubuntu)
    ↓
Nginx Web Server
    ↓
Website Files (HTML)

---

# 🔐 SSH Connection Flow

## How you connect to EC2

![SSH Flow](https://miro.medium.com/v2/resize:fit:1200/1*ZVZ1vZk5v0zzakDx4zYdZg.png)

```text
Your Laptop
   ↓ (SSH using .pem key)
Internet
   ↓
EC2 Instance (Ubuntu)
