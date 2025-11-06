# AWS Ecom Demo (static Apache site)

Simple demo static website to practice deploying on AWS EC2 + ALB + Route53.
This repository contains a small static demo HTML site and a console-friendly
deployment script intended for use as EC2 user-data.

## Files
- `index.html` — Demo landing page (shows region and instance metadata).
- `css/style.css` — Basic styling.
- `assets/logo.png` — Placeholder logo (replace if you want).
- `deploy/install-apache-and-deploy.sh` — Script to install Apache, pull repo, and deploy.
- `deploy/healthcheck.sh` — Simple script that returns HTTP 200 for health checks (optional).

## How to use
### Option A — Automatic (recommended for EC2 user-data)
1. When launching an EC2 instance in the AWS Console, paste the contents of
   `deploy/install-apache-and-deploy.sh` into the **Advanced > User data** text box.
2. Modify `GIT_REPO` in the script to point to this repository's HTTPS clone URL:
   e.g. `https://github.com/<your-username>/aws-ecom-demo.git`.
3. Boot the instance. Apache will be installed and the site deployed automatically.
4. Visit `http://<instance-public-ip>/` to view the demo page.

### Option B — Manual deploy on an already running Ubuntu instance
```bash
sudo apt update -y
sudo apt install -y git apache2
git clone https://github.com/<your-username>/aws-ecom-demo.git /tmp/aws-ecom-demo
sudo cp -r /tmp/aws-ecom-demo/* /var/www/html/
sudo chown -R www-data:www-data /var/www/html
sudo systemctl enable --now apache2
