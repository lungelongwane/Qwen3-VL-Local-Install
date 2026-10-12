# Maintenance

## Update to the latest versions

```bash
docker compose pull
docker compose up -d
```

Volumes are kept, so models and chats survive. Check the Open WebUI release notes for breaking changes before big version jumps.

## Back up a volume

Replace `<volume>` with the real volume name (`docker volume ls`):

```bash
docker run --rm -v <volume>:/data -v "%cd%":/backup alpine tar czf /backup/<volume>.tar.gz -C /data .
```

(In PowerShell use `${PWD}` instead of `%cd%`.)

Backing up `open-webui` (chats, users, settings) is the priority. Models in the `ollama` volume can simply be re-pulled.

## Restore a volume

```bash
docker run --rm -v <volume>:/data -v "%cd%":/backup alpine sh -c "cd /data && tar xzf /backup/<volume>.tar.gz"
```

## Free disk space

```bash
docker exec -it ollama ollama list      # see model sizes
docker exec -it ollama ollama rm <model>
docker image prune                      # remove unused images
```
