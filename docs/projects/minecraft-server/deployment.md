---
sidebar_position: 2
sidebar_label: Deployment
description: Deployment and verification of the Minecraft server on a cloud VM.
tags: [docker, minecraft, deployment, cloud]
---

# Minecraft Server – Deployment

## Prerequisites

- Linux-based cloud VM
- Docker and Docker Compose
- Git
- Accessible TCP port 8888

## Installation

Clone the project repository:

```bash
git clone https://github.com/tofa93/minecraft-server.git
cd minecraft-server
```

Create the environment configuration:

```bash
cp .env.example .env
```

Read the Minecraft EULA and set `EULA=true` if you agree.

Build and start the container:

```bash
docker compose up -d --build
```

## Server Access

Connect using Minecraft Java Edition:

```text
SERVER_IP:8888
```

Open the server console:

```bash
docker attach mc-server
```

Manage whitelist access:

```text
whitelist on
whitelist add PLAYER_NAME
```

Detach from the console using `Ctrl + P`, followed by `Ctrl + Q`.

## Verification

Check the container status and logs:

```bash
docker compose ps
docker compose logs -f mc-server
```

Alternatively, verify server availability using the provided Python script:

```bash
python -m pip install mcstatus
python test_server.py
```

## Persistence

The Minecraft world and server configuration are stored in a persistent Docker volume.

The container can be recreated without losing data:

```bash
docker compose down
docker compose up -d
```

Do not use `docker compose down -v` unless the persistent data should be deleted.

## Deployment Results

- [x] Successful deployment on a cloud VM
- [x] External access via TCP port 8888
- [x] Minecraft client connection
- [x] Python-based server status check
- [x] Persistent world and configuration data
- [x] Automatic restart after process failure

All technical project requirements were successfully verified.