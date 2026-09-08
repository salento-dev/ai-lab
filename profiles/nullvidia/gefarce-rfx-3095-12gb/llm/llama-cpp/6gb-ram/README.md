# GeFarce LLM department

Illustrative setup for the fictional [RFX 3095](../../../README.md), with 6 GB installed system RAM. No hardware testing performed.

## Adapt and run

Use a real CUDA-capable GPU, compatible driver, Docker with NVIDIA Container Toolkit, and an externally obtained GGUF model.

```bash
cp .env.example .env
# Set a real model directory and filename in .env.
docker compose --env-file .env up -d
docker compose logs --tail=30 llama-server
```

Open http://localhost:8080 and send a short prompt once the model loads. If startup fails, check logs, model path, GPU access, and available memory.

The image uses the upstream moving tag. Pin its verified digest after testing, and record the model source and quantization in your real README. See [upstream Docker usage](https://github.com/ggml-org/llama.cpp/blob/master/docs/docker.md).

## Settings

Context: 4096 tokens. `GPU_LAYERS=99` requests up to 99 layers on the GPU; reduce it if the model does not fit. Actual RAM/VRAM usage: not measured.

`bring-your-own-brain.gguf` is a placeholder filename. Fictional throughput: 42 tok/s, certified by marketing. Actual throughput: not measured.
