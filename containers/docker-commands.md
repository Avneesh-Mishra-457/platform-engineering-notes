# Docker Commands — Hands-On Reference

## Core Commands
| Command | Purpose |
|---|---|
| `docker pull <image>` | Download image from registry |
| `docker run -d --name <n> -p host:container <image>` | Run detached with port mapping |
| `docker ps` | List running containers |
| `docker ps -a` | All containers including stopped |
| `docker logs <name>` | View container output |
| `docker logs -f <name>` | Follow logs live |
| `docker inspect <name>` | Full container details as JSON |
| `docker exec -it <name> /bin/bash` | Shell inside running container |
| `docker stop <name>` | Stop container |
| `docker rm <name>` | Remove container |
| `docker rm -f <name>` | Force remove running container |

## Port Mapping
`-p HOST_PORT:CONTAINER_PORT`
Traffic on HOST_PORT → forwarded to CONTAINER_PORT inside container.

## Key Flags
- `-d` detached (background)
- `-it` interactive + TTY (for shell access)
- `--name` give container a name
- `-p` port mapping

## Debugging Workflow
1. `docker logs <name>` — check app output first
2. `docker inspect <name>` — check network, IP, mounts
3. `docker exec -it <name> /bin/bash` — go inside if container is running

## Quick Revision (Flashcards)
Q: What is the difference between docker logs and docker exec?
A: logs = read-only output from app. exec = live shell inside running container

Q: What does docker run -d -p 9090:80 nginx mean?
A: Run nginx in background, host port 9090 maps to container port 80

Q: How do you see stopped containers?
A: docker ps -a

Q: Container crashed. What is your first command?
A: docker logs <name> to see why it crashed
