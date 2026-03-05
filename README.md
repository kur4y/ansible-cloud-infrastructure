# Ansible Cloud Infrastructure

> "There is no cloud, it's just someone else's computer."

## 📜 About
This repository contains an Infrastructure as Code (IaC) project that automates the deployment of a secure, multi-container web architecture on a remote cloud instance (AWS EC2). It provisions a WordPress site, MariaDB, and phpMyAdmin, orchestrated behind an Nginx reverse proxy secured with Let's Encrypt TLS certificates.

## 🏗️ Architecture & Technologies
Each process runs in its own dedicated and isolated container, complying with strict deployment standards.
* **Provisioning & Automation:** Ansibleaa
* **Orchestration:** Docker Compose
* **Reverse Proxy:** Nginx (Alpine)
* **Application:** WordPress (PHP-FPM)
* **Database:** MariaDB
* **Database Management:** phpMyAdmin
* **Security:** Let's Encrypt (Certbot / TLSv1.3)

## ⚙️ Prerequisites
To run this deployment, your control node (local machine) needs:
* `ansible` installed.
* An SSH key configured and pushed to your remote cloud instance.
* A valid `.env` file containing the necessary secrets (database credentials, domain name, WordPress admin details).
* An `inventory.ini` file pointing to your remote server IP.
* A registered domain name pointing to your server's public IP (e.g., DuckDNS).

## 🚀 Usage

1. Clone the repository.
2. Ensure your `.env` and `inventory.ini` are properly configured (do not push these to public repositories).
3. Run the Ansible playbook:

\`\`\`bash
ansible-playbook -i inventory.ini playbook.yml
\`\`\`

The script will automatically:
- Configure server memory swap.
- Install Docker and Docker Compose.
- Secure a Let's Encrypt SSL/TLS certificate via standalone challenge.
- Deploy the Docker network, volumes, and containers.
- Wait for database initialization.
- Download WP-CLI and fully configure the WordPress site silently.