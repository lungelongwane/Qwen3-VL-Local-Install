# Security basics

- **Admin account:** the first account created in Open WebUI becomes admin. Use a strong password.
- **Disable open sign-ups** after creating your account: Admin Panel → Settings → General → turn off "Enable New Sign Ups".
- **Keep it local:** `ports: "3000:8080"` exposes the UI on all network interfaces. To restrict to this PC, bind to loopback:
  ```yaml
  ports:
    - "127.0.0.1:3000:8080"
  ```
  Do the same for Ollama (`127.0.0.1:11434:11434`). Ollama's API has **no authentication**, so never port-forward it to the internet.
- **Windows Firewall:** don't open ports 3000 or 11434 to the public profile.
- **Secrets:** keep API keys and passwords in a `.env` file (already in `.gitignore`), never in the compose file or docs committed to GitHub.
- **Updates:** pull new images regularly (see [maintenance](maintenance.md)).
