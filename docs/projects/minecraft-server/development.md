---
sidebar_position: 1
sidebar_label: Development
description: Development of a custom Dockerized Minecraft server.
tags: [docker, minecraft, java, devsecops]
---

# Minecraft Server – Development

## Project Overview

The goal of this project was to develop a custom Docker image for a Minecraft Java Edition server without using a prebuilt Minecraft image.

[GitHub Repository](https://github.com/tofa93/minecraft-server)

## Technologies

- Docker and Docker Compose
- Alpine Linux
- Eclipse Temurin Java 25
- Minecraft Java Edition 26.3
- Shell scripting
- Python and mcstatus

## Implementation

### Docker Image

The custom image is based on `eclipse-temurin:25-jre-alpine`.

The Minecraft server binary is automatically downloaded from Mojang and verified using its SHA-1 checksum during the image build.

A dedicated non-root user is used to run the server.

### Entrypoint

The entrypoint script handles:

- EULA acceptance
- Default environment variables
- Initial server configuration
- Java memory configuration
- Minecraft server startup

Existing server configuration files are preserved.

### Docker Compose

Docker Compose manages the Minecraft server service and its configuration.

| Setting | Value |
|---|---|
| Service | `mc-server` |
| Host port | `8888` |
| Container port | `25565` |
| Storage | `mc-data` |
| Restart policy | `on-failure` |

An interactive console allows direct server administration.

## Testing

The following functionality was successfully tested locally:

- Docker image build
- Minecraft client connection
- Persistent world and configuration data
- Container recreation

## Security

- Non-root container user
- Server binary checksum verification
- Environment files excluded from Git
- Minecraft authentication enabled
- Whitelist-based access control

## Conclusion

The project demonstrates how to containerize an existing Java application, manage persistent data, and create a configurable and reproducible server environment.