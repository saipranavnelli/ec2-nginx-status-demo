# ec2-nginx-status-demo
Hosting a website on EC2 using Nginx and testing HTTP status codes

cat > README.md <<EOF
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
EOF
