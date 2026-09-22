# Qwen3.6 35B A3B Uncensored — HauhauCS Aggressive (Q4_K_M)

MoE vision model (3B active parameters), run via
[llama-swap](https://github.com/mostlygeek/llama-swap) on the
[Intel Arc Pro B60 Creator 24 GB](../../../../README.md) using the
SYCL / Level Zero backend in the container.

## Model

- GGUF: `Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive-Q4_K_M.gguf`
  — Q4_K_M.
- Vision projector: `Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive/mmproj-Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive-f16.gguf`
  (f16).
- Context: 8192 tokens.
- GPU offload: all layers on GPU (`--n-gpu-layers 999`), flash attention on;
  4 MoE experts kept on CPU (`--n-cpu-moe 4`).
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
  -d '{"model":"qwen3.6-35b-a3b-uncensored","messages":[{"role":"user","content":"Say hi"}]}'
```

## Notes

- Single-model variant of the owner's running 11-model stack; config
  transcribed as provided. Not re-verified by this repository.
- RAM/VRAM usage and throughput: not measured.
