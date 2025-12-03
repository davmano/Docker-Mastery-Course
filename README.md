# 🐳 Docker Mastery for DevOps Engineers (Linux Edition)
**Author:** David Mano – *DevOps Engineer*  
**Edition:** Linux (Ubuntu) | **Visual Style:** Dark Terminal  

---

## ⚡ Quick Start (Local in VS Code)

```bash
# 1. Unzip this folder
cd docker-mastery-course

# 2. Open in VS Code
code .

# 3. Start with the main README
# Then follow modules in order: 01 → 09
```

---

## 🎯 Course Overview

This course is designed to give you **senior-level Docker skills** as a DevOps engineer.

You will:

- 🧱 Build and optimize Docker images using best practices  
- 🌐 Configure Docker networking and persistent storage  
- ⚙️ Use Docker Compose for multi-service applications  
- 🔒 Harden containers and scan for vulnerabilities  
- 🧩 Integrate Docker into CI/CD pipelines (GitHub Actions example)  
- ☸️ Deploy Dockerized apps to Kubernetes clusters  
- ⚡ Monitor, troubleshoot, and optimize containerized workloads  
- 🚀 Complete a capstone project that ties everything together  

---

## 🧠 Prerequisites

- Comfortable with **Linux (Ubuntu) terminal usage**
- Basic **Git** knowledge
- Familiar with basic **cloud / DevOps concepts**
- Installed locally:
  - `docker`
  - `docker compose`
  - `git`
  - `kubectl` (for Kubernetes module)
  - `trivy` (for image scanning, optional but recommended)

---

## 📑 Table of Contents

| # | File | Title |
|:-:|:-----|:------|
| 1️⃣ | [`module-01-docker-fundamentals.md`](module-01-docker-fundamentals.md) | Docker Fundamentals |
| 2️⃣ | [`module-02-image-optimization.md`](module-02-image-optimization.md) | Image Creation & Optimization |
| 3️⃣ | [`module-03-networking-storage.md`](module-03-networking-storage.md) | Networking & Storage |
| 4️⃣ | [`module-04-docker-compose.md`](module-04-docker-compose.md) | Docker Compose |
| 5️⃣ | [`module-05-security.md`](module-05-security.md) | Security Best Practices |
| 6️⃣ | [`module-06-cicd-integration.md`](module-06-cicd-integration.md) | CI/CD Integration |
| 7️⃣ | [`module-07-docker-kubernetes.md`](module-07-docker-kubernetes.md) | Docker + Kubernetes |
| 8️⃣ | [`module-08-advanced-topics.md`](module-08-advanced-topics.md) | Advanced Topics |
| 9️⃣ | [`module-09-capstone-project.md`](module-09-capstone-project.md) | Capstone Project |
| 💡 | [`appendix-common-commands.md`](appendix-common-commands.md) | Common Docker Commands |

---

## ⚙️ Environment Setup (Ubuntu Example)

```bash
sudo apt update
sudo apt install -y ca-certificates curl gnupg lsb-release git

# Add Docker’s official GPG key and repo
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo       "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg]       https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"       | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

sudo systemctl enable docker
sudo systemctl start docker

docker --version
```

Expected:

```
Docker version 27.0.1, build a33df3f
```

---

## 🧾 License

This course material is © 2025 **David Mano**.  
Free for personal and educational use with attribution.  
You may add an MIT `LICENSE` file later if you want to open-source it.
