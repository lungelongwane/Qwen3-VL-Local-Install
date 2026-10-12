# Choosing a model

Rule of thumb: the model file should fit in RAM with room to spare. Reference machine: 4 CPUs, ~11 GB RAM available to Docker, CPU only.

| RAM available | Suggested size | Examples (check https://ollama.com/library) |
|---------------|----------------|---------------------------------------------|
| 4–6 GB        | 1B–3B          | `llama3.2:1b`, `llama3.2:3b`, `qwen2.5:3b`  |
| 8–12 GB       | 3B–8B (4-bit)  | `llama3.1:8b`, `qwen2.5:7b`, `mistral`      |
| 16 GB+        | 8B–14B         | `qwen2.5:14b`                               |

Notes:
- Quantized tags (e.g. `q4_K_M`) are smaller and faster with a small quality loss.
- On CPU, expect a few tokens per second for 7B–8B models. Use 1B–3B for snappy replies.
- Pull with `docker exec -it ollama ollama pull <name>:<tag>`.
- Model names and sizes change often, so check the Ollama library for current options.
