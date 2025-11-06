# 6️⃣ Module 6 – CI/CD Integration

### 🎯 Objective
Integrate Docker into a CI/CD pipeline using GitHub Actions.

---

## 🧠 6.1 CI/CD Flow with Docker

Typical workflow:

1. Developer pushes code to GitHub.
2. GitHub Actions builds Docker image.
3. Tests run inside container.
4. Image is pushed to a registry.
5. Deployment system pulls and deploys image.

---

## ⚙️ 6.2 Sample GitHub Actions Workflow

File: `.github/workflows/docker-build.yml`

```yaml
name: Build and Push Docker Image

on:
  push:
    branches: ["main"]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v3

      - name: Login to Docker Hub
        uses: docker/login-action@v3
        with:
          username: ${{ secrets.DOCKERHUB_USERNAME }}
          password: ${{ secrets.DOCKERHUB_TOKEN }}

      - name: Build and push
        uses: docker/build-push-action@v5
        with:
          context: .
          push: true
          tags: |
            ${{ secrets.DOCKERHUB_USERNAME }}/flaskapp:latest
```

---

## 🧪 6.3 Lab – Add Test Step

Modify workflow to run tests before pushing:

```yaml
      - name: Run tests
        run: |
          docker build -t flaskapp:test .
          docker run --rm flaskapp:test pytest
```

If tests fail, the image won’t be pushed.

---

## 📋 Summary

| Step     | Tool          | Purpose                     |
|----------|---------------|-----------------------------|
| Build    | buildx        | Build image                 |
| Test     | pytest / etc. | Validate app in container   |
| Push     | Docker Hub    | Store image                 |
| Deploy   | GitHub Actions / others | Trigger deployment |

---

▶️ **Next:** [`Module 7 – Docker + Kubernetes`](module-07-docker-kubernetes.md)
