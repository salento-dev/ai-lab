# ai-lab

Community configurations for running AI locally, organized by hardware.

Share a setup that works for you, with configuration files and a short README. Include benchmarks when you have them; if you do not, the configuration is still useful.

## Configurations

| Hardware | Setups | Status |
| --- | --- | --- |
| [Nullvidia GeFarce RFX 3095 · 12 GB](profiles/nullvidia/gefarce-rfx-3095-12gb/) | LLM, diffusion, audio, vision, embeddings | Fictional 6 GB RAM example |
| [Intel Arc Pro B60 Creator · 24 GB](profiles/intel/arc-pro-b60-creator-24gb/) | LLM (llama-swap, 11 models) | Real hardware, 16 GB RAM profile |

Nullvidia is a temporary example profile, to be removed once real setups populate the catalog. Add yours following [CONTRIBUTING.md](CONTRIBUTING.md).

## Layout

```text
profiles/<vendor>/<device>/<workload>/<runtime-or-stack>/[<system-profile>/]
```

Choose the workload by what the setup does:

| Folder | Task | Example stacks |
| --- | --- | --- |
| `llm` | Text generation and language model inference | llama.cpp, Ollama, vLLM, SGLang, OpenVINO, MLX |
| `diffusion` | Image generation | ComfyUI, Forge, Diffusers |
| `audio` | Speech-to-text, text-to-speech, audio generation | whisper.cpp, faster-whisper, Piper, Kokoro |
| `vision` | OCR, detection, classification, image understanding | Ollama/llama.cpp for VLMs, ONNX Runtime, OpenVINO, TensorRT |
| `embeddings` | Semantic vectors for search and RAG | TEI, sentence-transformers, Ollama, llama.cpp |

These are organizational examples, not a compatibility list. The same runtime can serve different tasks. Add other workloads when someone shares a setup. Add the optional system profile only when it distinguishes configurations. Models belong in the README, not in a mandatory directory level.

Each setup has a README and the configuration files it needs. Docker Compose is optional.

Coding agents follow [AGENTS.md](AGENTS.md). CI checks Compose syntax where present; contributors describe what actually works on their hardware.
