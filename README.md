# Celebal-DevOps-Assignment-4
🐳 Docker Fundamentals Assignment
This repository contains step-by-step Docker tasks, commands, and resources to get started with containerization.

---

## 📚 Table of Contents

1. [Introduction & Basic Commands](#1-introduction--basic-commands)
2. [Dockerfile & Image Building](#2-dockerfile--image-building)
3. [Multi-Stage Build](#3-multi-stage-build)
4. [Custom Image from Container](#4-custom-image-from-container)
5. [Push/Pull to DockerHub](#5-pushpull-to-dockerhub)
6. [Docker Networking](#6-docker-networking)
7. [Docker Volumes](#7-docker-volumes)
8. [Docker Compose & Security](#8-docker-compose--security)

---

## ✅ 1. Introduction & Basic Commands

- Check Docker version: `docker --version`
- Run Hello World: `docker run hello-world`
- List containers: `docker ps`, `docker ps -a`
- List images: `docker images`
- Pull image: `docker pull ubuntu`

---

## ✅ 2. Dockerfile & Image Building

\`\`\`dockerfile
FROM ubuntu
RUN apt update && apt install -y curl
CMD ["curl", "https://example.com"]
\`\`\`

Commands:
\`\`\`bash
docker build -t my-ubuntu-curl .
docker run my-ubuntu-curl
\`\`\`

---

## ✅ 3. Multi-Stage Build

\`\`\`dockerfile
FROM golang:1.20 AS builder
WORKDIR /app
COPY . .
RUN go build -o app

FROM alpine
COPY --from=builder /app/app /app
CMD ["/app"]
\`\`\`

---

## ✅ 4. Custom Image from Container

\`\`\`bash
docker run -it ubuntu bash
# inside container
apt update && apt install -y git
exit
docker commit <container_id> ubuntu-with-git
\`\`\`

---

## ✅ 5. Push/Pull to DockerHub

\`\`\`bash
docker login
docker tag my-ubuntu-curl yourname/my-ubuntu-curl
docker push yourname/my-ubuntu-curl
docker pull yourname/my-ubuntu-curl
\`\`\`

---

## ✅ 6. Docker Networking

\`\`\`bash
docker network create my-bridge
docker run -dit --name c1 --network my-bridge ubuntu
docker run -dit --name c2 --network my-bridge ubuntu
docker exec -it c1 bash
ping c2
\`\`\`

---

## ✅ 7. Docker Volumes

\`\`\`bash
docker volume create my-volume
docker run -dit --name vtest -v my-volume:/data ubuntu
docker exec -it vtest bash
echo "hello docker" > /data/hello.txt
\`\`\`

---

## ✅ 8. Docker Compose & Security

### \`docker-compose.yml\`

\`\`\`yaml
version: '3'
services:
  web:
    image: nginx
    ports:
      - "8080:80"
  redis:
    image: redis
\`\`\`

Commands:
\`\`\`bash
docker-compose up -d
docker-compose ps
\`\`\`

---

## 🔐 Docker Security Best Practices

- Use minimal base images (e.g. Alpine)
- Set \`USER\` in Dockerfile
- Use \`.dockerignore\`
- Scan images: \`docker scan <image>\`

---

## 📘 Resources

- [Docker Curriculum](https://docker-curriculum.com/)
- [DockerHub](https://hub.docker.com/)
- YouTube tutorials included in task instructions
