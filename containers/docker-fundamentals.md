# Docker Fundamentals

## What is a Container?
A container is an isolated process running on a shared host OS kernel.
- **Namespaces** — isolation of view (process tree, network, filesystem)
- **cgroups** — resource limits (CPU, memory, I/O)

Unlike VMs, containers share the host kernel → start in milliseconds, no guest OS overhead.

## Docker Image vs Container
- **Image** — read-only stack of layers built from a Dockerfile
- **Container** — running instance of an image with a writable layer on top
- **Registry** — where images are stored (Docker Hub, ACR, ECR)

## Layer Caching — The Golden Rule
Put least-changing instructions at the TOP, most-changing at the BOTTOM.

```dockerfile
FROM python:3.11
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . /app
```

## Key Dockerfile Instructions
| Instruction | Purpose |
|---|---|
| FROM | Base image |
| RUN | Execute command during build |
| COPY | Copy files from host into image |
| WORKDIR | Set working directory |
| ENV | Set environment variables |
| EXPOSE | Document port (informational) |
| CMD | Default command at start (overridable) |
| ENTRYPOINT | Fixed command — CMD becomes its arguments |

## Interview Answer
A Docker image is a stack of immutable content-addressed layers. Each layer identified by SHA256 hash — unchanged layers reused from cache. In production we push to ACR and AKS pulls only changed layers.

## Quick Revision (Flashcards)
Q: What two kernel features give containers isolation and resource limits?
A: Namespaces (isolation) and cgroups (resource limits)

Q: What is a Docker image?
A: A read-only stack of immutable layers built from a Dockerfile

Q: What is a container?
A: A running instance of an image with a thin writable layer on top

Q: Why does layer order in Dockerfile matter?
A: Docker caches layers — least-changing at top means faster rebuilds

Q: What does SHA256 do for Docker layers?
A: Identifies each layer by content hash — same content = cached, changed content = rebuild
