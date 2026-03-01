# Docker Commands Reference

Basic and most commonly used Docker management commands, grouped logically for quick reference.

> **Note:** Works the same on Linux / macOS / Windows unless mentioned

## 🔹 Docker Info & Version

```bash
docker --version
docker version
docker info
```

## 🔹 Docker Service (Linux)

```bash
sudo systemctl start docker
sudo systemctl stop docker
sudo systemctl restart docker
sudo systemctl status docker
```

## 🔹 Images Management

```bash
docker images                    # List images
docker pull <image>:<tag>        # Download image
docker rmi <image_id>            # Remove image
docker image prune               # Remove unused images
```

**Example:**
```bash
docker pull mongo:7
```

## 🔹 Containers Management

```bash
docker ps                        # Running containers
docker ps -a                     # All containers
docker run <image>               # Run container
docker start <container_id>
docker stop <container_id>
docker restart <container_id>
docker rm <container_id>         # Remove container
docker container prune           # Remove stopped containers
```

**Example:**
```bash
docker run -d --name mymongo mongo:7
```

## 🔹 Run Container (Most Used Options)

```bash
docker run -d \
  --name mycontainer \
  -p 27017:27017 \
  -e ENV=value \
  -v /host/path:/container/path \
  image_name
```

## 🔹 Logs & Monitoring

```bash
docker logs <container_id>
docker logs -f <container_id>     # Follow logs
docker stats                      # Resource usage
docker top <container_id>         # Processes inside container
```

## 🔹 Exec into Container (Shell Access)

```bash
docker exec -it <container_id> bash
docker exec -it <container_id> sh
```

**Example:**
```bash
docker exec -it mymongo bash
```

## 🔹 Docker Networks

```bash
docker network ls
docker network inspect <network>
docker network create <network_name>
docker network rm <network_name>
```

## 🔹 Docker Volumes

```bash
docker volume ls
docker volume create <volume_name>
docker volume inspect <volume_name>
docker volume rm <volume_name>
docker volume prune
```

## 🔹 Build & Push Images

```bash
docker build -t myimage:1.0 .
docker tag myimage:1.0 myrepo/myimage:1.0
docker push myrepo/myimage:1.0
```

## 🔹 Cleanup (Very Useful)

```bash
docker system df                 # Disk usage
docker system prune              # Remove unused everything
docker system prune -a           # Aggressive cleanup
```

## 🔹 Docker Compose (Basic)

```bash
docker compose up -d
docker compose down
docker compose ps
docker compose logs -f
```

## ✅ Recommended Daily Commands

```bash
docker ps
docker logs -f <container>
docker exec -it <container> bash
docker system prune
```

---

## Additional Resources

If you need, I can also provide:
- Docker commands specifically for MongoDB
- Production-safe Docker checklist
- Docker + AWS EC2 best practices
- Docker commands cheat-sheet PDF

