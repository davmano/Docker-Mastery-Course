# 8️⃣ Module 8 – Advanced Topics

### 🎯 Objective
Learn registry management, performance tuning, and troubleshooting techniques.

---

## 📦 8.1 Working with Registries

Tag image:

```bash
docker tag flaskapp:v1 youruser/flaskapp:v1
```

Login & push:

```bash
docker login
docker push youruser/flaskapp:v1
```

---

## ⚡ 8.2 Resource Limits & Monitoring

Limit CPU and memory:

```bash
docker run -d --name limited-api       --cpus="1.0"       --memory="512m"       flaskapp:v1
```

Monitor usage:

```bash
docker stats
```

---

## 🧰 8.3 Debugging Containers

- View logs: `docker logs <name>`
- Exec into container: `docker exec -it <name> /bin/sh`
- Inspect container: `docker inspect <name>`

Example:

```bash
docker logs web
docker exec -it web /bin/sh
```

---

## 🧹 8.4 Cleanup & Disk Management

```bash
# Remove stopped containers
docker container prune

# Remove unused images
docker image prune

# Remove unused volumes
docker volume prune

# Show disk usage
docker system df
```

---

▶️ **Next:** [`Module 9 – Capstone Project`](module-09-capstone-project.md)
