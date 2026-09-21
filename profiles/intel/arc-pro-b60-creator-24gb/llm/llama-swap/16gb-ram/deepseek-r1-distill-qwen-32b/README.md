# DeepSeek R1 Distill Qwen 32B (Q4_K_M)

llama.cpp server, run via [llama-swap](https://github.com/mostlygeek/llama-swap)
on the [Intel Arc Pro B60 Creator 24 GB](../../../../README.md) using the
SYCL / Level Zero backend in the container.

## Model

- GGUF: `DeepSeek-R1-Distill-Qwen-32B/DeepSeek-R1-Distill-Qwen-32B-Q4_K_M.gguf` — Q4_K_M.
- Context: 8192 tokens.
- GPU offload: all layers on GPU (`--n-gpu-layers 999`), flash attention on.
- `--jinja` chat template.

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
  -d '{"model":"deepseek-r1-distill-qwen-32b","messages":[{"role":"user","content":"Say hi"}]}'
```

## Notes

- Single-model variant of the owner's running 11-model stack; config
  transcribed as provided. Not re-verified by this repository.
- RAM/VRAM usage and throughput: not measured.
