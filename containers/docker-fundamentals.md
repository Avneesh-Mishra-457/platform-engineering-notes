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
COPY requirements.txt .          # changes rarely → cached
RUN pip install -r requirements.txt  # cached until deps change
COPY . /app                      # code changes often → last
```

## Key Dockerfile Instructions
| Instruction | Purpose |
|---|---|
| FROM | Base image |
| RUN | Execute command during build (creates a layer) |
| COPY | Copy files from host into image |
| WORKDIR | Set working directory inside container |
| ENV | Set environment variables |
| EXPOSE | Document which port app uses (informational) |
| CMD | Default command at container start (overridable) |
| ENTRYPOINT | Fixed command — CMD becomes its arguments |

## Interview Answer
A Docker image is a stack of immutable, content-addressed layers. Each layer is identified by a SHA256 hash — unchanged layers are reused from cache. In production we push to ACR and AKS pulls only the changed layers, not the full image each time.

## Production Context (Azure)
- Build locally → tag → az acr login → docker push to ACR
- AKS pulls from ACR layer by layer — only diff is transferred
- Containers are ephemeral — stateful data must live in Persistent Volumes
