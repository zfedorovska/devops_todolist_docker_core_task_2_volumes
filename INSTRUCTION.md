# Django Todolist – Docker Instructions

This document describes how to run the **MySQL database container** and the **Django Todolist app container**, and how to access the application in a browser.

## 1. Prerequisites

- Docker installed and running
- Access to Docker Hub

Optional: you can either **build images locally** or **pull them from Docker Hub**.

### Pull images from Docker Hub (optional)

```bash
docker pull zoryana/mysql-local:1.0.0
docker pull zoryana/todoapp:2.0.0

docker volume create mysql_data
docker run -d \
  --name mysql-local \
  -p 3306:3306 \
  -v mysql_data:/var/lib/mysql \
  zoryana/mysql-local:1.0.0

docker inspect -f "{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}" mysql-local

docker run -d \
  --name todoapp \
  -p 8000:8000 \
  -e DB_HOST=172.17.0.3 \
  zoryana/todoapp:2.0.0

http://localhost:8000



