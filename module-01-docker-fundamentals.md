# 1️⃣ Module 1 – Docker Fundamentals

### 🎯 Objective
Understand what Docker is, install it, and run your first containers on Linux.

---

## 🧠 1.1 Docker Architecture

```
+-------------------+
| Docker CLI Client |
+-------------------+
          |
          v
+---------------------------+
| Docker Daemon (dockerd)   |
|  - Builds images          |
|  - Runs containers        |
|  - Manages networks       |
|  - Handles volumes        |
+---------------------------+
          |
          v
+---------------------------+
| Docker Registry (Hub/ECR) |
|  - Stores container images|
+---------------------------+
```

**Key components:**
- **Client:** CLI you use (`docker` command).
- **Daemon:** Background service that does the work.
- **Registry:** Remote store for images (Docker Hub, ECR, GHCR…).

---

## ⚙️ 1.2 Installation (Ubuntu)

```bash
sudo apt update
sudo apt install -y ca-certificates curl gnupg lsb-release
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo       "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg]       https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"       | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

✅ **Verification:**

```bash
docker --version
```

Expected:

```
Docker version 27.0.1, build a33df3f
```

---

## 🧪 1.3 Running Your First Container

```bash
docker run hello-world
```

Output:

```
Hello from Docker!
This message shows that your installation appears to be working correctly.
```

Run a real web server:

```bash
docker run -d -p 8080:80 --name web nginx
docker ps
```

Example output:

```
CONTAINER ID   IMAGE   STATUS   PORTS                  NAMES
a9d2a8f9b2c5   nginx   Up 8s    0.0.0.0:8080->80/tcp   web
```

Access the app → open **http://localhost:8080**.

---

## 🧱 1.4 Hands-On Lab – Serve Custom HTML

**1️⃣ Create files**

```bash
mkdir mysite && cd mysite
echo "<h1>Hello Docker World</h1>" > index.html
```

**2️⃣ Create Dockerfile**

```Dockerfile
FROM nginx:alpine
COPY index.html /usr/share/nginx/html/
```

**3️⃣ Build image**

```bash
docker build -t mysite:v1 .
```

**4️⃣ Run container**

```bash
docker run -d -p 8080:80 mysite:v1
```

✅ Open browser → `http://localhost:8080`  
You should see: **Hello Docker World**

---

## 🧩 Summary

| Concept        | Command                         | Description                    |
|----------------|----------------------------------|--------------------------------|
| Run container  | `docker run`                    | Create a container             |
| List containers| `docker ps`                     | Show running containers        |
| Build image    | `docker build -t name .`        | Build image from Dockerfile    |
| View logs      | `docker logs <name>`            | View container logs            |
| Stop container | `docker stop <name>`            | Gracefully stop a container    |
| Remove         | `docker rm <name>` / `rmi`      | Delete containers / images     |

---

▶️ **Next:** [`Module 2 – Image Creation & Optimization`](module-02-image-optimization.md)
