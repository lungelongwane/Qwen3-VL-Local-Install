# Commands

## Stack

```bash
docker compose up -d        # start
docker compose down         # stop and remove containers (volumes are kept)
docker compose pull         # update images
docker compose logs -f      # follow logs
docker ps -a                # list all containers
```

## Ollama

```bash
docker exec -it ollama ollama list          # installed models
docker exec -it ollama ollama pull <model>  # download a model
docker exec -it ollama ollama run <model>   # chat in the terminal
docker exec -it ollama ollama rm <model>    # delete a model
```

## Health checks

```bash
curl http://localhost:11434            # prints "Ollama is running"
curl http://localhost:11434/api/tags   # JSON list of models
```

## Cleanup

```bash
docker rm <container>      # remove a stopped container (volumes untouched)
docker volume ls           # list volumes. Do NOT remove ollama / open-webui
```
