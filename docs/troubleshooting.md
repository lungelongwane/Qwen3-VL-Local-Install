# Troubleshooting

## "Hmmm... can't reach this page" at `host.docker.internal:11434`

**Cause:** `host.docker.internal` only resolves from inside a container. A Windows browser cannot resolve it.
**Fix:** use `http://localhost:11434` in the browser.

## Open WebUI shows no models

1. Check Ollama is up: `curl http://localhost:11434`.
2. Check a model is installed: `docker exec -it ollama ollama list`. If empty, pull one.
3. Admin Panel → Settings → Connections: set the Ollama URL (see [setup](setup.md)) and refresh.

## Random-named duplicate containers (e.g. `modest_napier`, `wonderful_gold`)

**Cause:** the same image was started with `docker run` without `--name` or ports, which gives it a random name.
**Fix:** delete them in Docker Desktop (trash icon) or `docker rm <name>`. Keep `ollama` and `open-webui`. Volumes are unaffected. Use `docker compose` to avoid creating duplicates.

## Port already in use

Another container or program is using 11434 or 3000. Find it with `docker ps`, or change the left side of the mapping in `docker-compose.yml` (e.g. `"3001:8080"`).

## Model is slow or the container crashes

Not enough memory. Try a smaller model (e.g. a 1B–3B parameter one) or raise Docker Desktop's memory limit (Settings → Resources).
