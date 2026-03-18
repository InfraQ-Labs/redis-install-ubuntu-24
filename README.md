# Redis 8 Installation on Ubuntu 24

This repository provides a production-ready setup for installing Redis 8 from source on Ubuntu 24.

---

## 🚀 Quick Install (Automated)

Run the automated script:

```bash
chmod +x install-redis.sh
./install-redis.sh
```

---

## 📘 Detailed Guide (Recommended)

For step-by-step manual installation and explanation:

👉 [install-redis8-ubuntu24.md](./install-redis8-ubuntu24.md)

---

## 📂 Project Structure

- `install-redis.sh` → Fully automated installation script
- `install-redis8-ubuntu24.md` → Manual installation guide
- `README.md` → Quick start guide

---

## ⚠️ Security Note

By default, the script sets:

```
bind 0.0.0.0
```

This exposes Redis publicly.

Make sure to:
- Configure firewall (UFW / Security Groups)
- Set Redis password (`requirepass`)
- Restrict access to trusted IPs

---

## 📌 Default Paths

- Binary: `/usr/local/bin/redis-server`
- Config: `/etc/redis/redis.conf`
- Data: `/var/lib/redis`
- Service: `redis.service`
- Port: `6379`

---

## 📄 License

This project is licensed under the MIT License.
