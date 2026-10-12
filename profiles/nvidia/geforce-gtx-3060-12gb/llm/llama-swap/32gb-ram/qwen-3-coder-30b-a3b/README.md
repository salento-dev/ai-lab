# Qwen 3 Coder 30B A3B UD (Q4_K_XL)

llama.cpp server, run via [llama-swap](https://github.com/mostlygeek/llama-swap)
on the [NVIDIA GeForce RTX 3060 12 GB](../../../../README.md) using the
CUDA backend in the container, Ubuntu server host.

## Model

- GGUF: `Qwen3-Coder-30B-A3B-Instruct-UD-Q4_K_XL.gguf` - Q4_K_XL.
- Source: Hugging Face.
- Context: 32768 tokens.
- GPU offload: 99 layers on GPU (`--n-gpu-layers 99`), 24 MoE layers on CPU (`--n-cpu-moe 24`).

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
  -d '{{"model":"qwen3-coder-30b","messages":[{"role":"user","content":"Say hi"}]}}'
```

## Notes

- Single-model variant of the owner's 10-model stack on the RTX 3060 12
  GB; transcribed from the original compose. Not re-verified by this
  repository.
- Tested on the owner's hardware with Goose (coding agent) and OpenWebUI
  (chat, web search, image recognition). Token throughput: ~14-50 tok/s
  depending on model (owner-reported range, no formal benchmark here).
