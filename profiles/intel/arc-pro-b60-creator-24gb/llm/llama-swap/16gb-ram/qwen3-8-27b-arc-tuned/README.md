# Qwen3.8 27B (Intel Arc tuned, Q4_K)

llama.cpp server for a 27B model with speculative decoding, run via
[llama-swap](https://github.com/mostlygeek/llama-swap) on the
[Intel Arc Pro B60 Creator 24 GB](../../../../README.md) using the
SYCL / Level Zero backend in the container.

## Model

- GGUF: `Qwen3.8-27B-GSQ-RCO-IQ3_S-Intel-Arc-Tuned-MTP-Q4_K.gguf` — Q4_K,
  GSQ-RCO IQ3_S base tuned for Intel Arc, includes MTP draft weights.
- Vision projector: `mmproj-BF16.gguf` (BF16).
- Custom chat template: `chat_templates/qwen-sharp.jinja`, loaded via `--jinja`.
- Context: 200000 tokens. KV cache quantized to q4_0 (K and V).
- GPU offload: all layers on GPU (`-ngl 99`, draft `-ngld 99`), flash
  attention on. Threads: `-t 4`, batch `-b 1024 -ub 1024 -tb 6`.
- Speculative decoding: `ngram-mod` + `draft-mtp` (ngram match window 24,
  min 1 / max 3; draft max 3 tokens, min probability 0.5).
- Reasoning preserved: `--reasoning-preserve`.

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
  -d '{"model":"qwen3.8-27b-b60","messages":[{"role":"user","content":"Say hi"}]}'
```

## Notes

- Single-model variant of the owner's running 11-model stack; config
  transcribed as provided. Not re-verified by this repository.
- RAM/VRAM usage and throughput: not measured.
