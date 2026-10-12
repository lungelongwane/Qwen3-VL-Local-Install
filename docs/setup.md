# Setup

## Prerequisites

- Windows 10/11 with [Docker Desktop](https://www.docker.com/products/docker-desktop/) (WSL2 backend)
- Enough RAM for the model you choose. Docker Desktop's memory limit applies (ours showed ~11 GB available).

## Install

1. Clone this repo and `cd` into it.
2. Start the stack:
   ```bash
   docker compose up -d
   ```
3. Pull a model:
   ```bash
   docker exec -it ollama ollama pull llama3.2
   ```
4. Open http://localhost:3000, create the admin account (stored locally), and select the model.

## Connecting Open WebUI to Ollama

Admin Panel → Settings → Connections → Ollama API.

| Situation | URL to use |
|-----------|-----------|
| Both containers in the same compose project (this repo) | `http://ollama:11434` |
| Ollama is a separate container or runs natively on Windows | `http://host.docker.internal:11434` |
| Testing from your browser or PowerShell | `http://localhost:11434` |

Click the refresh icon next to the URL to verify the connection.

## Data and volumes

Models and chat history live in Docker **volumes** (`ollama`, `open-webui`), not in the containers. Removing a container does not delete them. Do not delete the volumes unless you want to re-download models and lose chats.

## Optional: n8n

n8n can call Ollama at `http://host.docker.internal:11434` (or `http://ollama:11434` if on the same network). Its UI is at http://localhost:5678.
