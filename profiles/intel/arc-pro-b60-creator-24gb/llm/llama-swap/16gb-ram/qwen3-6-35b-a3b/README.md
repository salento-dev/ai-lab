# Qwen3.6 35B A3B (UD Q3_K_XL)

MoE model (3B active parameters), run via
[llama-swap](https://github.com/mostlygeek/llama-swap) on the
[Intel Arc Pro B60 Creator 24 GB](../../../../README.md) using the
SYCL / Level Zero backend in the container.

## Model

- GGUF: `Qwen3.6-35B-A3B/Qwen3.6-35B-A3B-UD-Q3_K_XL.gguf` — Q3_K_XL.
- Context: 131760 tokens. KV cache quantized to q8_0 (K and V).
- GPU offload: all layers on GPU (`--n-gpu-layers 99`), flash attention on.
- Sampling: temp 0.7, top-p 0.80, top-k 20, min-p 0.0, repeat-penalty 1.05;
  `--jinja`.

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
  -d '{"model":"qwen3.6-35b-a3b","messages":[{"role":"user","content":"Say hi"}]}'
```

## Notes

- Single-model variant of the owner's running 11-model stack; config
  transcribed as provided. Not re-verified by this repository.
- RAM/VRAM usage and throughput: not measured.
