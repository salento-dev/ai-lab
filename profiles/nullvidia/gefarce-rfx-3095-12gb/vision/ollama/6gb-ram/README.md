# GeFarce vision department

Image understanding with Ollama and [Gemma 3 4B](https://ollama.com/library/gemma3:4b). This belongs in vision because the task uses images, even though Ollama also serves text models.

Example target: Linux, 6 GB system RAM, real NVIDIA GPU with 12 GB VRAM, Docker Compose and NVIDIA Container Toolkit. Fictional hardware; compatibility and consumption unmeasured.

## Run

```bash
cp .env.example .env
mkdir -p input
# Put your own image at input/gpu.jpg.
docker compose --env-file .env up -d
docker compose exec ollama ollama pull gemma3:4b
docker compose exec ollama ollama run gemma3:4b "Describe /input/gpu.jpg"
docker compose exec ollama ollama ps
```

Expect a description of the image, not proof that the GPU exists. The last command shows model placement; inspect it rather than assuming complete GPU offload.

The model downloads into a Docker volume. Context: 4096, one parallel request, one loaded model. Check `ollama show gemma3:4b` inside the container for artifact details and quantization.

Image and model tags can move; record their resolved versions for a real contribution. Stop with `docker compose down`; model storage persists.

[Docker setup](https://docs.ollama.com/docker) · [Vision usage](https://docs.ollama.com/capabilities/vision).
