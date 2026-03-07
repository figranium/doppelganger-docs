# Installation via Docker Image

This guide covers installing Figranium using the pre-built Docker image hosted on Docker Hub. This is a secondary installation method, ideal for environments where you don't want to clone the repository.

## Prerequisites

- [Docker](https://docs.docker.com/get-docker/) installed and running.

## Step-by-Step Installation

### 1. Pull the Docker Image

Pull the latest version of the Figranium image from Docker Hub:

```bash
docker pull mnemosynestack/doppelganger:latest
```

### 2. Run the Container

Start a new container using the pulled image:

```bash
docker run -d \
  --name figranium \
  -p 11345:11345 \
  -p 54311:54311 \
  -v figranium_data:/app/data \
  mnemosynestack/doppelganger:latest
```

This command will:

- Run the container in detached mode (`-d`).
- Name the container `figranium`.
- Map port `11345` for the web interface.
- Map port `54311` for the VNC/noVNC viewer.
- Create and mount a named volume `figranium_data` to `/app/data` for persistence.

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
  mnemosynestack/doppelganger:latest
```

## Volume Persistence

To ensure your tasks and settings are preserved when the container is stopped or removed, always use a volume.

- **Named Volume (Recommended)**: `-v figranium_data:/app/data`
- **Bind Mount**: `-v /path/to/your/local/data:/app/data`

The container stores its persistent data in `/app/data`.
