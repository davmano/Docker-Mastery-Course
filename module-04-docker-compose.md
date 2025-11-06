# 4️⃣ Module 4 – Docker Compose

### 🎯 Objective
Use Docker Compose to define and run multi-container applications with a single YAML file.

---

## ⚙️ 4.1 What is Docker Compose?

Docker Compose lets you define services, networks, and volumes in a **`docker-compose.yml`** file and manage them together.

Start all services:

```bash
docker compose up -d
```

Stop and remove:

```bash
docker compose down
```

---

## 📄 4.2 Basic docker-compose.yml Example

```yaml
version: "3.9"

services:
  db:
    image: mysql:8
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: appdb
    volumes:
      - dbdata:/var/lib/mysql

  api:
    build: ./api
    environment:
      DB_HOST: db
      DB_NAME: appdb
    depends_on:
      - db

  web:
    build: ./web
    ports:
      - "8080:80"
    depends_on:
      - api

volumes:
  dbdata:
```

Bring up the stack:

```bash
docker compose up -d
docker compose ps
```

---

## 🧪 4.3 Lab – Add Healthchecks & Restart Policy

Extend `docker-compose.yml`:

```yaml
services:
  api:
    build: ./api
    restart: always
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:5000/health"]
      interval: 30s
      timeout: 5s
      retries: 3
```

View health status:

```bash
docker ps
```

(Look under the **STATUS** column for “(healthy)”).

---

## 📋 Summary

| Concept            | Command / File              | Description                        |
|--------------------|-----------------------------|------------------------------------|
| Start stack        | `docker compose up -d`      | Start all services                 |
| Stop/remove stack  | `docker compose down`       | Stop and clean up                  |
| View services      | `docker compose ps`         | List services in this project      |
| Logs               | `docker compose logs -f`    | Tail logs for all services         |
| Scale service      | `docker compose up --scale api=3 -d` | Scale a service            |

---

▶️ **Next:** [`Module 5 – Security Best Practices`](module-05-security.md)
