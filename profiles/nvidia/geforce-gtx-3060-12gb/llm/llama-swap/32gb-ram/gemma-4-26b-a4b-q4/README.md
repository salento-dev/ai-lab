# Gemma 4 26B A4B IT QAT (Q4_K_XL)

llama.cpp server, run via [llama-swap](https://github.com/mostlygeek/llama-swap)
on the [NVIDIA GeForce RTX 3060 12 GB](../../../../README.md) using the
CUDA backend in the container, Ubuntu server host.

## Model

- GGUF: `gemma-4-26B-A4B-it-qat-UD-Q4_K_XL.gguf` - Q4_K_XL.
- Source: Hugging Face.
- Context: 200000 tokens.
- GPU offload: 99 layers on GPU (`--n-gpu-layers 99`), 12 MoE layers on CPU (`--n-cpu-moe 12`).

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
  -d '{{"model":"gemma-4-26B-A4B-Q4","messages":[{"role":"user","content":"Say hi"}]}}'
```

## Notes

- Single-model variant of the owner's 10-model stack on the RTX 3060 12
  GB; transcribed from the original compose. Not re-verified by this
  repository.
- Tested on the owner's hardware with Goose (coding agent) and OpenWebUI
  (chat, web search, image recognition). Token throughput: ~14-50 tok/s
  depending on model (owner-reported range, no formal benchmark here).
