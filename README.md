# Ollama + Open WebUI on Docker (Windows)

Knowledge base for running local LLMs with [Ollama](https://ollama.com) and chatting with them through [Open WebUI](https://github.com/open-webui/open-webui), all in Docker Desktop.

## Architecture

```
Browser ──► http://localhost:3000 ──► open-webui (container, port 8080)
                                          │
                                          ▼  http://ollama:11434
                                      ollama (container, port 11434)
                                          │
                                          ▼
                                   models (Docker volume)
```

| Service      | Container    | Host port | URL                      |
|--------------|--------------|-----------|--------------------------|
| Ollama API   | `ollama`     | 11434     | http://localhost:11434   |
| Open WebUI   | `open-webui` | 3000      | http://localhost:3000    |
| n8n (optional) | `n8n`      | 5678      | http://localhost:5678    |

## Quick start

```bash
docker compose up -d
docker exec -it ollama ollama pull llama3.2
```

Then open http://localhost:3000, create the local admin account, and pick the model from the dropdown.

## Docs

- [Prerequisites](docs/prerequisites.md): WSL2, Docker Desktop, memory limits, optional GPU
- [Setup](docs/setup.md): install, compose file, connecting Open WebUI to Ollama
- [Migrate existing containers](docs/migrate-existing-containers.md): move `docker run` containers to compose without losing data
- [Models](docs/models.md): picking a model for your RAM
- [Qwen3-VL](docs/qwen3-vl.md): vision-language model setup, images in Open WebUI, CPU tips
- [Maintenance](docs/maintenance.md): updates, backup, restore, freeing disk space
- [Security](docs/security.md): sign-ups, loopback binding, firewall
- [Commands](docs/commands.md): everyday Docker and Ollama commands
- [Troubleshooting](docs/troubleshooting.md): errors we have hit and their fixes

## Key rule to remember

`host.docker.internal` only works **from inside a container**. From your browser or Windows, use `localhost`.
