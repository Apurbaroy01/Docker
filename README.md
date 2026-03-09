# Docker Commands Guide (A–Z) – Bangla

এই README ফাইলটি Docker এর গুরুত্বপূর্ণ কমান্ডগুলো ব্যাখ্যা সহ দেখানোর জন্য তৈরি করা হয়েছে।
Docker ব্যবহার করে **image তৈরি, container চালানো, stop করা, delete করা, deploy করা**—সবকিছু এখানে সংক্ষেপে দেওয়া আছে।

---

# 1. Docker Version

Docker ঠিকভাবে ইনস্টল হয়েছে কিনা দেখার জন্য।

```bash
docker --version
docker version
docker info
```

---

# 2. Docker Login / Logout

Docker Hub এ login করার জন্য।

```bash
docker login
docker logout
```

---

# 3. Docker Help

Docker এর সব কমান্ড দেখার জন্য।

```bash
docker help
docker run --help
```

---

# 4. Docker Image Commands

### সব image দেখার জন্য

```bash
docker images
```

### Docker Hub থেকে image নামিয়ে আনা

```bash
docker pull nginx
```

### image delete করা

```bash
docker rmi image_name
```

### সব image delete করা

```bash
docker rmi $(docker images -q)
```

### unused image delete করা

```bash
docker image prune -a
```

---

# 5. Docker Image Build

Dockerfile থেকে image তৈরি করা।

```bash
docker build -t image_name .
```

উদাহরণ:

```bash
docker build -t node_app .
```

ব্যাখ্যা

* `build` → Dockerfile থেকে image বানায়
* `-t` → image এর নাম দেয়
* `.` → current folder ব্যবহার করে build করে

---

# 6. Container Run

Container চালানোর জন্য।

```bash
docker run image_name
```

---

# 7. Port Mapping

লোকাল পোর্ট container এর সাথে যুক্ত করা।

```bash
docker run -p 5001:5001 image_name
```

ব্যাখ্যা

* প্রথম `5001` → আপনার কম্পিউটার
* দ্বিতীয় `5001` → container এর port

---

# 8. Container Name

container এর নাম দেওয়া।

```bash
docker run --name my_container image_name
```

---

# 9. Detached Mode

background এ container চালানো।

```bash
docker run -d image_name
```

---

# 10. Container List

চলমান container দেখার জন্য।

```bash
docker ps
```

সব container দেখার জন্য।

```bash
docker ps -a
```

---

# 11. Container Stop / Start

container বন্ধ করা।

```bash
docker stop container_name
```

container চালু করা।

```bash
docker start container_name
```

container restart।

```bash
docker restart container_name
```

---

# 12. Container Delete

একটা container delete করা।

```bash
docker rm container_name
```

সব container delete করা।

```bash
docker rm $(docker ps -aq)
```

---

# 13. Remove Stopped Containers

```bash
docker container prune
```

ব্যাখ্যা

বন্ধ হয়ে থাকা সব container delete করে।

---

# 14. Container Logs

container এর log দেখার জন্য।

```bash
docker logs container_name
```

live log দেখার জন্য।

```bash
docker logs -f container_name
```

---

# 15. Container এর ভিতরে Command চালানো

```bash
docker exec -it container_name bash
```

ব্যাখ্যা

container এর ভিতরে terminal খুলে দেয়।

---

# 16. Copy Files

Host → Container

```bash
docker cp file.txt container_name:/app
```

Container → Host

```bash
docker cp container_name:/app/file.txt .
```

---

# 17. Docker Volume

volume তৈরি করা।

```bash
docker volume create my_volume
```

সব volume দেখার জন্য।

```bash
docker volume ls
```

volume delete।

```bash
docker volume rm my_volume
```

---

# 18. Docker Network

সব network দেখার জন্য।

```bash
docker network ls
```

network তৈরি করা।

```bash
docker network create my_network
```

---

# 19. Docker System Cleanup

unused data delete।

```bash
docker system prune
```

সব unused delete।

```bash
docker system prune -a
```

disk usage দেখার জন্য।

```bash
docker system df
```

---

# 20. Docker Tag

image এর নতুন tag তৈরি করা।

```bash
docker tag node_app username/node_app:v1
```

---

# 21. Docker Push

Docker Hub এ image upload করা।

```bash
docker push username/node_app
```

---

# 22. Docker Compose

multiple container একসাথে চালানোর জন্য।

```bash
docker compose up
```

background এ চালানোর জন্য।

```bash
docker compose up -d
```

stop করার জন্য।

```bash
docker compose down
```

---

# 23. Development Setup (Node.js + Docker)

এই কমান্ড ব্যবহার করলে container এর ভিতরে **live code change detect হয়**।

```bash
docker run -p 5001:5001 --name node_c --rm \
-v ${PWD}:/app \
-v /app/node_modules \
node_app
```

### ব্যাখ্যা

`-p 5001:5001`
লোকাল 5001 port → container 5001 port।

`--name node_c`
container এর নাম।

`--rm`
container stop হলে automatic delete হবে।

`-v ${PWD}:/app`
লোকাল project folder container এর `/app` এ mount করে।

`-v /app/node_modules`
node_modules container এর ভিতরে আলাদা রাখে।

`node_app`
Docker image এর নাম।

---

# 24. Danger Cleanup Command

সব container, image, network, volume delete।

```bash
docker rm -f $(docker ps -aq)
docker rmi -f $(docker images -q)
docker volume prune
docker network prune
```

সতর্কতা: এগুলো চালালে সব Docker data delete হয়ে যাবে।

---

# Basic Docker Workflow

```
Project
   ↓
Dockerfile তৈরি
   ↓
docker build
   ↓
docker run
   ↓
docker push (optional)
   ↓
VPS / Cloud deploy
```

---

# Summary (Most Used Commands)

```
docker build
docker run
docker ps
docker stop
docker rm
docker images
docker rmi
docker logs
docker exec
docker compose up
docker system prune
```

---
