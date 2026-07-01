# 1. Docker — Full Guide

> 🟡 **Level:** Intermediate | ⭐ **Interview Frequency:** High

---

## 🧠 Concept

**Docker** packages your app + all its dependencies (Java, libraries, config) into a
**container** — a lightweight, isolated box that runs **the same** on any machine.

Solves the classic problem: *"It works on my machine but not on the server."*

---

## 💬 Simple Explanation

A container is like a **shipping container** 📦 — no matter which ship (computer) carries it,
the contents stay the same and work identically.

---

## 📋 Key Terms

| Term | Meaning |
|------|---------|
| **Image** | A blueprint (read-only template) of your app |
| **Container** | A running instance of an image |
| **Dockerfile** | Instructions to build an image |
| **Registry** | Store for images (Docker Hub, ECR) |
| **Volume** | Persistent storage outside the container |
| **Network** | Lets containers talk to each other |

```
Dockerfile → (build) → Image → (run) → Container
```

### Container vs Virtual Machine
| Container | Virtual Machine |
|-----------|-----------------|
| Shares host OS kernel | Full OS per VM |
| Lightweight (MBs) | Heavy (GBs) |
| Starts in seconds | Starts in minutes |

---

## 🧩 Dockerfile (for a Spring Boot app)

```dockerfile
# Use a base image with Java
FROM eclipse-temurin:17-jdk-alpine

# Set working directory inside container
WORKDIR /app

# Copy the built jar into the image
COPY target/myapp.jar app.jar

# Expose the port the app runs on
EXPOSE 8080

# Command to run when container starts
ENTRYPOINT ["java", "-jar", "app.jar"]
```

### Common Commands
```bash
docker build -t myapp .            # build image from Dockerfile
docker run -p 8080:8080 myapp      # run container, map ports
docker ps                          # list running containers
docker images                      # list images
docker stop <id>                   # stop a container
docker logs <id>                   # view logs
docker exec -it <id> sh            # open shell inside container
docker rmi <image>                 # remove image
```

---

## 🗂️ Volumes (persistent data)

Containers are **temporary** — data is lost when they stop. **Volumes** store data outside the
container so it survives restarts.
```bash
docker run -v mydata:/var/lib/mysql mysql
```

---

## 🌐 Networking
Containers can talk over a shared network by **name**.
```bash
docker network create mynet
docker run --network mynet --name db postgres
docker run --network mynet myapp   # can reach db by hostname "db"
```

---

## 🧱 Docker Compose (multiple containers)

Define and run **multi-container** apps with one file.
```yaml
# docker-compose.yml
version: "3.8"
services:
  app:
    build: .
    ports:
      - "8080:8080"
    depends_on:
      - db
  db:
    image: postgres:16
    environment:
      POSTGRES_PASSWORD: secret
    volumes:
      - pgdata:/var/lib/postgresql/data
volumes:
  pgdata:
```
```bash
docker compose up -d      # start everything
docker compose down       # stop everything
```

---

## 🌍 Real-World Use Case
Ship a Spring Boot app + Postgres + Redis together with Docker Compose. The same setup runs on
a developer laptop, CI pipeline, and production server — identically.

---

## ❓ Interview Questions
1. What is Docker? What problem does it solve?
2. Difference between image and container?
3. Container vs virtual machine?
4. What is a Dockerfile? Explain common instructions.
5. What are volumes? Why needed?
6. What is Docker Compose?
7. Difference between `CMD` and `ENTRYPOINT`?
8. How do containers communicate?
9. What is a multi-stage build? (Smaller final image by separating build & run stages)
10. How to reduce Docker image size?

---

## ✅ Best Practices
- Use small base images (alpine).
- Use **multi-stage builds** to keep images small.
- Use `.dockerignore` to exclude unneeded files.
- One process/service per container.
- Never hardcode secrets in images.

## ⚠️ Common Mistakes
- Storing data inside the container (lost on restart) — use volumes.
- Huge images from full JDK + unused files.
- Running containers as root.

---

## ⚡ Quick Revision Notes
- Docker = package app + deps into a container that runs anywhere.
- Image = blueprint; Container = running instance; Dockerfile = build recipe.
- Volumes = persistent storage; networks = container communication.
- Compose = run multi-container apps with one YAML.

## 🙋 FAQs
**Q: CMD vs ENTRYPOINT?** ENTRYPOINT sets the main command; CMD gives default arguments (can be overridden).

## 📎 References
- docs.docker.com

[⬅ Back to Docker Index](./README.md)

