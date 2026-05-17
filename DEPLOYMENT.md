# Travel Memory Deployment Documentation

## Live Application URL

https://travelmemory.signalflyglobal.com

## Architecture

User
↓
Route53
↓
AWS Application Load Balancer
↓
Target Group
↓
EC2 Instance 1 + EC2 Instance 2
↓
Nginx Reverse Proxy
↓
React + NodeJS
↓
MongoDB Atlas

## Backend Deployment

- Cloned repository into EC2
- Configured MongoDB connection
- Configured environment variables
- Started Node.js using PM2

## Frontend Deployment

- Updated backend API URL
- Generated React production build
- Served frontend through Nginx

## Nginx Configuration

```nginx
server {
    listen 80;
    server_name _;

    root /var/www/TravelMemory/frontend/build;
    index index.html;

    location /api/ {
        proxy_pass http://127.0.0.1:3000/;
    }

    location / {
        try_files $uri /index.html;
    }
}
```

## Load Balancing

- Created Target Group
- Registered 2 EC2 instances
- Created Application Load Balancer
- Configured listener on port 80 and 443

## SSL Setup

- Requested ACM certificate
- Added validation CNAME in Route53
- Attached certificate to ALB
- Configured HTTP → HTTPS redirect
