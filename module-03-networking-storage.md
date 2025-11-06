# 3️⃣ Module 3 – Networking & Storage

### 🎯 Objective
Understand how containers communicate and how to persist data using volumes.

---

## 🌐 3.1 Docker Networking Basics

Common network drivers:

- **bridge** (default): Containers get private IPs, communicate via virtual bridge.
- **host**: Container shares the host’s network namespace.
- **none**: No networking for the container.

List networks:

```bash
docker network ls
```

Example output:

```
NETWORK ID     NAME      DRIVER    SCOPE
7c1a6e3f73c2   bridge    bridge    local
9e8e6c4a16d1   host      host      local
1393a6f84745   none      null      local
```

---

## 🌐 3.2 Custom Bridge Networks

Create a custom network for app-to-db communication:

```bash
docker network create app-net
```

Run containers on the same network:

```bash
docker run -d --name db --network app-net mysql:8
docker run -d --name web --network app-net nginx
```

Test connectivity (from `web` to `db`):

```bash
docker exec -it web ping -c 2 db
```

Example output:

```
PING db (172.18.0.2): 56 data bytes
64 bytes from 172.18.0.2: seq=0 ttl=64 time=0.08 ms
```

---

## 💾 3.3 Volumes & Persistence

Docker volumes are managed storage areas for containers.

List volumes:

```bash
docker volume ls
```

Create volume:

```bash
docker volume create mysql_data
```

Use in container:

```bash
docker run -d       --name db       -e MYSQL_ROOT_PASSWORD=root       -v mysql_data:/var/lib/mysql       mysql:8
```

Inspect volume:

```bash
docker volume inspect mysql_data
```

---

## 🧪 3.4 Lab – 3-Tier App with Persistent DB

**Goal:** Nginx → Flask → MySQL, all on a custom network, DB with volume.

1️⃣ Create network and volume:

```bash
docker network create web-net
docker volume create webapp_db
```

2️⃣ Run MySQL:

```bash
docker run -d --name db       --network web-net       -e MYSQL_ROOT_PASSWORD=root       -e MYSQL_DATABASE=appdb       -v webapp_db:/var/lib/mysql       mysql:8
```

3️⃣ Run Flask app (image assumed built as `flaskapp:v1`):

```bash
docker run -d --name api       --network web-net       -e DB_HOST=db       -e DB_NAME=appdb       flaskapp:v1
```

4️⃣ Run Nginx as frontend:

```bash
docker run -d --name frontend       --network web-net       -p 8080:80       nginx
```

5️⃣ Verify:

```bash
docker ps
docker network inspect web-net
```

---

## 📋 Summary

| Concept        | Command                            | Description                         |
|----------------|-------------------------------------|-------------------------------------|
| List networks  | `docker network ls`                | Show existing networks              |
| Create network | `docker network create name`       | Custom bridge network               |
| List volumes   | `docker volume ls`                 | Show Docker volumes                 |
| Create volume  | `docker volume create name`        | Persistent storage                  |
| Use volume     | `-v name:/path/in/container`       | Mount into container                |

---

▶️ **Next:** [`Module 4 – Docker Compose`](module-04-docker-compose.md)
