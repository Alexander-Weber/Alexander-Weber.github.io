---
title: Uptime Kuma
date: 2023-02-06 00:00:00 +0300
categories: [homelab, docker]
tags: [uptime-kuma,homelab,docker,installation]
---

Uptime Kuma is a self-hosted monitoring tool running in a [docker](https://www.docker.com/) container.
It is similar to "Uptime Robot".

## Installation

- Install [docker-compose](../docker-installation).
- Go to Uptime Kuma's [GitHub](https://github.com/louislam/uptime-kuma/)

#### Create a docker-compose.yaml 
```yaml
# Simple docker-compose.yaml
# You can change your port or volume location

version: '3'

services:
  uptime-kuma:
    image: louislam/uptime-kuma:1
    container_name: uptime-kuma
    volumes:
      - ./uptime-kuma-data:/app/data
    ports:
      - 3001:3001  # <Host Port>:<Container Port>
    restart: unless-stopped

  tunnel: 
    container_name: cloudflared-tunnel 
    image: cloudflare/cloudflared 
    restart: unless-stopped 
    command: tunnel run 
    environment: 
      - TUNNEL_TOKEN=mytokengoeshere

networks: 
  default: 
    external: 
      name: uptime-kuma

```

## How to Update

[Guide](https://github.com/louislam/uptime-kuma/wiki/%F0%9F%86%99-How-to-Update)

```bash
cd "<YOUR docker-compose.yml DIRECTORY>"
docker pull louislam/uptime-kuma:1
docker stop uptime-kuma
docker-compose up -d --force-recreate
```