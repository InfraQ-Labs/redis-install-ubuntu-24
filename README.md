# Install Redis 8 on Ubuntu 24.04 (Complete Step-by-Step Guide)

A production-ready guide to install **Redis 8 on Ubuntu 24.04** using both automated script and manual setup. Includes systemd configuration, persistence setup, and security best practices.

---

## 🔑 Keywords

Redis 8 Ubuntu 24 install, install Redis Ubuntu 24.04, Redis setup Linux, Redis systemd Ubuntu, Redis production setup, Redis install script Ubuntu

---

## 🚀 Quick Install (1 Command)

Run the automated installation script:

```bash
chmod +x install-redis.sh
./install-redis.sh
```

✔ Installs Redis 8 from source  
✔ Configures systemd service  
✔ Applies production-ready settings  
✔ Starts Redis automatically  

---

## 📘 Manual Installation Guide (Detailed)

For full step-by-step explanation:

👉 [Install Redis 8 on Ubuntu 24 Guide](./install-redis8-ubuntu24.md)

---

## 📂 Project Structure

```
.
├── install-redis.sh                # Fully automated installation script
├── install-redis8-ubuntu24.md     # Manual installation guide
└── README.md                      # Quick start + overview
```

---

## ⚙️ Features

- ✅ Install latest Redis (8.x) from source
- ✅ systemd service integration
- ✅ Persistent storage (AOF + RDB)
- ✅ Optimized for production environments
- ✅ Minimal and clean configuration
- ✅ DevOps-friendly automation

---

## 🔒 Security Best Practices

⚠️ By default, the configuration may expose Redis publicly:

```conf
bind 0.0.0.0
```

### Recommended Actions:

- Restrict access using firewall (UFW / AWS Security Groups)
- Enable authentication:
  ```conf
  requirepass StrongPasswordHere
  ```
- Allow only trusted IPs
- Avoid exposing Redis directly to the internet

---

## ⚡ Default Configuration Paths

- **Redis Binary:** `/usr/local/bin/redis-server`
- **Config File:** `/etc/redis/redis.conf`
- **Data Directory:** `/var/lib/redis`
- **Service Name:** `redis.service`
- **Default Port:** `6379`

---

## 🧪 Verify Installation

Check Redis status:

```bash
sudo systemctl status redis
```

Test connection:

```bash
redis-cli ping
```

Expected output:

```
PONG
```

---

## 🧠 Why This Guide?

Unlike generic tutorials, this repository provides:

- Real-world production configuration
- Automation + manual flexibility
- Clean systemd integration
- Security-focused setup
- Ubuntu 24.04 specific instructions

---

## 📈 SEO Tip (For Contributors)

If you found this useful, consider sharing:

- Dev.to
- Medium
- LinkedIn
- Reddit (r/devops, r/linux)

This helps improve visibility and ranking 🚀

---

## 📄 License

This project is licensed under the MIT License.
