# Qwen 3.5 9B Null-Space Abliterated (Q8_0)

llama.cpp server, run via [llama-swap](https://github.com/mostlygeek/llama-swap)
on the [NVIDIA GeForce RTX 3060 12 GB](../../../../README.md) using the
CUDA backend in the container, Ubuntu server host.

## Model

- GGUF: `qwen3.5-9b-null-space-abliterated-q8_0.gguf` - Q8_0.
- Source: Hugging Face.
- Context: 65536 tokens.
- GPU offload: 99 layers on GPU (`--n-gpu-layers 99`).

## Run

```bash
cp .env.example .env
# Point MODELS_HOST_DIR at the directory mounted as /models.
docker compose --env-file .env up -d
```

## Verify

```bash
curl -f http://localhost:11434/health
curl http://localhost:11434/v1/chat/completions \
  -H 'Content-Type: application/json' \
  -d '{{"model":"qwen3.5-9b-abliterated","messages":[{"role":"user","content":"Say hi"}]}}'
```

## Notes

- Single-model variant of the owner's 10-model stack on the RTX 3060 12
  GB; transcribed from the original compose. Not re-verified by this
  repository.
- Tested on the owner's hardware with Goose (coding agent) and OpenWebUI
  (chat, web search, image recognition). Token throughput: ~14-50 tok/s
  depending on model (owner-reported range, no formal benchmark here).
