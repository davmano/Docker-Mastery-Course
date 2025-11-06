# 2️⃣ Module 2 – Image Creation & Optimization

### 🎯 Objective
Write efficient Dockerfiles, understand image layers, and use multi-stage builds to reduce image size.

---

## 🧠 2.1 Image Layers

Each Dockerfile instruction creates a **layer**. Docker caches layers to speed up rebuilds.

```bash
docker history mysite:v1
```

Example output:

```
IMAGE          CREATED        CREATED BY                      SIZE
7ad3b5e23a1d   5 minutes ago  COPY index.html /usr/share...   1.5kB
<base>         ...            /bin/sh -c #(nop)  CMD ...      0B
```

---

## ⚙️ 2.2 Basic Dockerfile (Flask Example)

```Dockerfile
FROM python:3.10-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install -r requirements.txt

COPY . .

EXPOSE 5000
CMD ["python", "app.py"]
```

Build the image:

```bash
docker build -t flaskapp:v1 .
```

Example output:

```
Successfully built 87cd56f1234a
Successfully tagged flaskapp:v1
```

---

## ⚗️ 2.3 Multi-Stage Builds (Go Example)

```Dockerfile
# Stage 1: Build
FROM golang:1.21 AS builder
WORKDIR /src
COPY . .
RUN go build -o app .

# Stage 2: Runtime
FROM alpine:latest
COPY --from=builder /src/app /usr/local/bin/app
ENTRYPOINT ["app"]
```

Benefits:

- Only the **compiled binary** is in the final image.
- Smaller attack surface, faster pulls.

---

## 🧩 2.4 .dockerignore

Avoid sending unnecessary files into the build context.

Example `.dockerignore`:

```
.git
__pycache__
node_modules
*.log
.env
```

---

## 🧪 2.5 Lab – Optimize a Flask App Image

**1️⃣ Build unoptimized version**

```bash
docker build -t flaskapp:unoptimized .
```

**2️⃣ Apply optimization (example pattern)**

```Dockerfile
FROM python:3.10-slim AS base

FROM base AS builder
WORKDIR /app
COPY requirements.txt .
RUN pip install --user -r requirements.txt

FROM base
WORKDIR /app
COPY --from=builder /root/.local /root/.local
ENV PATH=/root/.local/bin:$PATH
COPY . .
CMD ["python", "app.py"]
```

**3️⃣ Compare image sizes**

```bash
docker images | grep flaskapp
```

Example expected output:

```
flaskapp   unoptimized   600MB
flaskapp   optimized     180MB
```

---

## 📋 Summary

| Technique          | Description                        | Example                            |
|--------------------|------------------------------------|------------------------------------|
| Layer caching      | Reuse unchanged build steps        | `RUN pip install`                  |
| Multi-stage builds | Separate build & runtime stages    | `FROM golang:1.21 AS builder`      |
| .dockerignore      | Exclude unused files from context  | `.git`, `node_modules`, `*.log`    |
| Image tags         | Version your images                | `flaskapp:v1`, `flaskapp:latest`   |

---

▶️ **Next:** [`Module 3 – Networking & Storage`](module-03-networking-storage.md)
