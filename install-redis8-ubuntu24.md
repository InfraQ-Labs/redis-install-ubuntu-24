# Install Redis 8 on Ubuntu 24

> 🚀 This guide installs Redis 8 on Ubuntu 24 from source with systemd and production-ready configuration.

---

## 1. Install required build dependencies

Install required packages needed to compile Redis:

```bash
sudo apt update

sudo apt install -y \
build-essential \
tcl \
curl \
pkg-config \
libssl-dev \
git \
cmake \
clang \
automake \
autoconf \
libtool
```

---

## 2. Download and install Redis

Download Redis source and extract:

```bash
cd /usr/src
sudo wget https://github.com/redis/redis/archive/refs/tags/8.0.0.tar.gz
sudo tar -xzf 8.0.0.tar.gz
cd redis-8.0.0
```

**Compile and install Redis:**

```bash
make -j $(nproc)
sudo make install
```

**Verify installation:**

```bash
redis-server --version
redis-cli --version
```

---

## 3. Configure Redis

Create the Redis configuration directory and copy the default configuration file:

```bash
sudo mkdir /etc/redis
sudo cp /usr/src/redis-8.0.0/redis.conf /etc/redis
sudo nano /etc/redis/redis.conf
```

### 🔧 Required Configuration Changes

---

### 3.1 Enable systemd supervision

**Default:**
```conf
# supervised no
```

**Change to:**
```conf
supervised systemd
```

**Reason:**
- Ensures proper integration with systemd

---

### 3.2 Enable Append-Only File (AOF) persistence

**Default:**
```conf
appendonly no
```

**Change to:**
```conf
appendonly yes
```

**Reason:**
- Enables durable persistence using AOF logs

> ⚠️ **Important Warning**
>
> - Enabling `appendonly yes` on an existing database via config change + restart can lead to data loss  
> - Prefer enabling it during initial setup  
> - For existing databases, use:
>
> ```bash
> redis-cli CONFIG SET appendonly yes
> ```
>
> More info: https://redis.io/docs/latest/operate/oss_and_stack/management/persistence/

---

### 3.3 Configure working directory

**Default:**
```conf
dir ./
```

**Change to:**
```conf
dir /var/lib/redis
```

**Reason:**
- Ensures proper data storage location

---

### 3.4 Configure bind address

**Default:**
```conf
bind 127.0.0.1 ::1
```

**Recommended (secure, local-only):**
```conf
bind 127.0.0.1
```

**Optional (public access):**
```conf
bind 0.0.0.0
```

**Reason:**
- `127.0.0.1` → Local only (safe)
- `0.0.0.0` → External access (requires firewall + authentication)

> ⚠️ Exposing Redis publicly without security controls is dangerous.

---

### 3.5 Add snapshot (RDB) save rules

Add these lines if not already present:

```conf
save 900 1
save 300 10
save 60 10000
```

---

### 3.6 Verify port configuration

```conf
port 6379
```
**Reason:**
- Default Redis port. Change only if required.

---

### 3.7 Configure Redis password (authentication)

**Default:**
```conf
# requirepass foobared
```

**Change to:**
```conf
requirepass YourStrongPasswordHere
```

**Reason:**
- Prevents unauthorized access

> ⚠️ **Security Note**
>
> - Always set a strong password if Redis is exposed externally  
> - Use firewall rules (`ufw`)  
> - Never expose Redis publicly without authentication  

---

✔️ Save and exit the configuration file

---

## 4. Configure systemd service

Create a systemd service file for Redis.

```bash
sudo nano /etc/systemd/system/redis.service
```
Paste:

```ini
[Unit]
Description=Redis In-Memory Data Store
After=network.target

[Service]
User=redis
Group=redis
ExecStart=/usr/local/bin/redis-server /etc/redis/redis.conf
ExecStop=/usr/local/bin/redis-cli shutdown
Restart=always
RestartSec=3

[Install]
WantedBy=multi-user.target
```

---

## 5. Create Redis user and directories

```bash
sudo adduser --system --group --no-create-home redis
sudo mkdir /var/lib/redis
sudo chown redis:redis /var/lib/redis
sudo chmod 770 /var/lib/redis
```

---

## 6. Start Redis and enable on boot

Reload systemd and start the Redis service.

```bash
sudo systemctl daemon-reload
sudo systemctl start redis
sudo systemctl enable redis
```

---

## 7. Verify Redis installation

Check Redis service status.

```bash
sudo systemctl status redis
```

Test Redis connectivity.

```bash
redis-cli ping
```

Expected output:

```
PONG
```

---

## ✅ Notes

- **Redis binaries:** `/usr/local/bin/redis-server`  
- **Configuration file:** `/etc/redis/redis.conf`  
- **Data directory:** `/var/lib/redis`  
- **Systemd service name:** `redis.service`  
- **Default port:** `6379`  

---
