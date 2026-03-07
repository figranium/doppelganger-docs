# Installation via Docker Image (Standalone)

This guide covers installing Figranium using the pre-built Docker image hosted on the GitHub Container Registry (GHCR). This is the primary installation method, ideal for standalone deployments.

## Prerequisites

- [Docker](https://docs.docker.com/get-docker/) installed and running.

## Step-by-Step Installation

### 1. Pull the Docker Image

Pull the latest version of the Figranium image from GHCR:

```bash
docker pull ghcr.io/figranium/figranium:latest
```

### 2. Run the Container

Start a new container using the pulled image:

```bash
docker run -d \
  --name figranium \
  -p 11345:11345 \
  -p 54311:54311 \
  -v figranium_data:/app/data \
  -v figranium_captures:/app/public/captures \
  ghcr.io/figranium/figranium:latest
```

This command will:

- Run the container in detached mode (`-d`).
- Name the container `figranium`.
- Map port `11345` for the web interface.
- Map port `54311` for the VNC/noVNC viewer.
- Create and mount named volumes `figranium_data` (for `/app/data`) and `figranium_captures` (for `/app/public/captures`) for persistence.

### 3. Access the Application

Once the container is running, open your browser and navigate to:

[http://localhost:11345](http://localhost:11345)

## Configuration via Environment Variables

You can customize the container's behavior by passing environment variables using the `-e` flag:

```bash
docker run -d \
  --name figranium \
  -p 11345:11345 \
  -e PORT=11345 \
  -e SESSION_SECRET=your_secret_here \
  -v figranium_data:/app/data \
  -v figranium_captures:/app/public/captures \
  ghcr.io/figranium/figranium:latest
```

## Volume Persistence

To ensure your tasks, settings, and captures are preserved when the container is stopped or removed, always use volumes.

- **Named Volumes (Recommended)**: `-v figranium_data:/app/data -v figranium_captures:/app/public/captures`
- **Bind Mounts**: `-v /path/to/local/data:/app/data -v /path/to/local/captures:/app/public/captures`

The container stores its persistent data in `/app/data` and its captures in `/app/public/captures`.
