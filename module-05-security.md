# 5️⃣ Module 5 – Security Best Practices

### 🎯 Objective
Harden Docker images and containers, and scan for vulnerabilities.

---

## 🔒 5.1 Run as Non-Root

In your Dockerfile, create a user and drop root privileges:

```Dockerfile
FROM python:3.10-slim

RUN useradd -m appuser
WORKDIR /app
COPY . .

RUN pip install -r requirements.txt

USER appuser
CMD ["python", "app.py"]
```

---

## 🧯 5.2 Limit Capabilities & Use Read-Only FS

```bash
docker run -d       --name secure-api       --read-only       --cap-drop=ALL       --cap-add=NET_BIND_SERVICE       flaskapp:secure
```

---

## 🧪 5.3 Scan Images with Trivy

```bash
trivy image flaskapp:v1
```

Example output (truncated):

```
flaskapp:v1 (debian 11)
========================
Total: 5 (CRITICAL: 1, HIGH: 2, MEDIUM: 2)
```

Fix critical issues by upgrading base images and dependencies.

---

## 🛡️ 5.4 Docker Bench for Security

```bash
git clone https://github.com/docker/docker-bench-security.git
cd docker-bench-security
sudo ./docker-bench-security.sh
```

This tool audits your Docker host configuration.

---

## 📋 Summary

| Practice         | Example                               |
|------------------|----------------------------------------|
| Non-root user    | `USER appuser` in Dockerfile          |
| Drop capabilities| `--cap-drop=ALL`                      |
| Read-only FS     | `--read-only`                         |
| Image scanning   | `trivy image yourimage:tag`           |
| Host audit       | `docker-bench-security.sh`            |

---

▶️ **Next:** [`Module 6 – CI/CD Integration`](module-06-cicd-integration.md)
