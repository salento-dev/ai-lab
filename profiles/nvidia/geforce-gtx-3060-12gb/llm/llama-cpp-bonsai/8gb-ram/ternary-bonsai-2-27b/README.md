# Ternary Bonsai 2 27B (PQ2_0)

Ternary Bonsai llama.cpp server, run directly in Docker on the
[NVIDIA GeForce RTX 3060 12 GB](../../../../README.md) Ubuntu server
host.

## Model

- GGUF: `Ternary-Bonsai-2-27B-PQ2_0.gguf` - PQ2_0 (ternary quantization).
- Source: Hugging Face (prism-ml/Ternary-Bonsai-2-27B-gguf).
- Context: 170000 tokens.
- GPU offload: all layers on GPU (`-ngl 99`), flash attention on.

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
  -d '{{"model":"ternary-bonsai-2-27b","messages":[{"role":"user","content":"Say hi"}]}}'
```

## Notes

- Standalone variant: in the owner's original stack the bonsai container
  was spawned from inside the llama-swap container via `docker run`
  (docker-in-docker, Docker socket mount). Here it is a first-class
  service of the same compose file, which is functionally equivalent for
  a single-model stack and drops the socket mount. Not re-verified by
  this repository.
- Tested on the owner's hardware with Goose (coding agent) and OpenWebUI
  (chat, web search, image recognition). Token throughput: ~14-50 tok/s
  depending on model (owner-reported range, no formal benchmark here).
