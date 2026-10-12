# Prerequisites (fresh Windows machine)

1. **Enable virtualization** in BIOS/UEFI if it is off (Task Manager → Performance → CPU shows "Virtualization: Enabled").
2. **Install WSL2** (PowerShell as Administrator), then reboot:
   ```powershell
   wsl --install
   ```
3. **Install Docker Desktop** from https://www.docker.com/products/docker-desktop/ and keep "Use WSL 2 based engine" ticked.
4. **Verify:**
   ```powershell
   docker --version
   docker run --rm hello-world
   ```
5. **Give Docker enough memory:** Docker Desktop → Settings → Resources. For WSL2 you can cap it in `%UserProfile%\.wslconfig`:
   ```ini
   [wsl2]
   memory=10GB
   processors=4
   ```
   Then run `wsl --shutdown` and restart Docker Desktop.

## Disk space

Models are large (roughly 2–5 GB each for small/medium models). Keep 20 GB or more free on the drive Docker uses.

## GPU (optional)

With an NVIDIA GPU, install the latest NVIDIA driver and add this to the `ollama` service in `docker-compose.yml`:

```yaml
    deploy:
      resources:
        reservations:
          devices:
            - driver: nvidia
              count: all
              capabilities: [gpu]
```

Without a GPU, Ollama runs on CPU. It works but is slower, so use smaller models.
