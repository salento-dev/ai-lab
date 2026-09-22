# Qwen3.5 27B (Q4_K_M)

llama.cpp server for a 27B model, run via
[llama-swap](https://github.com/mostlygeek/llama-swap) on the
[Intel Arc Pro B60 Creator 24 GB](../../../../README.md) using the
SYCL / Level Zero backend in the container.

## Model

- GGUF: `Qwen3.5-27B/Qwen3.5-27B.Q4_K_M.gguf` — Q4_K_M.
- Context: 131072 tokens. KV cache quantized to q8_0 (K and V).
- GPU offload: all layers on GPU (`-ngl 999`), flash attention on, `-np 1`.
- Sampling: temp 0.6, top-p 0.95, top-k 20, min-p 0.0.
- Reasoning on, with `preserve_thinking: true` chat template kwarg; `--jinja`.

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
  -d '{"model":"qwen3.5-27b","messages":[{"role":"user","content":"Say hi"}]}'
```

## Notes

- Single-model variant of the owner's running 11-model stack; config
  transcribed as provided. Not re-verified by this repository.
- RAM/VRAM usage and throughput: not measured.
