# Qwen3-VL (vision-language model)

Qwen3-VL accepts **images as well as text**, so you can ask questions about screenshots, photos, documents, charts, and so on. The `8b` variant is about 8.8B parameters.

> Tags, sizes, and version requirements change. Confirm on the model page: https://ollama.com/library/qwen3-vl

## Requirements

- A **recent Ollama version**. Qwen3-VL needs a newer release than older text-only models. If the pull fails with a "newer version of Ollama" message, update the image:
  ```bash
  docker compose pull ollama && docker compose up -d
  ```
- RAM: the 8B model is roughly 6 GB on disk at the default 4-bit quantization. Plan on about 8–10 GB in use once loaded. Images add extra memory and processing time. Docker should have 12 GB or more (see [prerequisites](prerequisites.md)).

## Pull and run

```bash
docker exec -it ollama ollama pull qwen3-vl:8b
docker exec -it ollama ollama run qwen3-vl:8b
```

Smaller options for slower machines: `qwen3-vl:4b`, `qwen3-vl:2b`. Variants with `-instruct` or `-thinking` in the tag may exist. Instruct answers directly. Thinking prints its reasoning first and is slower on CPU. Check the model page for the current tags.

## Use it in Open WebUI

1. Open http://localhost:3000 and select `qwen3-vl:8b` from the model dropdown.
2. Click the **+** (attach) button in the chat box and upload an image, or drag and drop one in.
3. Ask a question, e.g. "What does this chart show?" or "Extract the text from this waybill."

## Use it from the API

```bash
curl http://localhost:11434/api/chat -d '{
  "model": "qwen3-vl:8b",
  "stream": false,
  "messages": [{
    "role": "user",
    "content": "Describe this image.",
    "images": ["<base64-encoded image>"]
  }]
}'
```

## Performance tips (CPU only, e.g. i5-6500 with 24 GB)

- Expect roughly 3–4 tokens/s for the text output, and a noticeable delay (often tens of seconds) before the first token while the image is processed.
- Use **smaller images**. Resize large photos to about 1024 px on the long edge before uploading.
- One image per question is much faster than several.
- Keep the context window modest. Longer contexts use more RAM and slow things down.
- If it feels too slow, switch to `qwen3-vl:4b`.

## Troubleshooting

| Problem | Fix |
|---|---|
| Pull says a newer Ollama is required | Update Ollama (`docker compose pull ollama && docker compose up -d`) |
| No attach button or the image is ignored | Make sure you selected a `qwen3-vl` model, not a text-only one |
| Container killed or very slow | Not enough memory: raise the WSL2 limit or use `qwen3-vl:4b` |
| Garbled or empty answers on an image | Try a smaller or clearer image, or rephrase the question |
