# Moving existing `docker run` containers to compose

If `ollama` and `open-webui` were started by hand, switching to compose means re-creating the containers. **Your data lives in volumes, so do not delete the volumes.**

1. Find the volume names the current containers use:
   ```bash
   docker inspect ollama --format "{{ json .Mounts }}"
   docker inspect open-webui --format "{{ json .Mounts }}"
   ```
2. **Back up first** (see [maintenance](maintenance.md)).
3. In `docker-compose.yml`, mark the volumes as external so compose reuses them. Use the exact names from step 1:
   ```yaml
   volumes:
     ollama:
       external: true
       name: <existing-ollama-volume>
     open-webui:
       external: true
       name: <existing-open-webui-volume>
   ```
4. Stop and remove only the containers (not volumes):
   ```bash
   docker stop ollama open-webui
   docker rm ollama open-webui
   ```
5. Start the stack:
   ```bash
   docker compose up -d
   ```
6. Confirm models and chats are still there at http://localhost:3000.

If the existing Open WebUI was bound to a bind-mount folder instead of a named volume, use that path in the compose `volumes:` entry instead.
