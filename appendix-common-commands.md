# 💡 Appendix – Common Docker Commands

Quick reference for frequently used Docker commands.

---

## 📦 Images

```bash
docker images                 # List images
docker pull nginx:latest      # Pull image
docker build -t name:tag .    # Build image from Dockerfile
docker rmi name:tag           # Remove image
```

---

## 📦 Containers

```bash
docker ps                     # Running containers
docker ps -a                  # All containers
docker run -d --name web nginx  # Run container in background
docker stop web               # Stop container
docker rm web                 # Remove container
docker logs -f web            # Follow logs
docker exec -it web /bin/sh   # Exec into container
```

---

## 🌐 Networks

```bash
docker network ls
docker network create app-net
docker network inspect app-net
```

---

## 💾 Volumes

```bash
docker volume ls
docker volume create data-vol
docker volume inspect data-vol
docker volume rm data-vol
```

---

## 🧹 Cleanup

```bash
docker container prune   # Remove stopped containers
docker image prune       # Remove dangling images
docker volume prune      # Remove unused volumes
docker system prune      # Remove unused data
```

---

## 📊 Monitoring

```bash
docker stats             # Live container metrics
docker system df         # Disk usage
```

---

Use this appendix as your quick cheat sheet while working through the modules.
