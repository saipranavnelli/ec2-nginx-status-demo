# 🚀 EC2 Nginx HTTP Status Code Demo

---

## 📌 Overview

This project demonstrates:

* Connecting to AWS EC2 using SSH
* Hosting a website using Nginx
* Understanding Nginx architecture
* Learning `sites-available` vs `sites-enabled`
* Testing HTTP status codes using curl, browser, and Postman

---

## 🧠 1. Architecture Overview

![Architecture](https://upload.wikimedia.org/wikipedia/commons/3/3f/Client-server-model.svg)

```
User (Browser)
     ↓
Internet
     ↓
EC2 Instance (Ubuntu)
     ↓
Nginx Web Server
     ↓
Website Files (HTML)
```

---

## 🔐 2. SSH Connection Flow

![SSH Flow](https://miro.medium.com/v2/resize\:fit:1200/1*ZVZ1vZk5v0zzakDx4zYdZg.png)

```
Your Laptop
   ↓ (SSH using .pem key)
Internet
   ↓
EC2 Instance (Ubuntu)
```

### ✅ Command

```bash
ssh -i "demo-keypair.pem" ubuntu@<EC2-PUBLIC-IP>
```

---

## ⚙️ 3. What is Nginx?

Nginx is a web server that:

* Receives requests from browser
* Serves HTML files
* Handles routing
* Acts as reverse proxy

---

## 🧠 4. Nginx Flow

![Nginx Architecture](https://www.nginx.com/wp-content/uploads/2019/03/NGINX-Architecture.png)

```
Browser → Nginx → HTML / API / Backend
```

---

## 📁 5. Nginx Folder Structure

```bash
/etc/nginx/
    ├── nginx.conf
    ├── sites-available/
    ├── sites-enabled/
```

---

## 🔑 6. sites-available vs sites-enabled

### 🧠 Concept

```
sites-available → configs stored
sites-enabled → configs active
```

### 🔗 Connection

```bash
sites-enabled/default → symlink → sites-available/default
```

👉 Only enabled configs are used by Nginx

---

## 🎯 7. Goal

Test HTTP status codes:

* 200 OK
* 302 Redirect
* 404 Not Found
* 500 Internal Server Error
* 502 Bad Gateway

---

## 🛠️ 8. Step-by-Step Setup

### Step 1: Connect to EC2

```bash
ssh -i "demo-keypair.pem" ubuntu@<EC2-PUBLIC-IP>
```

---

### Step 2: Install Nginx

```bash
sudo apt update
sudo apt install nginx -y
```

Check status:

```bash
sudo systemctl status nginx
```

---

### Step 3: Check Nginx folders

```bash
ls -l /etc/nginx/sites-available
ls -l /etc/nginx/sites-enabled
```

---

### Step 4: Backup default config

```bash
cd /etc/nginx/sites-available
sudo cp default default.bak
```

---

### Step 5: Edit Nginx config

```bash
sudo nano /etc/nginx/sites-available/default
```

Paste:

```nginx
server {
    listen 80;
    listen [::]:80;

    server_name _;

    root /var/www/html;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }

    location /login {
        return 302 /dashboard;
    }

    location /dashboard {
        return 200 "Welcome to dashboard\n";
    }

    location /server-error {
        return 500 "Internal Server Error\n";
    }

    location /api {
        proxy_pass http://127.0.0.1:9999;
    }
}
```

---

### Step 6: Enable config

```bash
sudo rm -f /etc/nginx/sites-enabled/default
sudo ln -s /etc/nginx/sites-available/default /etc/nginx/sites-enabled/default
```

---

### Step 7: Create website

```bash
sudo nano /var/www/html/index.html
```

Paste:

```html
<h1>EC2 Nginx HTTP Status Demo</h1>

<ul>
<li><a href="/dashboard">200 Success</a></li>
<li><a href="/login">302 Redirect</a></li>
<li><a href="/missingpage">404 Not Found</a></li>
<li><a href="/server-error">500 Internal Server Error</a></li>
<li><a href="/api">502 Bad Gateway</a></li>
</ul>
```

---

### Step 8: Test config

```bash
sudo nginx -t
```

---

### Step 9: Restart Nginx

```bash
sudo systemctl restart nginx
```

---

### Step 10: Verify port

```bash
sudo ss -tulnp | grep :80
```

---

### Step 11: Test locally

```bash
curl -I http://localhost
```

---

## 🧪 9. Testing HTTP Status Codes

```bash
curl -i http://localhost/dashboard
curl -i http://localhost/login
curl -i http://localhost/missingpage
curl -i http://localhost/server-error
curl -i http://localhost/api
```

---

## 🌐 10. Browser Testing

```
http://<EC2-IP>/
http://<EC2-IP>/dashboard
http://<EC2-IP>/login
http://<EC2-IP>/missingpage
http://<EC2-IP>/server-error
http://<EC2-IP>/api
```

---

## 📬 11. Postman Testing

Check:

* Status Code
* Headers
* Response Body

---

## 🔍 12. Browser Inspect

Steps:

1. Press F12
2. Go to Network tab
3. Open endpoints

Check:

* Status
* Headers
* Response

---

## 🧠 13. Meaning of Routes

| Route         | Meaning         |
| ------------- | --------------- |
| /dashboard    | 200 success     |
| /login        | 302 redirect    |
| /missingpage  | 404 not found   |
| /server-error | 500 error       |
| /api          | 502 bad gateway |

---

## 🔐 14. Security Group (AWS)

Allow:

* 22 → SSH
* 80 → HTTP
* 443 → HTTPS (optional)

---

## 🛠️ 15. Troubleshooting

```bash
sudo systemctl status nginx
sudo nginx -t
sudo systemctl restart nginx
sudo ss -tulnp | grep :80
```

---

## 🧠 16. GitHub Setup

```bash
git init
git add .
git commit -m "Initial commit"

git remote add origin https://github.com/<username>/ec2-nginx-status-demo.git
git branch -M main
git push -u origin main
```

---

## 🎯 17. Final Summary

```
Laptop → SSH → EC2 → Nginx → Website → Browser
```

---

## 💡 18. Learning Outcome

You learned:

* EC2 basics
* SSH connection
* Nginx setup
* Website hosting
* HTTP status codes
* Debugging using curl/Postman
* GitHub integration

---
