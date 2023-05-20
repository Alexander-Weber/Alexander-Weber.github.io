---
title: Docker Installation
date: 2023-02-06 00:00:00 +0300
categories: [homelab, docker]
tags: [homelab,docker,installation]
---

Docker is an open-source platform that allows you to automate the deployment, scaling, and management of applications by packaging them into lightweight, portable containers.

## How to install docker and docker-compose on Linux:

Update apt:
```bash
sudo apt update && upgrade -y
```

____________________________________________

### Only Docker

Install docker.io: 
```bash
sudo apt install docker.io -y
```

Test docker:
```bash 
sudo docker run --name web -itd -p 8080:80 nginx
```

____________________________________________

### Alternative

Install docker.io with docker-compose:
```bash
sudo apt install docker.io docker-compose -y
```

### Test docker-compose

Create a folder:
```bash
mkdir docker-test && cd docker-test
```

Create and edit a docker-compose.yaml file:
```bash
nano docker-compose.yaml
```

Add this to the yaml file:
```yaml
version: "3"
services:
  website:
    image: nginx
    ports:
      - "8081:80"
    restart: always
```

Run docker compose from folder:
```bash
sudo docker-compose up -d
```

____________________________________________

Check if docker container is running:
```bash
sudo docker ps
```

Or for only docker compose containers:
```bash
sudo docker-compose ps
```

