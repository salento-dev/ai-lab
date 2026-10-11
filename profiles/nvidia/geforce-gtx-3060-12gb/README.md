# NVIDIA GeForce RTX 3060 · 12 GB

Real hardware profile: NVIDIA GeForce RTX 3060 12 GB (GA107) on an
Ubuntu server with 32 GB RAM, running llama.cpp inside Docker on the
NVIDIA CUDA backend.

| Spec | Value |
| --- | --- |
| GPU | NVIDIA GeForce RTX 3060 (GA107) |
| Memory | 12 GB GDDR6, 192-bit, ~360 GB/s |
| CUDA cores | 3584 |
| Interface | PCIe 4.0 x16 |
| Host | Ubuntu server, 32 GB RAM |

## Setups

Single-model variants of the owner's 10-model stack on the RTX 3060
12 GB, one directory per model:

**LLM / llama-swap**

- [Gemma 4 26B A4B IT QAT (Q4_K_XL)](llm/llama-swap/32gb-ram/gemma-4-26b-a4b-q4/)
- [Gemma 4 26B A4B IT QAT Uncensored HauhauCS-Balanced (IQ4_XS)](llm/llama-swap/32gb-ram/gemma-4-26b-a4b-q4-uncensored/)
- [Gemma 4 E4B Uncensored HauhauCS-Aggressive (Q8_K_P)](llm/llama-swap/32gb-ram/gemma-4-e4b-uncensored-q8/)
- [Qwen 3.5 9B Null-Space Abliterated (Q8_0)](llm/llama-swap/32gb-ram/qwen-3-5-9b-abliterated/)
- [Qwen 3 Coder 30B A3B UD (Q4_K_XL)](llm/llama-swap/32gb-ram/qwen-3-coder-30b-a3b/)
- [Qwen 3.6 35B A3B Uncensored HauhauCS-Aggressive (Q4_K_P)](llm/llama-swap/32gb-ram/qwen-3-6-35b-uncensored/)
- [Qwen 3.6 35B A3B Uncensored HauhauCS-Aggressive Multimodal (Q4_K_P)](llm/llama-swap/32gb-ram/qwen-3-6-35b-uncensored-vision/)
- [Spark-X2.5 4B (Q8_0)](llm/llama-swap/32gb-ram/spark-x2-5-4b/)

**LLM / llama-cpp-bonsai**

- [Ternary Bonsai 2 27B (PQ2_0)](llm/llama-cpp-bonsai/32gb-ram/ternary-bonsai-2-27b/)
- [Ternary Bonsai 2 27B Multimodal (PQ2_0)](llm/llama-cpp-bonsai/32gb-ram/ternary-bonsai-2-27b-visual/)

## Runtime notes

- The llama-swap models use `ghcr.io/mostlygeek/llama-swap:cuda`
  (llama.cpp built for NVIDIA CUDA). GPU access is via
  `deploy.resources.reservations.devices` (nvidia driver,
  `NVIDIA Container Toolkit` required).
- The Ternary Bonsai models run on the standalone image
  `emanuelepaiano/llama-cpp-bonsai2:cuda` (published by the owner on
  Docker Hub from the private `llama-cpp-bonsai:cuda`). In the original
  stack the bonsai container was spawned via `docker run` from inside
  llama-swap; here it is a first-class service of the same compose.
- Each stack is standalone and exposes port `11434` (Ollama-compatible
  endpoint). The original multi-model stack joined an external
  `ollama-network`; it is not reproduced here. Run one stack at a time.
- GGUF files come from Hugging Face and live in
  `${MODELS_HOST_DIR}` (mounted as `/models`); no weights in this
  repository.
- `--n-gpu-layers 99`, `--cpu-moe` / `--n-cpu-moe` values are the
  owner's: on the 12 GB card the large 35B A3B Mixture-of-Experts models
  offload expert layers to CPU.

## What was tried

- Tested on the owner's hardware: Goose (coding agent), OpenWebUI (chat,
  web search, image recognition on the multimodal models).
- Token throughput: ~14-50 tok/s depending on model (owner-reported range,
  no formal benchmark here).
- Configurations transcribed from the owner's running compose; not
  re-verified by this repository. GPU memory usage and per-model
  throughput: not measured.
